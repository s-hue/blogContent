# 使用Let's Encrypt给网站添加HTTPS访问

## 为什么要使用HTTPS访问网站

HTTPS（Hypertext Transfer Protocol Secure）在中文里翻译为超文本传输安全协议，它是在原有的HTTP的基础上使用SSL/TLS来对数据包进行加密，保护数据传输的隐私性和完整性，防止数据窃听和中间人攻击的发生。

HTTPS的简单的理解为：

1. 网站的服务器会产生一对密钥（公钥和私钥）；
2. 服务器将公钥提供给证书认证机构（Certificate Authority，CA），CA将公钥放入数字证书并将该数字证书颁布给服务器；
3. 服务器将数字证书发送给用户，用户可以利用数字证书中的数字签名机制询问CA来确定收到的数字证书是否来自服务器；
4. 得到确认后，用户使用数字证书中的公钥来加密数据发送给服务器。
5. 服务器使用私钥解密来得到数据。

CA在其中的作用就是来提供数字证书来对公钥进行验证，确定其是否是伪造的。

CA机构有很多，有免费，也有收费的，对于个人站点、博客来说，免费的CA就可以了，本文推荐[Let's Encrypt](https://letsencrypt.org/)。

## Let's Encrypt安装流程

Let's Encrypt是一个免费的、自动化、开放的证书签发服务项目。Let's Encrypt的有效期为90天，需要定期进行更新。

（*本流程适用于CentOS 6 x64 + Apache 2.2，流程中的以网址www.example.com为例*）

1. Let's Encrypt推荐使用Certbot来安装配置Let's Encrypt：

```sh
    # wget https://dl.eff.org/certbot-auto
    # chmod a+x certbot-auto
    # ./certbot-auto -n
```

2. 上一步最后一条命令是用来只安装依赖包，下面开始生成证书：

```sh
    # ./certbot-auto certonly --email email@example.com --agree-tos --no-eff-email --webroot -w /home/wwwroot/www.example.com -d www.example.com -d example.com
```

3. 生成完成后，证书会自动保存在文件夹`/etc/letsencrypt/live/www.example.com/`下，两个文件名为`fullchain.pem`和`privkey.pem`。

## 设置Apache虚拟主机

1. 修改apache的配置文件`/usr/local/apache/conf/httpd.conf`，找到`httpd-ssl`并将前面的`#`号去掉后保存文件；

2. 编辑`httpd-ssl.conf`文件：

```sh
    # cat >/usr/local/apache/conf/extra/httpd-ssl.conf<<EOF
    > Listen 443
    > 
    > AddType application/x-x509-ca-cert .crt
    > AddType application/x-pkcs7-crl .crl
    > 
    > SSLCipherSuite EECDH+CHACHA20:EECDH+CHACHA20-draft:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5
    > SSLProxyCipherSuite EECDH+CHACHA20:EECDH+CHACHA20-draft:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5
    > SSLHonorCipherOrder on
    > 
    > SSLProtocol all -SSLv2 -SSLv3
    > SSLProxyProtocol all -SSLv2 -SSLv3
    > SSLPassPhraseDialog builtin
    > 
    > SSLSessionCache "shmcb:/usr/local/apache/logs/ssl_scache(512000)"
    > SSLSessionCacheTimeout 300
    > 
    > SSLMutex "file:/usr/local/apache/logs/ssl_mutex"
    > 
    > SSLStrictSNIVHostCheck on
    > NameVirtualHost *:443
    > EOF
```

3. 在apache虚拟主机配置文件`/usr/local/apache/conf/extra/httpd-vhosts.conf`中的文件最后加上SSL的配置内容：

```apache_conf
<VirtualHost *:443>
DocumentRoot "/home/wwwroot/www.example.com"   #网站目录
ServerName www.example.com:443   #域名
ServerAdmin test@example.com      #邮箱
ErrorLog "/home/wwwlogs/www.example.com-error_log"   #错误日志
CustomLog "/home/wwwlogs/www.example.com-access_log" common    #访问日志
SSLEngine on
SSLCertificateFile /etc/letsencrypt/live/www.example.com/fullchain.pem  #生成的证书路径
SSLCertificateKeyFile /etc/letsencrypt/live/www.example.com/privkey.pem  #生成的证书路径
<Directory "/home/wwwroot/www.example.com">   #网站目录
    SetOutputFilter DEFLATE
    Options FollowSymLinks
    AllowOverride All
    Order allow,deny
    Allow from all
    DirectoryIndex index.html index.php
</Directory>
</VirtualHost>
```

4. 执行Apache重启命令使修改生效（如果有错误提示按提示进行修改后重复本命令）：

```sh
    # /etc/init.d/httpd restart
```

## HTTP自动跳转到HTTPS

本处使用将全部的http请求跳转到HTTPS的方式：

1. 开启Apache的Rewrite模块：修改apache的配置文件`/usr/local/apache/conf/httpd.conf`，找到`LoadModule rewrite_module modules/mod_rewrite.so`并将前面的`#`号去掉后保存文件。

2. 修改apache虚拟主机配置文件`/usr/local/apache/conf/extra/httpd-vhosts.conf`为：

```apache_conf
Listen 443
NameVirtualHost *:443
<VirtualHost *:443>
DocumentRoot "/home/wwwroot/www.example.com"   #网站目录
ServerName www.example.com:443   #域名
ServerAdmin test@example.com      #邮箱
ErrorLog "/home/wwwlogs/www.example.com-error_log"   #错误日志
CustomLog "/home/wwwlogs/www.example.com-access_log" common    #访问日志
SSLEngine on
SSLCertificateFile /etc/letsencrypt/live/www.example.com/fullchain.pem  #生成的证书路径
SSLCertificateKeyFile /etc/letsencrypt/live/www.example.com/privkey.pem  #生成的证书路径
<Directory "/home/wwwroot/www.example.com">   #网站目录
    SetOutputFilter DEFLATE
    Options FollowSymLinks
    AllowOverride All
    Order allow,deny
    Allow from all
    DirectoryIndex index.html index.php
</Directory>
</VirtualHost>
<VirtualHost *:80>
RewriteEngine on
RewriteCond %{SERVER_PORT} !^443$
RewriteRule ^/?(.*)$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]
</VirtualHost>
```

## 证书续期

因为证书有效期只有90天，所以建议60左右的时候进行一次续期，续期很简单可以交给crontab进行完成。如果有经常查看邮箱的习惯，官方会在证书到期前向你发送邮件，在发到邮件提示后，手动进行更新操作。自动续期的操作过程为：

1. 新建文件`certbot-autorenew-cron`设置certbot-auto的更新操作命令：

```sh
13 5,14 * */2 * /path/to/certbot-auto renew
```

这句话说的是每隔两个月的5:13和14:13时刻，对证书进行更新。在两个时间点进行更新是为了防止出现第一个时间点更新不成功的情况。

2. 用`crontab`来启动这个定时任务：

```sh
    # crontab certbot-autorenew-cron
```

经过上述过程后，网站的HTTPS升级工作就完成了。

## 证书到期了咋办

证书不小心到期了，可以使用下面的方法强制更新：

```sh
    # /path/to/certbot-auto renew --force-renew
    # /etc/init.d/httpd restart
```

发现crontab没有自动更新证书，所以按网上的建议，重新设置了更新命令，效果待测试。

```sh
    # 13 5,14 * */2 * /path/to/certbot-auto renew --quiet; /etc/init.d/httpd graceful
```

## 参考链接

[Certbot](https://certbot.eff.org/)

[免费SSL安全证书Let's Encrypt安装使用教程(附Nginx/Apache配置)](https://www.vpser.net/build/letsencrypt-free-ssl.html)

[月与灯依旧](https://www.zhukun.net/archives/8104)
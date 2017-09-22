# LAMP环境安全设置

本文记录LAMP环境安装之后的一些常用设置。

## PHPMyAdmin目录重命名

PHPMyAdmin是常用来管理MySQL数据库的默认登录入口，其默认路径位置是：
```
域名或IP/phpmyadmin
```
为了提高安全性，有必要将这个目录进行重命名，其默认路径为：
```
/home/wwwroot/default/phpmyadmin/
```

我们使用Xshell连接到VPS，使用下面的命令打开上层default目录，然后将phpmyadmin重命名新目录newcontent（newcontent可以是你想要改成的任何新目录名字）
```
    # cd /home/wwwroot/default/
    # mv phpmyadmin newcontent
```

## 修改SSH登陆VPS的端口

通常使用SSH方式登陆VPS的默认端口为22，我可以将这个端口号改为另外一个端口，比如：666，在CentOS中的修改端口的命令为：
```
    # sed -i 's/#Port 22/Port 666/g' /etc/ssh/sshd_config
```

## fail2ban

fail2ban是Linux上著名的入侵保护的开源框架，可以检测可疑的行为自动触发不同的防御动作，防护VPS遭到黑客的暴力密码入侵。

在安装fail2ban之前需要安装EPEL源，过程如下:

1. 确定系统的版本。
```
    # cat /etc/redhat-release
    CentOS release 6.9 (Final)
```
2. 根据系统版本安装相应的EPEL软件源。
```
    # wget http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
    # rpm -ivh epel-release-6-8.noarch.rpm
```
3. 安装完成后，测试EPEL是否添加到源列表中，成功安装后epel会出现在repo id中：
```
    # yum repolist
```

下面进行安装fail2ban：
```
    # yum install fail2ban
```
成功安装后，输入命令：
```
    # fail2ban-client ping
```
会返回消息：
```
    # Server replied: pong
```
将其设置为开机自启动：
```
    # chkconfig fail2ban on
```
到此，fail2ban就完成安装过程。

## 禁用Linux多余端口
因为我们的VPS没有太多的操作和应用，因此将多余的端口关闭，只留下常用端口是非常必要的。我们通过配置iptables来达到这个目的。

***iptables的配置很复杂，请谨慎操作，不要出现错误***

1. 清空默认规则：
```
    # iptables -F
```
2. 允许默认的SSH端口22：
```
    # iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    # iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
```
3. 允许本机访问本机：
```
    # iptables -A INPUT -s 127.0.0.1 -d 127.0.0.1 -j ACCEPT
    # iptables -A OUTPUT -s 127.0.0.1 -d 127.0.0.1 -j ACCEPT
```
4. 允许自定义的SSH端口666：
```
    # iptables -A INPUT -p tcp -s 0/0 --dport 666 -j ACCEPT
    # iptables -A OUTPUT -p tcp --sport 666 -m state --state ESTABLISHED -j ACCEPT
```
5. 允许http、https端口80，443：
```
    # iptables -A INPUT -p tcp -s 0/0 --dport 80 -j ACCEPT
    # iptables -A OUTPUT -p tcp --sport 80 -m state --state ESTABLISHED -j ACCEPT
    # iptables -A INPUT -p tcp -s 0/0 --dport 443 -j ACCEPT
    # iptables -A OUTPUT -p tcp --sport 443 -m state --state ESTABLISHED -j ACCEPT
```
6. 允许SSR端口，以444 555为例，有几个添加几个：
```
    # iptables -A INPUT -p tcp -s 0/0 --dport 444 -j ACCEPT
    # iptables -A OUTPUT -p tcp --sport 444 -m state --state ESTABLISHED -j ACCEPT
    # iptables -A INPUT -p tcp -s 0/0 --dport 555 -j ACCEPT
    # iptables -A OUTPUT -p tcp --sport 555 -m state --state ESTABLISHED -j ACCEPT
```
7. 保存iptables配置:
```
    # iptables-save > /etc/sysconfig/iptables
```
8. 重载iptables:
```
    # iptables -L
```

# SSR服务端配置说明

## 基本的配置文件

SSR服务端配置文件（位于`/etc/shadowsocks.json`）大体上为如下内容：

```json
{
"server": "0.0.0.0",                    // 监听地址，不用修改
"server_ipv6":"[::]",                   // ipv6监听地址，不用修改
"server_port": 1234,                    // ** 监听的服务器端口
"local_address": "127.0.0.1",           // 本地监听地址，不用修改
"local_port": 1080,                     // 本地监听端口，不用修改
"password": "1234567890",               // ** 密码
"timeout": 120,                         // 超时时间
"method": "aes-256-cfb",                // ** 加密方式，一般使用rc4-md5, salsa20, chacha20
"protocol": "auth_sha1_compatible",     // ** 协议插件
"protocol_param": "",                   // 协议插件的参数
"obfs": "http_simple_compatible",       // ** 混淆插件
"obfs_param": "",                       // 混淆插件的参数
"dns_ipv6": true,                       // 是否优先使用IPv6地址，有IPv6时可开启
"redirect": "",                         // 重定向参数
"fast_open": false,                     // 是否使用TCP_FASTOPEN
"workers":1                             // 一般不用修改
}
```
 
（*上面各选项中`//`为说明该参数的含义，在编辑JSON文件时请去除注释内容。一般情况下只需要修改上面带`**`标示的五个选项即可*）

## 关键参数说明

1. protocol可以选择的协议有：

+ “origin” ： 原版协议
+ “verify_simple”	： 带校验的协议
+ “verify_deflate”	： 带压缩的协议
+ “verify_sha1″	： 带验证抗CCA攻击的协议，可兼容libev的OTA
+ “auth_simple”	： 抗重放攻击的协议
+ “auth_sha1″ ： 带验证抗CCA攻击且抗重放攻击的协议
+ “auth_sha1_v2″ ： 类似”auth_sha1″，提供更好的长度混淆特性

2. obfs可以选择的混淆插件有：

+ “plain” ： 不混淆
+ “http_simple” ： 伪装为http协议
+ “tls_simple” ： 伪装为tls协议（不建议使用）
+ “random_head”	： 发送一个随机包再通讯的协议
+ “tls1.2_ticket_auth” ： 伪装为tls ticket握手协议（强烈推荐），同时能抗重放攻击

（**注：客户端的protocol和obfs配置必须与服务端的一致。**）

3. redirect参数的值为空字符串或一个列表，在连接方的数据不正确的时候，把数据重定向到列表中的其中一个地址和端口（不写端口则视为80），以伪装为目标服务器。如：

```json
“redirect”:[“bing.com”, “facebook.com:443″],
```

4. dns_ipv6参数为true则指定服务器优先使用IPv6地址。仅当服务器能访问IPv6地址时可以用，否则会导致有IPv6地址的网站无法打开。

## 多端口配置

多端口有两种情况：所有端口使用相同的加密方式、协议插件和混淆插件；不同端口有不同的组合方式。

第一种情况只用修改对应的端口和密码就行，如：

```json
{
"server": "0.0.0.0",
"server_ipv6":"[::]",
"local_address": "127.0.0.1",
"local_port": 1080,
"port_password": {
    "1314":"password1",
    "893":"1234567890"
    },
"timeout": 120,
"method": "chacha20",
"protocol": "auth_sha1_compatible",
"protocol_param": "",
"obfs": "http_simple_compatible",
"obfs_param": "",
"dns_ipv6": true,
"redirect": "",
"fast_open": false,
"workers":1
}
```

如果要为每个端口使用特殊的配置，则可以在`“port_password`中进行设置，没有详细设置的端口会使用后面的默认设置项。如：

```json
{
"server": "0.0.0.0",
"server_ipv6":"[::]",
"local_address": "127.0.0.1",
"local_port": 1080,
"port_password": {
    "1314":"password1",
    "80":{"protocol":"auth_sha1", "password":"123457", "obfs":"http_simple", "obfs_param":"www.baidu.com"},
    "8388":{"protocol":"auth_sha1_v2", "password":"123456", "obfs":"tls1.2_ticket_auth", "obfs_param":""},
    "8389":{"protocol":"origin", "password":"123456", "obfs":"plain", "obfs_param":""}
    },
"timeout": 120,
"method": "chacha20",
"protocol": "auth_sha1_compatible",
"protocol_param": "",
"obfs": "http_simple_compatible",
"obfs_param": "",
"dns_ipv6": true,
"redirect": "",
"fast_open": false,
"workers":1
}
```

## 常用命令

启动、停止、重启、查看状态的命令分别为：

```sh
# /etc/init.d/shadowsocks start
# /etc/init.d/shadowsocks stop
# /etc/init.d/shadowsocks restart
# /etc/init.d/shadowsocks status
```

使用重启命令可以修改生效。

## 相关的路径信息

配置文件路径：`/etc/shadowsocks.json`

日志文件路径：`/var/log/shadowsocksr.log`

代码安装路径：`/usr/local/shadowsocks`
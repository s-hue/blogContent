# VPS搭建个人站点和ShadowsocksR记录

很久以前就想着可以自己做个小网站，写点自己的东西，并把自己学习的东西做个总结，但是一直找不到时间（其实就是懒）。

现在终于迈出第一步，参考了网络上各位大神们的教程，可以把基本的框架做好，等待慢慢的完善自己的站点。这篇文章就记录下我的VPS建站历程。

## 准备工作

***思想上的准备：***建立站点不需要什么高深的技术知识，我们早就进入互联网的时代，各种教程网上遍地都是，只要自己照着步骤走，就不会有任何问题。*（就算有问题也可以马上搜索找到解决方案）*

***物质准备：***一台可以顺畅浏览互联网的电脑，一张还有几百块人民币余额的银行卡。

## 购买VPS
VPS（Virtual Private Server），中文是虚拟专用服务器，简单的可以理解为一台远端的电脑，你可以使用特殊的工具进行访问设置。

现在VPS提供商有很多，可以按照自己的需求来选择不同的供应商。本人推荐[美国Vultr公司](https://www.vultr.com/?ref=7214452)，它提供有2.5美元/月的VPS，足够新手来操作练手，更为方便的是可以使用[支付宝](https://www.alipay.com/)直接进行人民币结算来充值帐户，不用烦心美元兑换的问题。

Vultr公司提供了日本和新加坡的机房已供选择，但是这两个地方的最低价格VPS经常满员，如果没有速度上的严格要求，选择美国的机房也可以完全满足个人站点的访问速度要求。

本人购买Vultr VPS的过程如下：

1. 打开[Vultr官网](https://www.vultr.com/?ref=7214452)，点击右上角的Create Account，输入邮箱和密码进行注册即可。如果要长期使用，推荐登陆后台完善个人的相关信息。（其主页上也有接下来步骤的操作动画，可以进行查看）

2. 登陆后台，选择最右边的Servers，再选择左边的蓝底加号（+），开始VPSvps选择。

![VPS设置开始](https://jynbba.bn1304.livefilestore.com/y4m2HFtRdfrd989g-rDY5BvjF0gkUfiCMsIgIXPyRl0KWR7MBjT7fsFRUJqEFQdD4IogvmSfzl04rCKR7Sx_3ObmfyVkuX7zLicJF2SvCCRD94xrU8wimI-bG0b4B44pm5pVwE8EQZ_WmeY1xQmozWJL-FgEyGLbAAM1SclH6Xrr9QNMyPQjj2MmtX-QooSzIi6LGaMU1kNPSh7uIvpJOhvHA?width=1338&height=186&cropmode=none)

3. 按照自己的需求选择机房的位置，我选择在Miami（哎，东京和新加坡的便宜VPS没有了）。

![VPS机房位置](https://jynwpg.bn1304.livefilestore.com/y4mQGKoxp7LgZPOxkYWxk5f12naPZN4GNL8AuZ0mFlN1-tK9SV5yjfZxvDWAD0MKGjGXv8yLoK6T_1ePCMmNoxvmVNFG11NHTFCkm38bgqJK42WxKTROKDiPc4GSfCZfH-Ecx2r9ISfLMwT5ChfuBY_B6MTUIAum-GCi_zjQuMfItkIAHCMgQW5PDWecgYOLKgFRogRmkc1KDETiBOt3YYiMg?width=832&height=494&cropmode=none)

4. 选择系统型号，其实就是选择不同的操作系统，按自己的需求，推荐选择CentOS 6 X64。

![VPS系统型号](https://jykmka.bn1304.livefilestore.com/y4mTSEoWA64hbCnLbidpCY0oj7wbktTqNk6u_qxnDyMZz8Oou_Q6Q7Jqev5gja8kqssPdFT_yFN-n38Aef5sfrUfbNbMvldZU8M1ubnV6E_JekROIlatYHlHJqHS3kp3Zv-kquWZXXj3nYdwPOppUUdzw5KQ_-pJ4xKPGaMl7V4lvh063QV9PSIOZXhFjFxnknF1auHfgmOonopMwRNyBnRbQ?width=818&height=538&cropmode=none)

5. 选择服务器大小，这就是关系到最终价格的地方了，本着节约的目的，我就为了学习和建个小站点自己玩，当然是最便宜的2.5美元/月。

![VPS容量设置](https://jymlgw.bn1304.livefilestore.com/y4mwi1wwhGDyicxWVDV438MwzapJwwmh4ShSg-OT3uCDnfAnG2M3jz76L_iK9vgdCWslD8scNHlfeaBb7ou_9b4AAKkIij4KGs-wJGvK68pP8dvc3yfXm9goZIhqIc7LETkvFEcH0NLR4iGsvHeUr34q87fbzVspFgYyJa5Z6oAPLaqd0gvMMjpaI4LJ4vLPzhY6NPlqGq_1UhQG7gP5cbR5A?width=905&height=451&cropmode=none)

6. 设置附加项，对我这样的初级玩家，不需要，略过。

![VPS附加项设置](https://jylvmg.bn1304.livefilestore.com/y4mwB4dphBp2_SwgqobHezxc2HHI2NYBpz1GO7FyJmoI-QKWUtlyNCzsBCns4FoC7ppg4eaLr_nYUrOTx51-CrByY4zVWAGoJ_ZZQ2YdurOVfu7Pzoo8gOclFkAKmXOJOBrAOdsltd59peVcfAO4zIArD2YLpjKmrZJ8yEt40sI3UTC1pU2o4Qa_6y_1ejjBEOP0bGru6-PPtLoMfa7KC_Nnw?width=571&height=524&cropmode=none)

7. 主机标签，按个人喜好，如果不是准备开很多个VPS，完全不用设置。

![VPS主机标签](https://jlrwxw.bn1304.livefilestore.com/y4mhG4aLlfFAFdvDboHlbacZOpTos2lNHWY9L3UpGsFaIXS9UPmxysb4BeyHhMRh3NAnMx20Av5_KCkFqslA-Y-EAAuELnCgBY9vtdUGIPfgp8xgNh_lFdPbLOl5ydQGyo9w1UCQxY6kQX4xwwEm_DlWjpnKebKNUmXiu2jk3vk0rHZu9xnruDI-QCFEIRtf7gz8vqKoipPb-Ax3H1wZtbApw?width=1171&height=397&cropmode=none)

8. 点击最后的Deploy Now，等待几分钟，当出现“Server added successfully”的时候，就说明你的VPS已经成功开通。

9. 最后一步，点击主机名，进入管理界面，可以查看主机的***IP地址和密码***。（请记住这两个参数，后续设置会用到）

## 在VPS服务器上部署ShadowsocksR

因为这个VPS你看不见，摸不着，你需要一个工具来远程连接它，然后对它进行一些设置。常用的工具有[Xshell 5](https://www.netsarang.com/products/xsh_overview.html), [Putty](http://www.putty.org/)等，Xshell 5 针对个人和学生用户有免费的许可证，注册申请就可以了，推荐。

使用Xshell连接VPS的方法过程，请参考[自建ss服务器教程](https://github.com/Alvin9999/new-pac/wiki/%E8%87%AA%E5%BB%BAss%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B)的第二部分"部署VPS服务器"。

登录VPS成功后，修改root密码，改为容易记、足够安全的新密码。代码为（本篇Blog中的每行代码前都有“\# ”，目的是为了防止代码长度比较长时，Blog可能自动开始新行，故同时出现多行代码时，以每个“\# ”表示为一行完整的代码，复制代码时请不要复制“\# ”）：

    # passwd

回车后就可以设置新的root密码，需要回车后再输入一次。修改好后会有成功的提示信息。（**注意：**如果设置新的密码，请去Xshell会话属性中的密码修改为新的密码）

部署SSR的代码：

    # wget --no-check-certificate  https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
    # chmod +x shadowsocksR.sh
    # ./shadowsocksR.sh 2>&1 | tee shadowsocksR.log

回车，等待安装完成。

完成后就会开始提示开始设置ShadowsocksR的密码和服务器端口，随后会提示你选择加密方式（推荐aes-256-cfb）、协议（推荐auth_aes128_md5）和混淆方式（推荐tls1.2_ticket_auth），都是以数字选择的方式输入回车确认即可。（*如果有输错的时候，请使用ctrl+Backspace组合键进行删除，而不是单一的Backspace键*）

设置完成后，按任意键开始安装ShadowsocksR, 完成后会给出你的配置信息，**请一定记好这些信息，推荐截图保存，客户端设置时需要使用到**。之后可以使用客户端连接测试是否可以连接。

基本的Shadowsocks部署就已经完成，如果还希望优化速度，可以搜索BBR优化或者锐速等优化方法。

## 域名注册

对于新手来说，不需要去花过多的钱在这上面，推荐域名注册商[namesilo](https://www.namesilo.com/?rid=c6de758mj)，优势很明显：价格很便宜、重要的是支持支付宝付款；而且还有免费赠送whois保护，免费赠送域名停靠服务。

注册流程我不此处重复了，可以去[王掌柜的网站](https://since1989.org/wordpress/namesilo-coupon-godaddy-domain-free.html)看整个流程，还可享受优惠码哦。

## 域名解析

有了自己的域名（网址），有了VPS的IP地址，怎么让这两个东西连接起来，可以输入自己的网址来访问自己的站点，这就需要域名解析来完成。所以我们还需要注册一家域名解析的公司让他们可以把我们的网址和IP连在一起，并且告诉全网络，这样所有人就可以通过网址访问我们之后建立起来的个人站点了。

同样为了偷懒，还是去[王掌柜的网站](https://since1989.org/namesilo/dnspod-name-servers-domain.html)看整个流程和设置方法，超级容易。

**域名解析是需要时间的，不能立刻就生效，所以请在部署自己站点之前把域名注册和域名解析完成好，不然会和我一样等几天没事做，不能配置WordPress。**

## LAMP环境部署

LAMP指的是个什么呢？它是Linux（操作系统）、Apache（HTTP服务器），MySQL（数据库软件） 和PHP（有时也是指Perl或Python）的第一个字母，主要用来建立web应用平台（通俗的讲就是来搭建网站的）。

新手嘛，LNMP一键安装包是个好东西，登陆VPS后，输入代码：

    # screen -S lnmp

回车，创建screen会话。输入代码下载LNMP稳定版（末尾的lamp不能忘，不然就会默认安装为LNMP）：

    # wget -c http://soft.vpser.net/lnmp/lnmp1.4.tar.gz && tar zxf lnmp1.4.tar.gz && cd lnmp1.4 && ./install.sh lamp

回车，进入搭建LAMP环境前的必要配置（没有特殊要求，一般选择默认项就可以）。

1. 选择数据库（**需要注意的是MySQL 5.6,5.7及MariaDB 10必须在1G以上内存的更高配置上才能选择！**），输入对应MySQL或MariaDB版本前面的序号，回车进入下一步：

![Database](https://jymsyg.bn1304.livefilestore.com/y4m4kFFCJWb91CuURCCuIrLE1lcDZVzBn-EY7SlUiNx11vaj6b2i0OJLYYxPAUSmKiDr-i4I_0xzSizWYcof67IIV6_TXbsahPa_6QUuMwREIxrIPKp9hY1H0P_ZBoCraeUde-BUsp2inzIVmkWljXnNOzW3NmbCFxuRlnXfzoqadX0zKLUK5J32pNQegfpPeczriBO3TDH5_kafElX8n00wg?width=347&height=170&cropmode=none)

2. 设置MySQL的root密码（不输入直接回车将会设置为root）如果输入有错误需要删除时，可以按住Ctrl+Backspace组合键进行删除(个别情况下是只需要Backspace键)。输入完成后回车进入下一步：

![MySQLpassword](https://wp381a.bn1304.livefilestore.com/y4mRj9Eunbo6NfOcdn84mGlSb-DeHtvG8DQZMbIi5WwLA2weFwW98IiBO92a0_XSYpR2eD1NJWmciHfnof1pHM-EFBvKG-Omca6W3U3KhYWA9h8CZFajf5xzIZoxYXbdAsLLmtJYYfCnv1S_h6ZbDJXhvNKyQ1TFGeNsLrzuLgPXAmzFpbLND6pyOdZJPgnVHCQIZ21cJlj0ubQqJCpBxo1hw?width=426&height=39&cropmode=none)

3. 选择是否启用MySQL InnoDB，InnoDB引擎默认为开启，一般建议开启，直接回车或输入 y ，回车进入下一步：

![InnDBEngine](https://jylceq.bn1304.livefilestore.com/y4m1j6q05NcczEkwpCj_WpayS2iNCN__HmJgcSb6FofVwpsDNgdq678fU9wDG1EHs_Uhgn8Wlfe2xyjXtyvcwAalislXGd52ZHZmCGBbE6ija1cusODPwYu23PA5tLNmUeehOKZynwpcbntRkTXXSUMsmxD3AUDaYljQLV6CoGybBZM8Lz_H7YmdQLSMJ1Jc3Fl-zZsZvNXyt0Hg3Jg5kKJCQ?width=423&height=42&cropmode=none)

4. 输入要选择的PHP版本的序号（*注意：选择PHP7等高版本时需要自行确认是否与自己的程序兼容。*），回车进入下一步：

![PHP](https://jyn37q.bn1304.livefilestore.com/y4mnlIbes9nWb-ojTUSgmpAveEa9zx18PkBonkeADfvrJB3zqXNG4dqQcd-AeGyOtQjD6mpnfowxwe8IhQyefqZzap8Uomjt2StUi1GR4qayZuLLqge4JURG-qI9NB1SwPT_OSOumYdkn1Xl5IPGFQuIMZIwl1-LbPVCYDCMyBKV4oki0FL7VSGYiKJ2a7iiVuwQ13aFjEGUkqmUCaXeODeiA?width=324&height=152&cropmode=none)

5. 选择是否安装内存优化，默认为不安装，回车进入下一步：

![MemoryAllocator](https://wp0yvg.bn1304.livefilestore.com/y4mucyUGETW0RpNI29Fm21MBH8y9yg3k2Eu8JaAtRuUfWV3fa7viqgO8l-XeQSwZsu5ocBWJYzdS3SKap-ig5DZLOKMG-9eWvajCvntzGKPqP6SHlr-Ncp6-SlmAA3IXO8ttLIZXreteH0CHVTFuDZBAFNnOgfLwKS7nZL2qdQBhomn5U2Vg0ro5Ig11rWNEB9feajnSgEduBxdfzgwJJCwbA?width=384&height=84&cropmode=none)

6. 提示设置管理员邮箱，该邮箱会在报错时显示在错误页面上：

![AdminEmail](https://jykyag.bn1304.livefilestore.com/y4m23tOf5-NfbT4EOOTHgGiZcNFklTMVykCPxqwMgmTfhDK3CDySL4DxWWZetfKFNGVcqKBHDgOdbwiuLK9Dt56fowxkweH9wJYiDAMHwqNAADzPrKlSyskD-zKxmGSMI3h7jR23GCOrILN-ZykCE2Wchrro_B8YvcTUkCBoy4QPcNkGNepnyNnO9ASIqngQwifKtrfTmiznjOVN0cY8YJcPQ?width=293&height=40&cropmode=none)

7. 选择Apache版本，输入对应版本前面的数字序号，回车。

![Apache](https://wp2xsq.bn1304.livefilestore.com/y4mlMLs-vJZQuPCDQjdd0SwRPOLbFCJPiFsiBow2A2xt6lnGGcW9A171i5XmIT7WdwGaDjnJJQ1rGNSxx3eo1a4HpRsRtETzc8p8-0yIHMKyHVKM-8vvVdwZH4iZQdQLnDyW7EuWE89n9gBComewC5REoIq34DpssbWPJrdFaYh-mCvhGMU9mDeVnaW3lafBE1TYwtPM3Je_HxDBdsCNVAzZA?width=308&height=73&cropmode=none)

8.提示“Press any key to install...or Press Ctrl+c to cancel”后，按回车键确认开始安装。LNMP脚本就会自动安装编译Nginx、MySQL、PHP、phpMyAdmin、Zend Optimizer这几个软件。

安装时间可能会几十分钟到几个小时不等，主要是机器的配置网速等原因会造成影响。如果显示Nginx: OK，MySQL: OK，PHP: OK，并且Nginx、MySQL、PHP都是running，80和3306端口都存在，并提示安装使用的时间及“Install lnmp V1.4 completed! enjoy it.”的话，说明已经安装成功。

![SuccessRunning](https://jyl9jq.bn1304.livefilestore.com/y4mSYlrI4asNQOcdIAxINafDiUzV_RlJcY2TVTup6SyxGwkh_yv8x03JaE1mQORJ0n4h1Vaiw-KaeESGhGkdkwWWZ5YQ2HY_QTeGWkczvZKFxynI9ElnQ3Icn_e4ifDYGK-W-1QzN4sT7k-nkK_ScsoKNJ3NCm7IA83VEk2bwPMz3yiKByIIIMZ_jdeCtOYets9X5m75W-PQJI8UGiAvtdhGg?width=534&height=644&cropmode=none)


## 添加虚拟主机

经过上面的操作，VPS上已经有了网站运行的基本环境LAMP，距离个人网站的成功又进了一步。现在要做的就是创建虚拟主机来给我们的网站当个容器。这个操作需要使用Xshell连接到VPS后，输入命令来完成，所以请仔细小心不要出错。（*万一出错了，请在按回车之前用Ctrl+Backspace组合键删除输入错误的部分*）

1. 成功连接VPS后，输入命令开始操作：
```
    # lnmp vhost add
```
2. 输入要添加网站的域名（*就是你在域名注册商注册好的那个网址*），以本站为例，输入：
```
    # www.workhub.life
```
3. 询问是否添加更多域名，直接再输入要绑定的域名，这里我们将workhub.life 也绑上，多个域名空格隔开，如不需要绑其他域名就直接回车。(注：**带www和不带www的是不同的域名，如需带www和不带的www的域名都访问同一个网站需要同时都绑定**)。

4. 设置网站的目录，不输入直接回车的话，采用默认目录：/home/wwwroot/域名

5. 然后设置允许Rewrite，伪静态可以使URL更加简洁也利于SEO，我们之后要使用的是WordPress，所以我们输入:
```
    # wordpress 
```
6. 设置日志，如启用日志输入y，不启用输入n，回车。

7. 询问是否用相同的名字添加数据库和数据库用户，输入y，回车。此时会先验证MySQL的root密码(注：输入密码将不显示，所以不要输入错误)，输入完成后回车。

8. 输入要创建的数据库名称，要创建的数据库用户名会和数据库同名，回车确认。
```
    # db_neworklife
```
9. 设置该数据库用户的密码，回车确认。

10. 如果安装了FTP服务器会询问是否添加FTP账号的相关信息

11. 接下来是LNMP1.4新增的添加SSL功能，如果需要添加输入y，不添加输入n回车。

12. 提示Press any key to start create virtul host...后，回车确认便会开始创建虚拟主机。添加成功会提示添加的域名、目录、伪静态、日志、数据库、FTP等相关信息

## 安装WordPress

此处介绍使用命令行的方式来安装WordPress中文版。

1. 首先还是通过Xshell与VPS连接上，输入命令进入刚刚建立的域名目录，回车确认：
```
    # cd /home/wwwroot/www.workhub.life
```
2. 输入代码下载WordPress的程序压缩包，回车确认：
```
    # wget https://cn.wordpress.org/wordpress-4.8.1-zh_CN.tar.gz
```
3. 下载完之后，命令解压压缩包，回车确认：
```
    # tar -zxvf wordpress-4.8.1-zh_CN.tar.gz
```
4. 将解压出来的wordpress文件夹内全部文件移动到当前的域名目录下，回车确认（最后的小句点不要漏掉）：
```
    # mv wordpress/* .
```
5. 然后删掉空文件夹wordpress，回车确认：
```
    # rm -rf wordpress
```
6. 赋予根目录文件的可写权限，避免因权限的问题导致安装出错（比如wp-config.php无法创建、需要提供FTP用户密码以及主题和插件不能更新等），回车确认：
```
    # chmod -R 755 /home/wwwroot
    # chown -R www /home/wwwroot
```
（*提示：以后每添加一个域名，都要执行一次以上两步操作。*）
7. LNMP安装包默认禁用了scandir函数，会导致WordPress后台看不到安装的主题，以及当前主题总显示 “有新的翻译可用” 的提醒。所以，需要开启此函数。

- 打开文件php.ini，回车确认：
```
    # vi /usr/local/php/etc/php.ini
```
- 查找scandir函数，回车确认：
```
    # ?scandir
```
- 按delete键删除，接下来需要保存并退出vi命令，回车确认：
```
    # :wq
```
- 重启一下LNMP，回车确认：
```
    # lnmp restart
```
8. 在你的域名正常解析后，在浏览器中输入网址打开博客进行最后的安装

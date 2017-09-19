# VPS搭建个人站点和ShadowsocksR记录

很久以前就想着可以自己做个小网站，写点自己的东西，并把自己学习的东西做个总结，但是一直找不到时间（其实就是懒）。

现在终于迈出第一步，参考了网络上各位大神们的教程，可以把基本的框架做好，等待慢慢的完善自己的站点。这篇文章就记录下我的VPS建站历程。

## 准备工作

***思想上的准备：***建立站点不需要什么高深的技术知识，我们早就进入互联网的时代，各种教程网上遍地都是，只要自己照着步骤走，就不会有任何问题。*（就算有问题也可以马上搜索找到解决方案）*

***物质准备：***一台可以顺畅浏览互联网的电脑，一张还有几百块人民币余额的银行卡。

### 购买VPS
VPS（Virtual Private Server），中文是虚拟专用服务器，简单的可以理解为一台远端的电脑，你可以使用特殊的工具进行访问设置。

现在VPS提供商有很多，可以按照自己的需求来选择不同的供应商。本人推荐[美国Vultr公司](https://www.vultr.com/?ref=7214452)，它提供有2.5美元/月的VPS，足够新手来操作练手，更为方便的是可以使用[支付宝](https://www.alipay.com/)直接进行人民币结算来充值帐户，不用烦心美元兑换的问题。

Vultr公司提供了日本和新加坡的机房已供选择，但是这两个地方的最低价格VPS经常满员，如果没有速度上的严格要求，选择美国的机房也可以完全满足个人站点的访问速度要求。

本人购买Vultr VPS的过程如下：

1. 打开[Vultr官网](https://www.vultr.com/?ref=7214452)，点击右上角的Create Account，输入邮箱和密码进行注册即可。如果要长期使用，推荐登陆后台完善个人的相关信息。（其主页上也有接下来步骤的操作动画，可以进行查看）

2. 登陆后台，选择最右边的Servers，再选择左边的蓝底加号（+），开始VPSvps选择。

!(VPS设置开始)[https://jynbba.bn1304.livefilestore.com/y4m2HFtRdfrd989g-rDY5BvjF0gkUfiCMsIgIXPyRl0KWR7MBjT7fsFRUJqEFQdD4IogvmSfzl04rCKR7Sx_3ObmfyVkuX7zLicJF2SvCCRD94xrU8wimI-bG0b4B44pm5pVwE8EQZ_WmeY1xQmozWJL-FgEyGLbAAM1SclH6Xrr9QNMyPQjj2MmtX-QooSzIi6LGaMU1kNPSh7uIvpJOhvHA?width=1338&height=186&cropmode=none]

3. 按照自己的需求选择机房的位置，我选择在Miami（哎，东京和新加坡的便宜VPS没有了）。

!(VPS机房位置)[https://jynwpg.bn1304.livefilestore.com/y4mQGKoxp7LgZPOxkYWxk5f12naPZN4GNL8AuZ0mFlN1-tK9SV5yjfZxvDWAD0MKGjGXv8yLoK6T_1ePCMmNoxvmVNFG11NHTFCkm38bgqJK42WxKTROKDiPc4GSfCZfH-Ecx2r9ISfLMwT5ChfuBY_B6MTUIAum-GCi_zjQuMfItkIAHCMgQW5PDWecgYOLKgFRogRmkc1KDETiBOt3YYiMg?width=832&height=494&cropmode=none]

4. 选择系统型号，其实就是选择不同的操作系统，按自己的需求，推荐选择CentOS 6 X64。

!(VPS系统型号)[https://jykmka.bn1304.livefilestore.com/y4mTSEoWA64hbCnLbidpCY0oj7wbktTqNk6u_qxnDyMZz8Oou_Q6Q7Jqev5gja8kqssPdFT_yFN-n38Aef5sfrUfbNbMvldZU8M1ubnV6E_JekROIlatYHlHJqHS3kp3Zv-kquWZXXj3nYdwPOppUUdzw5KQ_-pJ4xKPGaMl7V4lvh063QV9PSIOZXhFjFxnknF1auHfgmOonopMwRNyBnRbQ?width=818&height=538&cropmode=none]

5. 选择服务器大小，这就是关系到最终价格的地方了，本着节约的目的，我就为了学习和建个小站点自己玩，当然是最便宜的2.5美元/月。

!(VPS容量设置)[https://jymlgw.bn1304.livefilestore.com/y4mwi1wwhGDyicxWVDV438MwzapJwwmh4ShSg-OT3uCDnfAnG2M3jz76L_iK9vgdCWslD8scNHlfeaBb7ou_9b4AAKkIij4KGs-wJGvK68pP8dvc3yfXm9goZIhqIc7LETkvFEcH0NLR4iGsvHeUr34q87fbzVspFgYyJa5Z6oAPLaqd0gvMMjpaI4LJ4vLPzhY6NPlqGq_1UhQG7gP5cbR5A?width=905&height=451&cropmode=none]

6. 设置附加项，这对我这样的初级玩家，不需要，略过。

!(VPS附加项设置)[https://jylvmg.bn1304.livefilestore.com/y4mwB4dphBp2_SwgqobHezxc2HHI2NYBpz1GO7FyJmoI-QKWUtlyNCzsBCns4FoC7ppg4eaLr_nYUrOTx51-CrByY4zVWAGoJ_ZZQ2YdurOVfu7Pzoo8gOclFkAKmXOJOBrAOdsltd59peVcfAO4zIArD2YLpjKmrZJ8yEt40sI3UTC1pU2o4Qa_6y_1ejjBEOP0bGru6-PPtLoMfa7KC_Nnw?width=571&height=524&cropmode=none]

7. 主机标签，按个人喜好，如果不是准备开很多个VPS，完全不用设置。

!(VPS主机标签)[https://jlrwxw.bn1304.livefilestore.com/y4mhG4aLlfFAFdvDboHlbacZOpTos2lNHWY9L3UpGsFaIXS9UPmxysb4BeyHhMRh3NAnMx20Av5_KCkFqslA-Y-EAAuELnCgBY9vtdUGIPfgp8xgNh_lFdPbLOl5ydQGyo9w1UCQxY6kQX4xwwEm_DlWjpnKebKNUmXiu2jk3vk0rHZu9xnruDI-QCFEIRtf7gz8vqKoipPb-Ax3H1wZtbApw?width=1171&height=397&cropmode=none]

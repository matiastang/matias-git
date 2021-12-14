<!--
 * @Author: matiastang
 * @Date: 2021-12-13 17:28:38
 * @LastEditors: matiastang
 * @LastEditTime: 2021-12-13 19:40:51
 * @FilePath: /matias-git/md/ssh免密登录服务器.md
 * @Description: ssh免密登录服务器
-->
1. 打开本地iterm2（终端）输入ssh-keygen，一直回车（当然可以根据提示自定义密钥存储位置、密码），生成公私钥

默认生成位置为~/.ssh/.id_rsa为私钥 id_rsa.pub为公钥


2. 设置ssh连接配置 sudo vi ~/.ssh/config 编辑后:wq保存


#ssh模版
Host            hostname 

HostName        xxx.xxx.xxx.xxx      

Port            22

User            root # 用户名

ServerAliveInterval 60 # 每隔60秒 发送KeepAlive请求，保证不会因为超时空闲断开

IdentityFile    ~/.ssh/id_rsa #私钥地址
这时候可以通过ssh <hostname> 的方式访问，但需要填写服务器登陆密码

3. 这时就需要公钥的存在 将公钥拷贝至服务器端,下面方法选其一

* 直接拷贝
拷贝复制id_rsa.pub的内容
ssh <hostname>输入密码登入服务器
echo 拷贝内容 >> ~/.ssh/authorized_keys
* scp 文件远程传输
scp ~/.ssh/id_rsa.pub root@xxx.xxx.xxx.xxx:~/.ssh/temp
ssh <hostname>输入密码登入服务器
cat ~/.ssh/temp >> ~/.ssh/authorized_keys
4. 现在就可以ssh <hostname>直接登陆
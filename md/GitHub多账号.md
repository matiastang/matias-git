<!--
 * @Author: tangdaoyong
 * @Date: 2021-08-17 16:21:10
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-08-17 16:21:41
 * @Description: GitHub多账号
-->
# GitHub多账号

使用多个GitHub账号时
> $git push
报错：
```
remote: Permission to ******.git denied to ***.
fatal: unable to access 'https://github.com/******.git/': The requested URL returned error: 403
```
(Git 最著名报错 “ERROR: Permission to XXX.git denied to user”)[http://www.jianshu.com/p/12badb7e6c10]
GitHub中一个账号可以拥有多个公钥，所有重新生成公钥添加

1. 在.ssh文件下生成新的秘钥路径
> $mkdir 文件夹名称

2. 生成秘钥(指定需要保存秘钥的文件夹)
> $ssh-keygen -t rsa -C "邮箱" -f ~/.ssh/github/matias_github_key/id_rsa

> 连续3次回车，简单暴力，可知道为啥不？容我来解释一下，第一次回车对应的内容是 Enter file in which to save the key (/Users/yezhu/.ssh/id_rsa): id_rsa_name 需要填写文件名，如果不写的话就是默认名称为id_rsa，会把之前的生成已经存在的覆盖掉，所以我们可以在这里写的是id_rsa_name(自定义名称);第二次和第三次都是声明是否需要为文件设置密码，默认即为不设置，所以这里连续2次回车。

3. 添加公钥到GitHub
4. 添加配置

* 打开`~/.ssh/config`,如果没有就创建一个config文件($ git touch  config命令创建，或者如下命令也可以)
> $vim ~/.ssh/config

* 写入新的host配置(格式如下)
```
#配置个人帐号邮箱(******@163.com)
#IdentityFile路径一定要对，指向.ssh 文件夹(可以自定义秘钥保存的位置)中的id_rsa私钥(可以自定义秘钥命名)
Host matias_github
HostName github.com
User git
IdentityFile ~/.ssh/github/matias_github_key/id_rsa
```

* 查看(确认修改)
> $cat config

5. 将GitHub SSH仓库地址中的git@github.com替换成新建的Host别名

* 关于替换的规则
原来的项目的ssh地址为：
> $ git@github.com:***/Demo.git
那么替换后的地址为：
> $ matias_github:***/BestoneGitHub.git
或者：
> $ git@matias_github:***/Demo.git

* 步骤

1. 项目根目录下，查看链接的仓库地址
>$git remote -v

2. 查看默认配置
>$vim .git/config

修改host(可以使用$ ssh -T matias_github命令看看是否修改成功:Hi matiastang! You've successfully authenticated, but GitHub does not provide shell access.)
>$git remote  set-url origin matias_github:matiastang/CSS3.git

查看配置是否修改成功
>$vim .git/config

查看链接的仓库地址
>$git remote -v

然后再次进行提交项目等操作，应该就可以了。

6. 如果还不行，进行下一步操作：把你的密钥加入sshAgent代理中：

* 启动ssh-agent环境，先执行命令(出现 Agent pid * 意味着开启成功)：
>$eval "$(ssh-agent -s)" # start the ssh-agent in the background

然后添加密钥 id_rsa (.ssh/github/matias_github_key)：
>$ssh-add ~/.ssh/github/matias_github_key/id_rsa

第一次使用直接添加即可使用
然后添加默认密钥 id_rsa(.ssh)：
>$ssh-add ~/.ssh/id_rsa

[Linux命令：ssh-agent](https://man.linuxde.net/ssh-agent)
[Linux命令：ssh-add](https://man.linuxde.net/ssh-add)

7. 测试
这样就应该ok了。可以使用$ ssh -T git@github.com来看一下密钥isa是否连接成功github或者$ ssh -T git@matias_github测试密钥id_rsa (.ssh/github/matias_github_key)是否连接成功github

如果是第一次需要确认一次，(输入yes回车即可)
```
matias@192 git-svn % ssh -T matias_github
The authenticity of host 'github.com (13.250.177.223)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com,13.250.177.223' (RSA) to the list of known hosts.
Hi matiastang! You've successfully authenticated, but GitHub does not provide shell access.
matias@192 git-svn % 
```
我的测试：
```
~/.ssh/github/matias_github_key » ssh -T matias_github
Hi matiastang! You've successfully authenticated, but GitHub does not provide shell access.
----------------------------------------------------------------------------------------
~/.ssh/github/matias_github_key » ssh -T git@github.com
Hi tangdaoyong! You've successfully authenticated, but GitHub does not provide shell access.
----------------------------------------------------------------------------------------
~/.ssh/github/matias_github_key » ssh -T git@matias_github
Hi matiastang! You've successfully authenticated, but GitHub does not provide shell access.
```

补充：ssh-agent 会开启一个进程运行在后台，相当于一个服务。其机制是每隔几十秒向用 SSH 连接的服务器发送数据，由此服务器就不会自动断开跟你的 SSH 连接了。“还在吗 ~ ”。 也因此有时候电脑重启之后需要重新启动ssh-agent令之运行在后台，Windows用户经常要手动启动。

第一次提交建议使用命令行，需要输入github账号信息
```
Username for 'https://github.com': 自己的github账号名称
Password for 'https://matiastang@github.com': github账号密码
```
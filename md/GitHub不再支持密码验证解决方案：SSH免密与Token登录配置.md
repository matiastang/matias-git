<!--
 * @Author: tangdaoyong
 * @Date: 2021-08-17 16:45:42
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-08-17 17:04:18
 * @Description: GitHub不再支持密码验证解决方案：SSH免密与Token登录配置
-->

[token使用官方介绍](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)
[GitHub不再支持密码验证解决方案：SSH免密与Token登录配置](https://cloud.tencent.com/developer/article/1861466)
[忽然发现GitHub用不了了，原来git的账密验证已经弃用，改用 token 或 SSH 密钥](https://xiaoqiang666.blog.csdn.net/article/details/119712839)
[解决git@github.com: Permission denied (publickey). Could not read from remote repository.](https://www.jianshu.com/p/7d57ce4147d3)

配置好`公钥`之后，记住，你项目得使用 `SSH clone`.如果本地是https 源，那么就修改git 仓库地址

git修改远程仓库地址
方法有三种：

1.修改命令
git remote origin set-url [url]
先删后加
git remote rm origin
git remote add origin [url]
直接修改config文件
git文件夹，找到config，编辑，把就的项目地址替换成新的。
顺手安利下 [《git宝典—应付日常工作使用足够的指北手册》](https://www.zhoulujun.cn/html/tools/VCS/git/402.html)

## 使用token
原来输入密码的时候，输入生成的token就可以了
$ git clone https://github.com/username/repo.git

Username: your_username
Password: your_token
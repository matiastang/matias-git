<!--
 * @Author: your name
 * @Date: 2021-09-17 17:55:00
 * @LastEditTime: 2021-09-17 17:59:42
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: /matias-git/md/git使用.md
-->
# git使用

git pull命令用于从另一个存储库或本地分支获取并集成(整合)。git pull命令的作用是：取回远程主机某个分支的更新，再与本地的指定分支合并，它的完整格式稍稍有点复杂。

如果当前分支只有一个追踪分支，连远程主机名都可以省略。

$ git pull
上面命令表示，当前分支自动与唯一一个追踪分支进行合并。

当出现上面的情况时，我们可以有两种解决方法

对于这种情况有两种解决办法，就比如说要操作master吧，一种是直接指定远程master：
```
git pull origin master
```

另外一种方法就是先指定本地master到远程的master，然后再去pull：
```
git branch --set-upstream-to=origin/master master
git pull
```
这样就不会再出现“There is no tracking information for the current branch”这样的提示了。

`git pull`提示`fatal: refusing to merge unrelated histories解决`
强制拉取
```
git pull origin master --allow-unrelated-histories
```
可以允许不相关历史提，强制合并，确实解决了这个问题，感谢网友

查看当前关联的远程地址：git remote -v
添加远程链接地址：git remote add origin ssh://git@git.51keti.cn:2222/dw-sdk-front/dw-request.git

修改远程链接地址：git remote set-url origin ssh://git@git.51keti.cn:2222/dw-sdk-front/dw-request.git
<!--
 * @Author: tangdaoyong
 * @Date: 2021-08-17 16:17:43
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-08-17 16:18:05
 * @Description: githubusercontent.com
-->
# githubusercontent.com

[raw.githubusercontent.com](https://raw.githubusercontent.com/) 是 github 的素材服务器 (assets server), 避免跟主服务抢占负载。

如果访问地址[raw.githubusercontent.com](https://raw.githubusercontent.com/) 不能成功（比如GitHub中的MarkDown的图片未显示成功）。查看是否添加了`raw.githubusercontent.com`到`hosts`。

如果没有就如下添加：

通过 [IPAddress.com](https://www.ipaddress.com/) 首页，输入raw.githubusercontent.com 查询到真实IP地址。 修改 /etc/hosts，Ubuntu，CentOS 及 macOS 直接在终端输入
```
$ sudo vi /etc/hosts
```
如果是第一次需要输入开机密码 添加以下内容保存即可
```
199.232.68.133  raw.githubusercontent.com
```
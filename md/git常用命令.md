<!--
 * @Author: tangdaoyong
 * @Date: 2021-01-18 18:00:47
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-01-18 18:05:28
 * @Description: git常用命令
-->
# git常用命令

## 常用命令

### 回滚到制定位置
```
git reset --hard origin/dev
git reset --hard 9bef251c740d5433d063b0dba9ab0ebddf39719b
```

### 查看提交日志
```
git log
```

### 强推本地分支代码（覆盖远程分支代码）
```
git push origin 分支名 --force
git push origin dev-tangdaoyong --force
```

### 删除远程已没有的，已废弃的分支
```
git fetch -p
```
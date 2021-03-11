### git的学习

> 修改邮箱和用户名

```bash
git config --global user.name "You Name"
git config --global user.email 2031360580@qq.com
```
> 基本的命令
添加到缓存区，从缓存区加到marster，查看状态
```bash
git add [[.][文件]]
git commit -m "提交的描述"
git status
```
> 查看更改文件的差异

提交之后就不能更改了

```bash
git diff fileName
```

> 历史记录的查看，和版本的回退

如果要回到过去的版本，首先要看到历史的记录
```bash
git log
```
如果要到将来的版本，就是先从未来到过去然后版本回退
```bash
git reflog
```
如果要实现版本的回退,就要先知道每个版本的版本号，然后根据版本号回退
```bash
git reset --hard 版本号
git reset --head HEAD[[^][~n]]//HEAD 是指向当前的版本 HEAD^^ 表示上上个版本
```
> 工作区和版本库在还没有提交之前的回退
```bash
git restore [文件]... // 丢弃工作区的改动
git checkout -- [fileName]
git restore --staged [文件]... //取消暂存
git reset HEAD [fileName]
```
> 版本库的概念

<image src="https://static.liaoxuefeng.com/files/attachments/919020037470528/0">

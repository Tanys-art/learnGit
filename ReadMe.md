### git的学习

> 修改邮箱和用户名

```bash
$ git config --global user.name "You Name"
$ git config --global user.email 2031360580@qq.com
```
> 基本的命令
添加到缓存区，从缓存区加到marster，查看状态
```bash
$ git add [[.][文件]]
$ git commit -m "提交的描述"
$ git status
```
> 查看更改文件的差异

提交之后就不能更改了

```bash
$ git diff fileName
```

> 历史记录的查看，和版本的回退

如果要回到过去的版本，首先要看到历史的记录
```bash
$ git log
```
如果要到将来的版本，就是先从未来到过去然后版本回退
```bash
$ git reflog
```
如果要实现版本的回退,就要先知道每个版本的版本号，然后根据版本号回退
```bash
$ git reset --hard 版本号
$ git reset --head HEAD[[^][~n]]//HEAD 是指向当前的版本 HEAD^^ 表示上上个版本
```
> 工作区和版本库在还没有提交之前的回退
```bash
$ git restore [文件]... // 丢弃工作区的改动
$ git checkout -- [fileName]
$ git restore --staged [文件]... //取消暂存
$ git reset HEAD [fileName]
```
> 版本库的概念

<image src="https://static.liaoxuefeng.com/files/attachments/919020037470528/0">

> 远程仓库

远程仓库克隆出来有两种协议，https 和 ssh 协议，ssh要通过生成公钥然后在git上配置公钥，克隆不要使用```sudo```命令
```bash
$ git remote add origin git@github.com:Tanys-art/learngit.git //origin 建立关联
$ git push -u origin master //推送到远程仓库 参数 -u可以简化之后推送的命令
$ git push origin master
// 远程仓库克隆出来可通过两种协议
$ git clone git@github.com:Tanys-art/gitskills.git // 或者使用https协议
```

> 删除远程仓库的概念

```bash
$ git remote -v //查看远程仓库的信息
$ git remote rm origin
```
+ 此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。

> 分支的管理

我们的提交是从分支出发的
```bash
$ git branch // 查看分支
$ git branch [分支的名字] // 建立分支
$ git checkout [分支的名字] //切换分支
```
> 分支的合并

使用下面的命令合并分支

```bash
$ git merge [分支的名字] // 使用这条命令将命令给定的分支合并到当前的分支
```

> 删除分支

在合并之后将不用的分支删除

```bash
$ git branch -d [分支的名字] 
```

> switch 命令

使用switch 命令来代替branch的一些功能

```bash
创建+切换分支：git checkout -b <name>或者git switch -c <name>
$ git switch -c [分支的名字] //创建并切换分支
$ git switch [分支的名字] //切换分支
```
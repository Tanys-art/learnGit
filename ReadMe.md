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

> 分支的冲突问题

查看简化日志之后的命令和合并分支命令

```bash
$ git log --graph --pretty=oneline --abbrev-commit
$ git log --graph // 分支合并图
$ git merge [分支的名字]
```

> 分支管理策略

在多人开发中，一般不会在主分支上做操作，会建立一个dev分支，然后在分支dev上操作，然后最后合并起来如下图

<image src = "https://static.liaoxuefeng.com/files/attachments/919023260793600/0"></image>

在多人开发中也不会使用fist forword ,常用的命令如下

```bash
$ git merge --no-ff -m "merge with no-ff" dev // 正常的合并方式
```

> bug 的修复

场景：当我们在dev分支上的时候做了一些修改，然后发现main 分支上面还有bug,然后我的dev也还没有提交的时候，这个时候dev也还没完成不能提交，这个时候要保留dev的现场，然后，建立一个修复bug的分支，然后修复bug后再，把修改的现场再提交上去

```bash
$ git stash //保留现场
$ git checkout main //切换到bug分支
$ git checkout -b issue-101 //建立修复bug的分支并切换
$ git add [fileName]
$ git commit -m "" //提交
$ git switch [分支名字] 
$ git merge --no-ff -m "描述" [分支名字] // 合并之后发现之前做的修改消失
$ git switch dev // 之前做的修改消失
$ git stash list //查看之前保留的现存
$ git stash apply + git stash pop == git stash pop // 用一个命令就可以
$ git cherry-pick 4c805e2 // 这个命令是用来复制修改的
```
> feature 分支

我们在开发过程中，如果开发一个新的功能的话就需要我们创建一个新的分支来开发，然后如果在开发过程中这个功能要丢弃，然后要删除这个分支，这个时候就要强行删除

```bash
git branch -D feature // -d 是删除一个已经合并的分支，-D是删除一个还没合并的分支，也叫强行删除
```

> 多人协作

多人协作模式

```bash


    首先，可以试图用git push origin <branch-name>推送自己的修改；

    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

    如果合并有冲突，则解决冲突，并在本地提交；

    没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
```

总结：本地创建的分支和远程的最好一致

```bash
git checkout -b branch-name origin/branch-name //这样做可以同步分支的名字
```

技巧：我们一般在开发过程中会使用dev 分支进行合作，最后合并之后拉取请求，最后合并到main 分支

> rebase

让历史提交更加的直观

```bash
git rebase
```
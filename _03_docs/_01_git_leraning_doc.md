# git使用文档

## 创建用户名及邮箱

```git
git config --global user.name "User Name"
git config --global user.email "email address"
```

## 进入相应目录初始化仓库

```git
git init
```

## 把文件添加到版本库中

```git
git add filename //将文件或者文件夹添加到暂存区
git commit [-m "注释信息"] 将暂存区中的内容存放到仓库中，可选的-m为提交提示信息
```

## 查看状态

```git
git status
```

## 查看提交历史记录

```git
git log [--pretty=oneline] //可选项表示单行显示日志
```

## 版本回退

```git
git reset --hard HEAD^ //回退1个版本

git reset --hard HEAD^^ //回退2个版本


git reset --hard HEAD~100 //回退100个版本
```

## 回退之后在回退到新版本

```git
git reflog //查看所有版本号


git reset --hard 版本号 //回退到指定版本
```

## Git撤销修改文件操作

```git
git checkout -- file_name 
//撤销对工作区中file_name文件的修改，暂存区有新版本就恢复到暂存区版本状态，
//否则恢复到仓库版本状态
```

## Git删除文件操作

```git
git rm file_name //删除指定文件,即使我们使用系统文件管理器删除了也需要执行这一步
```

## 比较不同文件版本之间的差异diff

```git
git diff
```

`git diff`结果解析详见：[Git-git diff命令结果解析-CSDN博客](https://blog.csdn.net/CSDN___LYY/article/details/102555882 "Git-git diff命令结果解析-CSDN博客")

## 分支操作

```git
git branch //列出本地所有分支
git branch -v //列出远程所有分支
git branch -a //列出所有本地分支和远程分支，用不同颜色区分
git branch [branch_name] //新建一个分支branch_name
git branch -d [branch_name] //删除一个分支branch_name，-D（大写）强制删除
git branch [branch] [commit] //新建一个分支，指向指定commit id

git branch --track [branch] [remote-branch]
//    新建一个分支，与指定的远程分支建立关联

git branch --set-upstream [branch] [remote-branch]
//在现有分支与指定的远程分支之间建立跟踪关联

git branch --set-upstream-to=[remote-branch]
//在当前分支与指定的远程分支之间建立跟踪关联

git checkout [branch_name] //切换到指定分支branch_name，并更新工作区
git switch [branch_name] //切换到指定分支branch_name
git checkout -b [dev] //从当前分支创建并切换到dev分支
git switch -c [branch_name] //创建并切换到指定分支branch_name

git checkout -b feature1 dev 
//从本地dev分支代码创建一个feature1分支，并切换到新分支


git checkout -b hotfix remote hotfix
//从远端remote的hotfix分支创建本地hotfix分支


git checkout . //撤销工作区的（未暂存）修改，把暂存区恢复到工作区。

git checkout HEAD . //撤销工作区、暂存区的修改，用HEAD指向的当前分支最新版本替换


git merge [branch] //合并指定分支到当前分支


git rebase master //将当前分支变基合并到master分支
```

> **注意：**
> 
> - *如果修改（包括未暂存、已暂存）和待切换的分支没有冲突，则切换成果，且未提交修改会一起带过去，所以要注意！*
> 
> - *如果有冲突，则会报错，提示先提交或隐藏，关于隐藏可查看后续章节内容“stash”。*

## 

## 远程仓库操作

### 远程用户登录：SSH

- **生成公私钥**

```bash
ssh-keygen -t rsa //生成公私钥，默认在C:\Users\用户名\.ssh目录
```

- **配置公钥**
  
  > 1. 打开`id_rsa.pub`文件，复制内容。Github上，打开`Setting`➤ `SSH and GPG keys` ➤ `SSH keys` ➤ 按钮`New SSH key`，标题（Title）随意，秘钥内容粘贴进去即可
  > 
  > 2. SSH配置完后，可用`ssh -T git@github.com`来检测是否连接成功。

### 远程仓库指令

```git
git clone repo_addr //克隆远程仓库到本地


git remote -v //查看所有远程仓库，不带参数-v只显示名称


git remote show [remote] //显示某个远程仓库的信息


git remote add [name] [url] //增加一个新的远程仓库，并命名

git remote rename [old] [new] //修改远程仓库名称

git pull [remote] [branch]    //取回远程仓库的变化，并与本地版本合并

git pull    //同上，针对当前分支

git fetch [remote]    //获取远程仓库的所有变动到本地仓库，不会自动合并！需要手动合并

git push <远程主机名> <本地分支名>:<远程分支名>
//将<本地分支名>的代码推送到<远程主机名>中的<远程分支名>上


//如果本地分支名和远程分支名一样的情况下，可以省略:<远程分支名>。
//如果远程主机中不存在该分支，那么会被创建。
git push origin dev //即git push origin dev:dev

//如果本地分支已经跟远程分支建立了追踪关系，那么可以省略<本地分支名>和:<远程分支名>
//如果本地master和origin/master已经建立了关联
git push origin //相当于git push origin master:master

//我们只需要保证本地仓库只跟一台远程主机有关联，同时<本地分支名>已经和<远程分支名>关联
//可以省略远程主机名
git push //相当于将当前所在本地分支内容推送到唯一远程主机和当前分支关联的远程分支上

git push --set-upstream origin feature
//将本地feature分支推送到origin远程仓库feature分支上，同时本地分支和远程分支建立关联
//如果远程分支没有feature分支，则会新建一个
```

## 处理冲突<<<<<<< HEAD

> - 在有冲突的文件中，`<<<<<<< HEAD`开头的内容就表示是有冲突的部分，需要人工处理。
> 
> - `=======`分割线上方是当前分支的内容，下方是被合并分支的变更内容。
> 
> - 冲突处理完成后将冲突文件重新`add`和`commit`即可完成冲突处理

## 后悔指令

| 命令                          | 描述                                                        |
| --------------------------- | --------------------------------------------------------- |
| `git checkout .`            | 撤销工作区的（未暂存）修改，把暂存区的修改还原到工作区。不会影响暂存区，如果需要清空，删除所有文件后再执行这个命令 |
| `git checkout [file]`       | 同上，file指定文件名                                              |
| `git checkout HEAD .`       | 撤销工作区、暂存区的修改，用HEAD中指向的提交历史来替换掉工作区、暂存区                     |
| `git checkout HEAD [file]`  | 同上，file指定文件名                                              |
| `git reset`                 | 把缓冲区恢复到最近一次commit, 不影响工作区                                 |
| `git reset HEAD [file]`     | 同上, file指定文件名, HEAD可省略                                    |
| `git reset [commit]`        | 回退到指定版本, 丢弃之后版本, 不影响工作区。工作目录里面对应checkout出来                |
| `git reset --soft [commit]` | 保持分支master, HEAD到制定版本处。不影 响暂存区、工作目录。需要对checkout出来         |
| `git reset --hard HEAD^`    | 撤销本次提交, 且不保留修改内容。回退到前一 版本，并且重置了工作、缓冲和内容                   |
| `git reset --hard HEAD~n`   | 回退到指定版本，并且重置了缓冲和内容                                        |
| `git revert[commit]`        | 取消某个提交，在当前一个新的提交（撤销某次 提交）生成一个新的提交记录，如果已经Push则 需要再push回去   |



### reset的三种模式

| 提交代码类型     | 描述                                     | HEAD的位置 | 暂存区 | 工作区 |
|:----------:|:--------------------------------------:|:-------:|:---:|:---:|
| soft       | 回退到某一个版本, 工作区不变, 需手动git checkout 修改    | 修改      | 不丢失 | 不丢失 |
| mixed (默认) | 保留修改但不会标记为已暂存, 不影响工作区, 需手动git checkout | 修改      | 修改  | 不丢失 |
| hard       | 重置本地修改（工作区、暂存 区）                       | 修改      | 修改  | 修改  |



### revert用法

>  安全的撤销某一个提交记录，基本原理就是生产一个新的提交，用原提交的逆向操作来完成撤销操作。注意，这不同于`reset`，`reset`是回退版本，revert只是用于撤销某一次历史提交，操作是比较安全的。

```git
git revert 41ea42 -m '撤销对***的修改'//revert commit_id，-m 附加说明
```



## stash隐藏未提交内容

| 命令                       | 描述                                |
| ------------------------ | --------------------------------- |
| git stash                | 把未提交内容隐藏起来，包括未暂存、已暂存。等以后恢复现场后继续工作 |
| git stash list           | 查看所有被储藏的内容列表                      |
| git stash pop            | 恢复最近的被储藏的内容，并删除该储藏记录              |
| git stash save "message" | 同git stash，可以给该次储藏加message        |
| git stash apply          | 恢复最近的被储藏的文件，但是不删除隐藏记录             |
| git stash drop           | 删除隐藏的记录                           |

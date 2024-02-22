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

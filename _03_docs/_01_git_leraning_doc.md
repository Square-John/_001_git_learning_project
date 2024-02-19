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
git checkout --file_name 
//撤销对工作区中file_name文件的修改，暂存区有新版本就恢复到暂存区版本状态，
//否则恢复到仓库版本状态

```



## Git删除文件操作

```git
//工作区中如果删除了某个文件，可以通过commit保证新版本仓库中也同样删除该文件
//在没有
```



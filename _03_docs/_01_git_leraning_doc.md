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
git log [–pretty=oneline] //可选项表示单行显示日志
```

# GIT 使用

## 1、安装GIT

[zhao_Note/wiki/git 笔记.md at master · zhaodahan/zhao_Note](https://github.com/zhaodahan/zhao_Note/blob/master/wiki/git 笔记.md)

## 2、本地配置

安装完`Git`应该做的第一件事就是设置你的用户名称与邮件地址。 这样做很重要，因为每一个`Git`的提交都会使用这些信息，并且它会写入到你的每一次提交中，不可更改：

```python
C:\Users\fancy>git config --global user.name "francis"

C:\Users\fancy>git config --global user.email fancylan@gmail.com
```

![image-20250713135032179](D:\Note\Wiki\resource\image-20250713135032179.png)

再次强调，使用了 `--global` 选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事情， Git 都会使用那些信息。 当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有 `--global` 选项的命令来配置。

## 创建版本库

现在windows本地创建目标目录D:\Note\Wiki，作为后期所有项目的本地空间，然后在该目录下创建一个子目录，用于存储Typora的所有图片资源。位于format目录下image，完成设置后，你每次插入到Typora的图片都会自动保存到该目录。

<img src="D:\Note\Wiki\resource\image-20250713141515294.png" alt="image-20250713141515294" style="zoom:80%;" />

完成后，在git命令行下进入对应目录，并执行如下命令初始化版本库。

```
$ cd d:/note/wiki
fancy@ECBUPJKT MINGW64 /d/note/wiki
$ git init
Initialized empty Git repository in D:/Note/Wiki/.git/

```

命令执行后，会提示你，仓库建好了，并且告诉你是一个空的仓库（empty Git repository），可以发现当前目录下多了一个`.git`的目录(建议隐藏的)，这个目录是`Git`来跟踪管理版本库的，不要手动修改这个目录里面的文件，否则就把Git仓库给破坏了。

## 添加文件到版本库

`git`仓库搭建好了，现在就来添加文件到版本库里面。 创建一个`md`文档起名叫做`git使用.md`，往里面添加一点内容`hello git`. 注意，最好不要用系统自带的`txt`来编写，因为这里需要文件是`UTF-8`格式的，所以我使用`Typora`这种可以把文件另存为`UTF-8`格式的编辑器的。 创建好文件后，添加到仓库只需要2个操作： 第一步，用命令`git add`告诉`Git`，把本地代码托送到暂存区

```python
git add git使用.md
```


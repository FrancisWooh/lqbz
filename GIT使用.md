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

第二步，用命令`git commit`告诉`Git`，把文件提交到仓库

```
$ git commit -m "first commit"
[master (root-commit) dc0e2a2] first commit
 1 file changed, 46 insertions(+)
 create mode 100644 "GIT\344\275\277\347\224\250.md"

fancy@ECBUPJKT MINGW64 /d/note/wiki (master)
$

```

`-m` 参数是用来注释你提交的信息的，这样以后才知道这次提交时用来干嘛

或者你嫌弃文件太多，一次次add感觉很麻烦，那么可以试试使用`git add .`提交，`.`表示提交当前目录所有文件

```
git add . 
或者
git add *
```

## 查看当前新增或者修改的文件

实际使用中你不止只有一个文件，或新增或修改多个文件，可能时间一久就忘了有多少文件需要提交 这里模拟一下，首先新建一个`hello.txt`的文件，然后修改`readme.txt`内容，添加一句`come on baby`. 这样就有2个文件需要提交了。 我们使用`git status`命令来查看当前状态,是否有未提交的文件

```
git status
```

![image-20250713142854210](D:\Note\Wiki\resource\image-20250713142854210.png)

如图，可以看到红色的字体显示的一个`GIT***.md`被修改过了，但还没有准备提交的修改，另外一个是`Untracked files: hello.txt`和resource目录，表示新增的文件。

这时候准备把上面2个文件都提交，使用命令：

```
D:\Note\Wiki>git add .

D:\Note\Wiki>git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   "GIT\344\275\277\347\224\250.md"
        new file:   hello.txt.txt
        new file:   resource/image-20250713135032179.png
        new file:   resource/image-20250713141515294.png
        new file:   resource/image-20250713142854210.png


D:\Note\Wiki>
D:\Note\Wiki>git commit -m "second commit"
[master 40aa02e] second commit
 5 files changed, 41 insertions(+)
 create mode 100644 hello.txt.txt
 create mode 100644 resource/image-20250713135032179.png
 create mode 100644 resource/image-20250713141515294.png
 create mode 100644 resource/image-20250713142854210.png
```

## 比较当前文件跟版本文件内容

假如你已经记不清上次怎么修改的`GIT使用.md`，所以，需要用`git diff`这个命令看看：

```
git diff GIT使用.md
```

会显示变化的部分，按q退出比较

## 查看历史提交记录

有时候你想看看之前提交的历史纪录~那么就需要使用到`git log`命令：

```
D:\Note\Wiki>git log
commit 40aa02e747edf5195d35ed737304a38fb81ebd99 (HEAD -> master)
Author: francis <fancylan@gmail.com>
Date:   Sun Jul 13 14:31:34 2025 +0800

    second commit

commit dc0e2a27b4f71df1bc9aba2ed2e11aecd52b4143
Author: francis <fancylan@gmail.com>
Date:   Sun Jul 13 14:25:21 2025 +0800

    first commit

D:\Note\Wiki>
```

可以看到有两次提交，以及对应的提交者和提交日期，按照日期从新到旧排列。

# 理解git暂存区

暂存区，在`git`中是个很重要的概念，弄懂了暂存区才算真正懂了`git`

## 什么是暂存区



------

工作区： 我们正在编辑的区域

暂存区： 执行了add 操作后的区域

版本库 ：执行了commit之后的 (这里还要有区别，这个版本库，包含了本地版本库的和远程版本库的内容，push 后就是同步本地与远程的版本库)

------

下图展示了工作区、版本库中的暂存区和版本库之间的关系。 [![img](https://camo.githubusercontent.com/be9c1b452a9c3e6e1ada9cb0c694fb693dc6f4ae3774196451977c5c4681f0f4/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d376530656435363433623761613864312e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-7e0ed5643b7aa8d1.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240) 图中可以看到 `Git`命令是如何影响工作区和暂存区`（stage, index）`的。

- 图中左侧为工作区，右侧为版本库。在**版本库中标记为 `index` 的区域是暂存区**`（stage, index）`，标记为 `master` 的是 `master` 分支所代表的目录树。
- 图中我们可以看出此时`HEAD`实际是指向`master`分支的一个“游标”。所以图示的命令中出现`HEAD`的地方可以用`master`来替换。
- 图中的`objects`标识的区域为`Git`的对象库，实际位于`.git/objects`目录下。
- 当对工作区修改（或新增）的文件执行`git add`命令时，暂存区index的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的`ID` 被记录在暂存区的文件索引中。
- 当执行提交操作`（git commit）`时，暂存区的目录树写到版本库（对象库）中，`master`分支会做相应的更新。即`master`指向的目录树就是提交时暂存区的目录树。
- 当执行 `git reset HEAD` 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。
- 当执行 `git checkout .` 或者 `git checkout -- [file]` 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区的改动。
- 当执行 `git checkout HEAD .` 或者 `git checkout HEAD [file]` 命令时，会用 `HEAD` 指向的 `master` 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。
- 当执行 `git rm --cached [file]`命令时，会直接从暂存区删除文件，工作区则不做出改变。
- 当执行 `git rm file`命令时，会同时删除暂存区和工作区的文件。
- 当执行 `rm file`命令时，只会删除工作区的文件。

------

## 举例子来证明以上观点



------

假设： 工作区：a 暂存区（index）:b HEAD:C

git diff命令结论

```git
git diff           比较a跟b
git diff --cached  比较b跟c
git diff HEAD      比较a跟c
```



git reset跟 git checkout结论

```
git reset HEAD              c覆盖b
git checkout -- <file>      b覆盖a
git checkout HEAD <file>    c覆盖a,b
```



git rm命令结论

```
git rm          删除a跟b
git rm --cached 只删除b
rm file         只删除a
```



## 证明git diff结论



------

例子，默认新建一个`readme.txt`，里面输入内容`one`然后add并且`commit`一次。

1：修改`readme.txt`，新增内容`two`，这时候a内容改变了,多了`two`，而b跟c内容不变，都只有`one`。 执行`git diff readme.txt`查看效果

[![img](https://camo.githubusercontent.com/5d136fa8459cb9b4b12e6700819d429debfbf4910608b63549392d1492a2475e/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d663263356235386464396638343938342e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-f2c5b58dd9f84984.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

结论：如图看出，内容有修改， a跟b比较了

------

执行`git diff --cached readme.txt`查看效果

[![img](https://camo.githubusercontent.com/059cc364ac8a9cc9c9df42f2951838e88000e622c0de42a190c0e195ecf94e07/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d653830633337653938336336643736372e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-e80c37e983c6d767.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

结论：如图看出，没有变化，因为b跟c内容一样。

------

执行`git diff HEAD readme.txt`查看效果

[![img](https://camo.githubusercontent.com/b1aead514ffa2119cb57fbe365856a19bd1c6e1cff4be3923e14b47ef034ce02/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d663761323035656436353434393238642e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-f7a205ed6544928d.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

如图所示：内容有修改，a跟c比较了

------

2.这时候执行`git add readme.txt`,这时候a，b内容都多了two，而c内容不变，只有`one` 执行`git diff readme.txt`查看效果

[![img](https://camo.githubusercontent.com/8ae632f7df14fc4093beed11010c2bfcb90e4e48caf2569e222bc230dd80e78b/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d633134356266306434373030323866312e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-c145bf0d470028f1.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

结论：如图看出，没有变化， 因为a跟b内容一样。

------

执行git diff –cached readme.txt查看效果

[![img](https://camo.githubusercontent.com/a513fe59a77d4cd3721f98643423ba598d8d54e42dca74d91fba3ddc6c0932e3/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d383638363937323437646337333337372e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-868697247dc73377.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

结论：如图看出，内容有修改，b跟c比较了

------

执行`git diff HEAD readme.txt`查看效果

[![img](https://camo.githubusercontent.com/607f9ee4ed3082365b20bca3f2abeaebbe4b48948d4c632245cec76ee772bebb/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d336566346234633638616335396663332e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-3ef4b4c68ac59fc3.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

结论：如图看出，内容有修改，a跟c比较了

3.最后使用`git commit`提交一次，这时候a,b,c内容都一样，都包含`two`。

[![img](https://camo.githubusercontent.com/7038487816cd6d19ff7f05bb10db5889efe3102e25c71ede435d824d56a903c5/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d636232323762653330353662623432302e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-cb227be3056bb420.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

结论，如图看出，没有变化，说明a,b,c内容一样

------

根据上面的实例再一次证明了如下观点：

```
git diff           比较工作区跟暂存区
git diff --cached  比较暂存区跟HEAD
git diff HEAD      比较工作区跟HEAD
```



## 证明git reset跟 git checkout结论



------

例子，默认新建一个`readme.txt`，里面输入内容`one`然后add并且`commit`一次，这时候a,b,c内容都是`one`

------

1.修改`readme.txt`，新增内容`two`，执行`git add readme.txt`操作，这时候a ,b内容都多了`two`,c还是只有`one`. 执行`git reset HEAD -- readme.txt`命令后，c覆盖b,这时候b内容也变成只有`one`了，使用`git diff readme.txt`命令可以看到，有内容修改，a跟b内容不一样。

[![img](https://camo.githubusercontent.com/03b96ae35de2b26ca68eae82809a69566f21f9d3bc77774d75574e439ece3fb2/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d656633356132376535316431616137392e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-ef35a27e51d1aa79.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

------

2.此时a内容有two,b和c都只有one，执行`git checkout -- readme.txt`后，b覆盖a,此时a,b,c都是one。执行`git diff readme.txt`命令可以看到，没有改变。

[![img](https://camo.githubusercontent.com/3f9278e1eb4350d901ab89fe57d30fb4553dca7c0e354d4e94a634a353484644/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d383162326366303963623038363463642e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-81b2cf09cb0864cd.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

------

3.此时a,b,c都只有`one`，修改一下，添加内容`two`，执行`git add readme.txt`和`git commit -m "two"`.再修改一次`readme.txt`,添加内容`three`,然后会执行`git add readme.txt`，此时a跟b都包含three，而c只包含one跟two。执行`git checkout HEAD readme.txt`后，c覆盖a和b,a,b里面内容都只有one跟two。分别使用命令`git diff --cached`和`git diff HEAD`来查看b跟c，a跟c的比对，发现都一样。

[![img](https://camo.githubusercontent.com/3e884f1099abb66a9a54c072767a066cdd4c83628beb84f289758f46e380cf0a/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d666633313332613234396637356134642e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-ff3132a249f75a4d.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

------

根据上面的实例再一次证明了如下观点：

```
git reset HEAD              HEAD覆盖暂存区
git checkout -- <file>      暂存区覆盖工作区
git checkout HEAD <file>    HEAD覆盖暂存区和工作区
```



------

## 证明git rm 结论



------

默认新建一个`readme.txt`，里面输入内容`one`，然后使用`git add readme.txt`命令。 1.执行git rm readme.txt命令，发现文件被删除了。

2.再新建一个一个`readme.txt`，里面输入内容 one，然后使用`git add readme.txt`命令。执行`git rm --cached readme.txt`命令，发现文件内`readme.txt`还在，然后执行`git status`命令，发现是`Untracked`状态，也就是未`add`，这就说明暂存区被删除了。

[![img](https://camo.githubusercontent.com/d748cc62180fc680de62f4c65bca713bd955af00a7d63ce7e45669bf4ffa9627/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d633930353834373833623235616330652e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-c90584783b25ac0e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

------

根据上面的实例再一次证明了如下观点：

```
git rm file      会将文件从缓存区和你的硬盘中（工作区）删除
git rm --cached  只删除暂存区，不删除工作区
rm file          只删除工作区
```



# 提交错了我想撤销或者回退版本



这几个功能正式体现版本控制工具的强大之处。(十分好用)

## 撤销操作



如果你文件**只是在工作区修改**了，但是还没提交到暂存区的时候,回滚就是从暂存区覆盖到工作区

```
git checkout -- [file]  b覆盖a
```



你可以用`git checkout -- [file]`来撤销。简单的说就是暂存区覆盖工作区。这里模拟一下，比如现在`readme.txt`里面内容是`first day`，并且已经提交到暂存区了，此时修改`readme.txt`，内容改成`second day.`，然后执行`git checkout -- readme.txt`命令,你会发现`readme.txt`内容又变成`first day`了 [![ img](https://camo.githubusercontent.com/9b7a28a0cd25931a0f297062a4cf5f83c832179fa8e628d740ee028cb8d0e045/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d393731396434303166373965616161662e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-9719d401f79eaaaf.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

如果你文件**在工作区修改了 ,并且也执行`git add`命令提交给暂存区**了，那么执行上面的`git checkout -- [file]`已经无效了，因为两者内容一致。 这时候就需要版本库的内存覆盖缓存区

```
git reset HEAD  c覆盖b
```



这时候就应该使用`git reset HEAD`命令来撤销，简单的说就是让`HEAD`覆盖暂存区，因为此时的`HEAD`这边的文件内容还是上次提交时的内容。现在模拟一下，现在有`readme.txt`跟`hello.txt`两个文件，都经过修改 [![img](https://camo.githubusercontent.com/c47ee2a88819d81d31f1fc6375fe08a840e3444a9fad5d0dd395c33aa73a2de7/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d396236363035373963633665323738652e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-9b660579cc6e278e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240) 如图可以看到，使用`git status -s`来查看的时候，红色的M表示这2个文件都经过修改，使用`git add .`提交后在查看，发现都是绿色的M，表示都提交到暂存区了，这时候执行`git reset HEAD hello.txt`后再查看，发现`hello.txt`变成红色M了，说明hello.txt从暂存区撤销了。

```
git checkout HEAD [file]
```



`git checkout HEAD [file]`命令是`git checkout -- [file]`和`git reset HEAD`的合成体，直接用HEAD覆盖工作区,暂存区。如下图中所示，一开始 工作区暂存区以及HEAD中文件内容都是`first day.`,此时修改`readme.txt`内容为`second day.`，然后执行`git add .`提交到暂存区，接着执行`git checkout HEAD readme.txt`命令，再查看`readme.txt`内容的时候你会发现变成了`first day.` [![img](https://camo.githubusercontent.com/f0bbca36c02dfd17704df34c037d8544110cf97c595ee999c2a97bddef91b262/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d646634346438616238386532643638392e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-df44d8ab88e2d689.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

## 版本回退以及切换



```
git reset --hard HEAD^  （这个命令用于C覆盖b比较好用） 这个命令使用来移动 HEAD 指针的
```



首先，`Git`必须知道当前版本是哪个版本，在`Git`中，用`HEAD`表示当前版本，也就是最新的提交`3628164...882e1e0`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。 先查看当前版本记录 `git log --oneline`，发现最近的两个版本为`b520a36 第一次提交`和`479c6fd 第二次提交` [![img](https://camo.githubusercontent.com/c5904cfb0bec75559dcaa36a28711680de8e6e6a1def21cc4edae31c7cb1d551/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d633630323461346564396265333264392e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-c6024a4ed9be32d9.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

当前版本是`b520a36 第一次提交`,现在我们来执行`git reset --hard HEAD^`来回退到`479c6fd 第二次提交`版本,如图： [![img](https://camo.githubusercontent.com/3f2dabe0cbbafebeb74c868f0668297cbc95641c9e81ffee05a3250d2198ec6c/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d613431393830663139613536373861622e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-a41980f19a5678ab.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

```
git reset --hard commit_id
```



如果你回退版本后又后悔了，想恢复最后那个版本怎么办，通过`git reset --hard commit_id`命令可以搞定，注意这里的`commit_id`是版本号，只要记得版本号，你想切换到哪个版本都行，如果你忘记了刚才最后一个的版本号，可以通过`git reflog`来查看，这里我们记得最后那次版本号为`b520a36`，执行`git reset --hard b520a36` [![img](https://camo.githubusercontent.com/9bbf9c09983dd046b3ee88e31dddf5cfd6397d382293c135bf1cbab6eb360ec5/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d656366643538623166376632313061622e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-ecfd58b1f7f210ab.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

## 删除操作



------

这里介绍一下`git`中的删除操作命令，以及意外删除了该如何还原。

```
git rm
```



执行`git rm`命令会同时删除工作区跟暂存区中的指定文件，要慎重处理。

但是如果你意外删除了也是可以恢复的。不过要分成2种情况处理：

1. 还未执行`git commit`提交到`HEAD`的时候删除文件，这时候直接使用`git checkout HEAD [file]`就能还原。 [![img](https://camo.githubusercontent.com/9d1048ed9eb74c733ff831ea748cb184b50353e84490ada10303e45cae45f847/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d303439343865656364663662323432612e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-04948eecdf6b242a.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)
2. 执行`git commit`提交到`HAED`后时候才删除文件，这时候就只能执行`git reset --hard HEAD^`回退上一个版本。 [![img](https://camo.githubusercontent.com/6676cb6706f3b6f1321a5d1d8950dafbf4e8cbca93f192aef64f2ec853421cf6/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f313633373932352d333839353464316562363862383239302e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f31323430)](http://upload-images.jianshu.io/upload_images/1637925-38954d1eb68b8290.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

------

### 删除错误提交的commit



 有时，不仅添加到了暂存区，而且commit到了版本库，这个时候就不能使用git rm了，需要使用git reset命令。

 **错误提交到了版本库，此时无论工作区、暂存区，还是版本库，这三者的内容都是一样的**，所以在这种情况下，只是删除了工作区和暂存区的文件，下一次用该版本库回滚那个误添加的文件还会重新生成。

 这个时候，我们必须撤销版本库的修改才能解决问题！

 git reset有三个选项，--hard、--mixed、--soft。

```
//仅仅只是撤销已提交的版本库，不会修改暂存区和工作区
git reset --soft 版本库ID
```



```
//仅仅只是撤销已提交的版本库和暂存区，不会修改工作区
git reset --mixed 版本库ID
```



```
//彻底将工作区、暂存区和版本库记录恢复到指定的版本库
git reset --hard 版本库ID
```



 那我们到底应该用哪个选项好呢？

 （1）如果你是在提交了后，对工作区的代码做了修改，并且想保留这些修改，那么可以使用git reset --mixed 版本库ID，注意这个版本库ID应该不是你刚刚提交的版本库ID，而是**刚刚提交版本库的上一个版本库**。如下图：

 （2）如果不想保留这些修改，可以直接使用彻底的恢复命令，git reset --hard 版本库ID。

 （3）为什么不使用--soft呢，因为它只是恢复了版本库，**暂存区仍然存在你错误提交的文件索引**，还需要进一步使用上一节的删除错误添加到暂存区的文件，详细见上文。

[![img](https://camo.githubusercontent.com/fb5dfe9dc0402cff597c8591dd297d5748a0c630a267ff652d34cefd558aadd7/68747470733a2f2f696d61676573323031352e636e626c6f67732e636f6d2f626c6f672f3639353733312f3230313531302f3639353733312d32303135313031373136343230353237322d313830383130313333372e706e67)](https://camo.githubusercontent.com/fb5dfe9dc0402cff597c8591dd297d5748a0c630a267ff652d34cefd558aadd7/68747470733a2f2f696d61676573323031352e636e626c6f67732e636f6d2f626c6f672f3639353733312f3230313531302f3639353733312d32303135313031373136343230353237322d313830383130313333372e706e67)

------

## 结束



------

总结一下上面所学的：

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，使用`git reset --hard HEAD^`。

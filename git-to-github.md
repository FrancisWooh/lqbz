# Connect Local Git DB with Remote Repository

Git尝试连接远程仓库了，目前国内外比较出名的提供`Git`仓库远程托管的有国外的`github`，国内的`开源中国`以及`coding`。这里以`github`为例子介绍如何操作远程仓库。

# Github创建Repository

![image-20250713152421686](D:\Note\Wiki\resource\image-20250713152421686.png)

进入自己的github账号，查看对应的https克隆地址。然后在本地库内部执行git remote add命令，给远程repository创建一个别名。然后就可以使用git push remote_repository_name  local_branch_name  来推送本地的repository了。

```python
D:\Note\Wiki>git remote add origin https://github.com/FrancisWooh/lqbz.git

D:\Note\Wiki>git push origin master
info: please complete authentication in your browser...
Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 24 threads
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 87.06 KiB | 14.51 MiB/s, done.
Total 14 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), done.
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/FrancisWooh/lqbz/pull/new/master
remote:
To https://github.com/FrancisWooh/lqbz.git
 * [new branch]      master -> master

D:\Note\Wiki>cd ..
```

后续，如果需要添加或者改变文件，使用git在本地添加和提交就可以同步到github了。

同样的，如果想要把别人的库拉到本地，可以使用同样的命令方式。

先创建一个新的目录结构，并git init来创建一个新库。

```
D:\Note>mkdir zhao_Note

D:\Note>cd zhao_Note

D:\Note\zhao_Note>git init
Initialized empty Git repository in D:/Note/zhao_Note/.git/

D:\Note\zhao_Note>git remote add zhao_note https://github.com/zhaodahan/zhao_Note.git

D:\Note\zhao_Note>git pull zhao_note master
remote: Enumerating objects: 1976, done.
remote: Counting objects: 100% (86/86), done.
remote: Compressing objects: 100% (76/76), done.
remote: Total 1976 (delta 17), reused 30 (delta 10), pack-reused 1890 (from 1)
Receiving objects: 100% (1976/1976), 315.07 MiB | 9.50 MiB/s, done.
Resolving deltas: 100% (24/24), done.
From https://github.com/zhaodahan/zhao_Note
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> zhao_note/master
Updating files: 100% (1909/1909), done.

D:\Note\zhao_Note>
```


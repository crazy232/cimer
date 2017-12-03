### git 命令使用

#### git status

```shell
# git status 用于查看当前还未被提交的修改,以及当前一些状态
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
	new file:   LICENSE
```

####  git reset

```shell
# git reset 用于版本库的版本回退
# git reset --hard commit_id
# 回退上个版本就是HEAD^  上上个版本就是HEAD^^  再往上就是HEAD~100
$ git reset --hard HEAD^
HEAD is now at 7b35a95 change Readme.md
# 也可以根据版本id 来回退,甚至回到未来版本
$ git reset --hard edee974
HEAD is now at edee974 add i do to README.md
```

#### git log 

```shell
# git log 用于查看最近到最远的提交日志
$ git log
commit edee974c90d8bdf1f3621c128b4170f124060b1b
Author: crazychl <1047824797@qq.com>
Date:   Sun Dec 3 20:22:13 2017 +0800

    add i do to README.md

commit 7b35a9574c955f72874947e21fd6bcc0e2def72a
Author: crazychl <1047824797@qq.com>
Date:   Sun Dec 3 20:18:07 2017 +0800

    change Readme.md

commit 90ef13dbc4d70ea9181d89cccf4a9869593829f0
Author: crazychl <1047824797@qq.com>
Date:   Sun Dec 3 20:11:04 2017 +0800

    add Readme.md
# 也可加上--pretty=oneline参数，便于直观显示
$ git log --pretty=oneline
edee974c90d8bdf1f3621c128b4170f124060b1b add i do to README.md
7b35a9574c955f72874947e21fd6bcc0e2def72a change Readme.md
90ef13dbc4d70ea9181d89cccf4a9869593829f0 add Readme.md


```

#### git reflog 

```
# git reflog用于记录你的每一次命令
$ git reflog
edee974 HEAD@{0}: reset: moving to edee974
7b35a95 HEAD@{1}: reset: moving to HEAD^
edee974 HEAD@{2}: commit: add i do to README.md
7b35a95 HEAD@{3}: commit: change Readme.md
90ef13d HEAD@{4}: commit (initial): add Readme.md

```

#### git checkout -- file

```shell
# git checkout -- file 用于撤销工作区所有修改，两种情况：
# 第一种是git add 后没有git commit,撤销的效果就和版本回退一样
# 第二种是git add后执行了git commit,撤销回到git add 前的状态
#切记不可省略 -- 否则就变成切换分支命令
# "commit"单词虽然git add,但是没有执行git commit ,所以回退后就没有此次修改
# "i will be back 被提交后，checkout后就被擦除" 
$ git commit -m "i will commit LICENSE"
[master de0b9e7] i will commit LICENSE
 1 file changed, 1 insertion(+)
$ cat LICENSE 
license saved 
return
commit
$ echo  "i will be back" >> LICENSE 
$ git checkout -- LICENSE
$ cat LICENSE 
license saved 
return

```

#### git rm

```shell
# 当想删除某个文件时就需要使用git rm,然后在git commit 
$ git rm LICENSE 
rm 'LICENSE'
$ git commit -m "delete LICENSE"
[master f87dd55] delete LICENSE
 1 file changed, 2 deletions(-)
 delete mode 100644 LICENSE
$ ls
README.md

#当然如果是误删，还可以使用 git reset
```

#### git branch

```shell
# git branch 查看当前分支
$ git branch
* dev
  master
 
 # git branch dev   创建dev分支
 # git branch -d dev  删除dev分支
```

#### git checkout 

```
# 切换当前分支
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

#加上 -b参数为新建并切换分支
$ git checkout -b dev
Switched to a new branch 'dev'

```

#### git merge

```
# git merge 用于合并两个分支，合并的方式有几种，例如下面的Fast-forward就是一种
# 例如下，在dev分支创建branch.sh文件并git commit后，切换到master分支没有branch.sh
# 通过git merge dev即可将dev分支创建的文件合并到master上
$ ls
LICENSE  README.md
$ git merge dev
Updating de0b9e7..78b0fa3
Fast-forward
 branch.sh | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 branch.sh
$ ls
branch.sh  LICENSE  README.md

```

#### git merge冲突解决

```
# git merge合并分支是也可能出现冲突，可通过git status查看冲突文件 如下提示：
$ git merge fea
Auto-merging branch.sh
CONFLICT (content): Merge conflict in branch.sh
Automatic merge failed; fix conflicts and then commit the result.
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   branch.sh

no changes added to commit (use "git add" and/or "git commit -a")

# 找到冲突文件后，多文件进行修改，再次git add 和git commit
# 可以通过 git log 查看分支合并情况
$ git log --graph --pretty=oneline --abbrev-commit
*   4b771e8 fix conflict
|\  
| * 43d0f7e AND simple
* | 6e42b0c & simple
|/  
* 78b0fa3 add branch.sh
* de0b9e7 i will commit LICENSE
* d4ed930 add file LICENSE
* edee974 add i do to README.md
* 7b35a95 change Readme.md
* 90ef13d add Readme.md

```


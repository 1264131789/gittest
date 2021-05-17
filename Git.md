#### Git笔记

#### 1.Git简介

##### 1、三种状态

已修改，表示修改了文件，但还没保存到数据库中。

已暂存，表示对已修改文件的当前版本做了标记，使之包含在了下次提交的快照中。

已提交，表示数据已经安全的保存在了本地数据库中。

##### 2.Git项目的三个阶段

工作区，暂存区以及Git目录（本地仓库）。

<img src="C:\Users\shbj\Desktop\笔记\git\areas.png" style="zoom: 80%;" />

工作区，是对项目某个版本独立提取出来的内容。

暂存区，是一个文件，保存了下次将要提交的文件列表信息，一般在Git目录仓库中。

Git仓库目录，是Git用来保存项目的元数据和对象数据库的地方。这是Git最重要的部分，从其他计算机克隆仓库时复制的就是这里的数据。

##### 3、基本的Git工作流程

1.在工作区中修改文件

2.将你想要下次提交的更改选择性地暂存，这样只会将更改的部分添加到暂存区。

3.提交更新，找到暂存区的文件，将快照永久性的存储到Git目录。

如果自上次检出后，做了修改但还没有放到暂存区，就是**已修改**状态；如果文件已修改并放入暂存区，就属于**已暂存**状态；如果Git目录中保存着特定版本的文件，就属于**已提交**状态

##### 4.Git配置

1、查看所有配置以及他们所在的位置

git config --list --show-origin

2、用户信息

git config --global user.name  “John Doe”

git config --global user.email “Johndoe@example.com”

3、检查配置信息

git config --list

git config user.name

4、查看那个配置文件最后设置了配置信息

git confit --show-origin user.name

=> file:C:/Users/shbj/.gitconfig   shbj

##### 5.获取帮助

1、git help \<verb>

git help config

2、git \<verb> -h ，用-h获得更简明的help输出。

git add -h

#### 2.Git基础

##### 1、获取Git仓库

1.将尚未进行版本控制的本地目录转换为Git仓库

git init

2.从其他服务器克隆一个已存在的Git仓库

git clone https://github.com/libgit2/libgit2

git clone https://github.com/libgit2/libgit2 mylibgit

##### 2、记录每次更新到仓库

工作目录下的每一个文件都不外乎两种状态：已跟踪或未跟踪。已跟踪的文件是指那些被纳入版本控制的文件。

编辑过某些文件之后，由于自从上次提交后对他们进行了修改，Git将他们标记为已修改文件。在工作时可以有选择性地将这些已修改过的文件放入暂存区，然后提交所有以暂存的修改，如此反复。

<img src="C:\Users\shbj\Desktop\笔记\git\fileStatus.png" style="zoom:80%;" />

1、检查当前文件状态

git status

2、跟踪新文件

git add

```
git add README
```

##### 3、暂存已修改的文件

git add 

这是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。 将这个命令理解为“精确地将内容添加到下一次提交中”而不是“将一个文件添加到项目中”要更加合适。

##### 4、状态简览

git status -s

##### 5、查看已暂存与未暂存的修改

git diff ：比对的是工作目录中当前文件和暂存区快照之间的差异。

git diff --staged（--cached） ：比对已暂存文件与最后一次提交的文件的差异。

##### 6、提交更新

git commit //会打开文本编辑器

git commit -m 

提交时记录的是放在暂存区域的快照。 任何还未暂存文件的仍然保持已修改状态，可以在下次提交时纳入版本管理。 每一次运行提交操作，都是对你项目作一次快照，以后可以回到这个状态，或者进行比较。

##### 7、跳过使用暂存区域

git commit -a

```
git commit -a -m "添加新内容"
```

虽然省略了add步骤，但是依然会将已跟踪的文件放到暂存区。

##### 8、移除文件

要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。

1.从工作区手动删除已暂存的文件后，可以执行

git rm 

把暂存区的记录也删除了。

2.如果要删除之前修改过或已经放到暂存区的文件，则必须使用强制删除选项 -f。也就是暂存了还没提交。

git rm -f

3.我们想把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录
中。

git rm --cached README

##### 9、移动文件

git mv file_from file_to

##### 10、查看提交历史

git log

-p 显示每次提交所引入的差异

git log -p -2 //-2表示只显示最近两次的提交

想看到每次提交的简略统计信息，可以使用 --stat 选项

git log --stat

##### 11、撤销操作

有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 --amend 选
项的提交命令来重新提交：

git commit --amend

##### 12、取消暂存的文件

git reset HEAD \<file>... 来取消暂存

git restore --staged \<file>...

##### 13、撤销对文件的修改

如何方便地撤消修改——将它还原成上次提交时的样子（或者刚克隆完的样子，或者刚把它放入工作目录时的样子）。工作区内未暂存的文件

```
git checkout -- CONTRIBUTING.md
```

如果是已暂存的文件可以先取消暂存，再撤销修改

```
git restore --staged CONTRIBUTING.md

git checkout -- CONTRIBUTING.md
```

##### 14、远程仓库的使用

###### 1.查看远程仓库

git remote：列出你指定的每一个远程服务器的简写

git remote -v：会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL

###### 2.添加远程仓库

git remote add \<shortname> \<url> 

```
git remote add cv https://github.com/1264131789/CustomView.git
```

###### 3.从远程仓库抓取与拉取

git fetch \<remote>

这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支
的引用，可以随时合并或查看。

如果你的当前分支设置了跟踪远程分支， 那么可以用 git pull 命令来自动抓取后合并该远程分支到当前分支。 git
pull 通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支。

###### 4.推送到远程仓库

当你想分享你的项目时，必须将其推送到上游。 这个命令很简单：git push \<remote> \<branch>。

将 master 分支推送到 origin 服务器

```
git push origin master
```

只有当你有所克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。 当你和其他人在同一时
间克隆，他们先推送到上游然后你再推送到上游，你的推送就会毫无疑问地被拒绝。 你必须先抓取他们的工作
并将其合并进你的工作后才能推送。

###### 5.查看某个远程仓库

git remote show \<remote>

```
git remote show cv
```

###### 6.远程仓库重命名与移除

git remote rename 

```
git remote rename cv rCv
```

git remote remove 

```
git remote remove rCv
```

##### 15、打标签

###### 1.列出标签

git tag

git tag -l “v1.8.5*”

###### 2.创建标签

Git支持两种标签轻量标签和附注标签

轻量标签很像一个不会改变的分支——它只是某个特定提交的引用。
而附注标签是存储在 Git 数据库中的一个完整对象， 它们是可以被校验的。

附注标签

```
git tag -a v1.1 -m "version 1.1"
```

轻量标签

```
git tag v1.1-lw
```

###### 3.后期打标签

要在那个提交上打标签，你需要在命令的末尾指定提交的校验和（或部分校验和）

```
git log --pretty=oneline//列出提交历史

1e1316852a2731da7ba7ecee29c448afb176c074 创建file_from
e91ac4d18da79c7e6958700221c12733f7049836 删除本地仓库中test3.txt
```

```
 git tag -a v1.0 1e131 -m "my version 1.0"
```

###### 4.共享标签

默认情况下，git push 命令并不会传送标签到远程仓库服务器上。 在创建完标签后你必须显式地推送标签到
共享服务器上。

git push origin \<tagname>

想要一次推送很多标签

git push origin --gats

git push 推送两种标签
使用 git push \<remote> --tags 推送标签并不会区分轻量标签和附注标签， 没有简单的选项能够让你只选择推送一种标签。

###### 5.删除标签

git tag -d \<tagname>

更新远程标签

第一种变体是 git push \<remote> :refs/tags/\<tagname> 

第二种 git push origin --delete \<tagname>

###### 6.检出标签

如果你想查看某个标签所指向的文件版本，可以使用 git checkout 

```
git checkout v2.0.0
```

##### 16、Git别名

git config --global alias.co checkout

git config --global alias.ci commit

当要输入 git commit 时，只需要输入 git ci

#### 3.Git分支

##### 1、分支简介

 暂存操作会为每一个文件计算校验和（SHA-1 哈希算法），然后会把当前版本的文件快照保存到Git 仓库中 （Git 使用 blob 对象来保存它们），最终将校验和加入到暂存区域等待提交。当使用 git commit 进行提交操作时，Git 会先计算每一个子目录（本例中只有项目根目录）的校验和， 然后在 Git 仓库中这些校验和保存为树对象。随后，Git 便会创建一个提交对象， 它除了包含上面提到的那些信息外，还包含指向这个树对象（项目根目录）的指针。 如此一来，Git 就可以在需要的时候重现此次保存的快照。

<img src="C:\Users\shbj\Desktop\笔记\git\git提交对象.png" alt="image-20210517183003976" style="zoom: 50%;" />

##### 2、分支创建

```
git branch testing
```

HEAD指针，指向当前所在的本地分支（译注：将 HEAD 想象为当前分支的别名）

git log 命令查看各个分支当前所指的对象。 提供这一功能的参数是 --decorate

```
$ git log --oneline --decorate
bc9ab1f (HEAD -> master, testing) git 基础
d47ccf5 Git别名
```

##### 3、分支切换

git checkout 命令

```
git checkout testing
修改文件内容，提交，再切回master分支
git checkout master
```

一是使 HEAD 指回 master 分支，二是将工作目录恢复成 master 分支所指向的快照内容。 也就是说，你现在做修改的话，项目将始于一个较旧的版本。 本质上来讲，这就是忽略 testing 分支所做的修改，以便于向另一个方向进行开发。

分支切换会改变你工作目录中的文件

git log --oneline --decorate --graph --all ，它会输出你的提交历史、各个分支的指向以及项目的分支分叉情况

创建新分支的同时切换过去

通常我们会在创建一个新分支后立即切换过去，这可以用 git checkout -b \<newbranchname> 一条命令搞定。

##### 4、分支的新建与合并

只有提交后，切换分支，工作目录才会切换回来。

```
git checkout -b hotfix
git checkout master
git merge iss53
git branch -d hotfix
git add *
git commit -m "add test2.txt"//提交后，当再切回iss53分支，工作目录才会还原
git checkout iss53
```

##### 5、分支的合并

```
git checkout master
git merge iss53
```


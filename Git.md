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

#### 2.Git配置

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
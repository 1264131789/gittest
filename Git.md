##### 1、Git工作区、暂存区和版本库（本地仓库）、远程仓库

##### 2.Git基本命令

1. git init： 创建仓库

2. git clone [url] :拷贝一个git远程仓库到本地

   git clone https://github.com/1264131789/CustomView.git

   git clone https://github.com/1264131789/CustomView.git MyCustomView，重命名项目名

3. git add [dir] [file2] ...：添加一个或多个文件（目录）到暂存区

   git add git.md

4. git status：查看当前仓库的状态，显示有变更的文件

   git status -s ：获取简短的输出结果

5. git diff：比较文件的不同，即工作区和暂存区的差异

   git diff [file]：显示暂存区与工作区的差别

   git diff -cached [file] 或git -diff -staged [file]：显示暂存区与上一次提交（commit）的差异

   git diff [first-branch]...[second-branch]：显示两次提交间的差异

   git status显示的是改动了那些文件，而git diff是详细显示出来改动的内容

6. git commit：提交暂存区到本地仓库

7. git commit -m [message]：提交暂存区到仓库

   git commit [file1] [file2]... -m [messsage]：提交指定文件或目录到本地仓库

   git commit -a：-a参数修改后的文件不需要执行git add命令，直接提交

8. 设置提交时的用户信息

   git config --gloab user.name ‘shbj’

   git config --gloab user.email ‘test@qq.com’

9. 

   






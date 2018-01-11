## git安装及配置
* 进入[git官网](https://git-scm.com/)，下载安装
* 基础命令：   
  版本查看：git --version  
  配置信息：git config user.name xxx --global
           git config user.email xxx@xxx.xxx -g   
  文档查看：git config --help 或者 git help config  
  查看状态：git status  
> gitignore 把不需要跟踪的文件添加到这个文件中就可以避免跟踪了。在这个文件中可以使用通配符。有些时候文件夹里没有这个文件，你可以自己手动建一个.gitignore文件
* git配置的三个等级      
  1.system  –针对于系统  
  2.global –针对于当前用户  
  3.local  –针对于当前仓库  
  配置的优先级：local>global>system
* git 仓库命令  
  - git init xxx (初始化一个xxx文件仓库，里面生成.git)  
  - git init xxx --bare (生成一个裸的仓库，它不带.git文件，也就是不带工作区)  
  - git clone url路径 （根据url地址，克隆一个已有的仓库）
* git仓库的三个区域
  1.working directory：工作区 -> git add xxx 提交到暂存区  
  2.staging area：暂存区      -> git commit -m "备注信息" 提交到分支
  3.local repository：历史仓库  ->git push  提交到远程分支
## git 分支
* 分支创建：git branch xx //新建xx分支
* 查看分支：git branch //当前分支前面会加“*”号标记    
           git branch -r //查看远程分支
           git branch -a //all 查看所有分支（本地分支和远程分支）
* 删除分支：git branch -d xxx
* 删除远程分支：git branch -d -r xxx
* 切换分支：git checkout xxx  //切换到xxx分支上
* 合并分支：git merge xxx  //把xxx分支合并到当前分支上。
* 还原暂存区: git reset xx //git add xx 提交后，通过此命令可以还原暂存区  
* 还原工作区：    
          命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：  
          一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；   
          一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。  
          总之，就是让这个文件回到最近一次git commit或git add时的状态。
          **git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令**
## git 远程分支操作
* git clone https://github.com/xxx.git // 克隆远端仓库到本地
* git fetch：获取远端仓库的所有内容，包括所有分支内容
```
  Git fetch origin master
  git log -p master..origin/master
  git merge origin/master
```
  *首先从远程的origin的master主分支下载最新的版本到origin/master分支上，然后比较本地的master分支和origin/master分支的差别，最后进行合并。*
```
  git fetch origin master:tmp
  git diff tmp
  git merge tmp
```
*从远端获取最新的版本到本地的tmp分支上，之后进行比较合并*
* git pull (相当于git fetch 和 git merge的操作合并)  
  git pull origin master
* git push (将本地分支推送到远程分支)  
  git push  orgin master  
  上面命令表示，将本地分master分支推送到origin筑基的master分支。如果后者不存在，则会被新建。  
  如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。即直接用git push

## git 本地分支与远程分支
* github上已经有master分支 和dev分支  
  git checkout -b dev 新建并切换到本地dev分支  
  git pull origin dev 本地分支与远程分支相关联  
  在本地新建分支并推送到远程   
  git checkout -b test  
  git push origin test   
  这样远程仓库中也就创建了一个test分支  

## 在dev分支开发代码
- git checkout dev  # 切换到dev分支进行开发  
>> 开发代码之后，我们有两个选择  
    1.如果功能开发完成了，可以合并主分支  
      git checkout master  # 切换到主分支  
      git merge dev  # 把dev分支的更改和master合并  
      git push  # 提交主分支代码远程  
      
    2.如果功能没有完成，可以直接推送
      git checkout dev  # 切换到dev远程分支    
      git push  # 提交dev分支到远程

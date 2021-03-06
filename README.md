
# 关于git的相关学习及流程
#### 1、安装git 安装方法网上都有

####  1.1 创建版本库
> ##### 进入需要创建仓库的文件夹位置、使用 git init创建本地仓库

####  1.2 添加文件到版本库
> #####  在版本库中编辑需要更新的文件、git add 文件（若不在版本库根目录需要带上路径），然后使用git commit -m "更改记录" 去进行文件修改的备注

####  1.3 查看版本库状态
> #####  git status 查看当前版本库状态，比如告诉当前哪些文件是add后被修改过的

####  1.4 查看文件修改内容
> #####  若想查看add后文件修改的内容可以使用命令 git diff 文件

####  1.5 文件版本退回
> ##### 使用 git log 查看所有的提交历史记录 git log --pretty=oneline可以进行简化
> ##### 版本退回方法1：git reset --hard HEAD^   '^'为上个版本，若想退回上上个版本为'^^'以此类推

####  1.6 文件版本穿越
> ##### 如果文件版本退回了又想回到最近的版本，可以找到之前的commit id值进行穿越，可以指定跳到该版本 git reset --hard commit的id   commit id只需要前几位就可以了
> #####  如果找不到上个版本号了，可以使用 git reflog 获取每次一次命令找到版本号的commit id

****
#### 2、关于工作区和暂存区
> ##### 工作区即为git init初始化的文件夹，工作区中有个隐藏目录为.git,这是git的版本库，git版本库中最重要的就是stage的暂存区，以及指向master的一个指针叫HEAD。
> ##### git add实际上就是把文件修改添加到暂存区，git commit实际上就是把暂存区的所有内容提交到当前分支，一旦提交暂存区就清除该文件

####  2.1 管理修改
> ##### 若果第一次修改了直接git add后未进行git commit，又进行了第二次修改直接git commit就会只会传入第一次修改的，可以用git diff HEAD -- 文件名称 查看最新文件和上一次git add提交文件的区别

####  2.2 撤销修改
> ##### git checkout -- 文件名可以进行撤销修改，还原最近一次git add的文件内容
> ##### 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
> ##### 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

#### 2.3 删除文件
> ##### 如果一个文件git commit后，直接被删除了，使用git status后git会提示你哪个文件被删除了，现在会有两个选择，一是要从版本库中删除该文件使用命令git rm删除,并且需要git commit。另一种情况是误删，因为版本库还有所以很轻松的可以恢复使用git checkout -- 文件名


****
#### 3 关于远程仓库

> ##### 搭建GIT服务器推荐  推荐查看 [廖雪峰老师的搭建GIT服务器](https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664)

#### 3.1 添加远程仓库

> ##### git remote add origin git@github.com:michaelliao/learngit.git 执行命令添加远程仓库，添加后远程库就叫做origin
> ##### 把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。  由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
> ##### 第一次push后，之后的只要本地作了提交，就可以通过命令 git push origin master 把本地master分支的最新修该推送到git服务器中

#### 3.2 从远程库克隆

> ##### git clone git@github.com:michaelliao/learngit.git

> #### 远程库克隆下的文件内只有master 若想在其他分支上开发则需要执行类似 git checkout -b dev origin/dev命令


****

#### 4 分支管理

> ##### git checkout -b dev 创建并切换到dev分支
> ##### git branch 查看当前分支  git checkout 切换分支，切换不同分支文件的内容会发生变化
> ##### 将dev分支合并到master分支 git merge dev 此命令相当于合并指定分支到当前分支
> ##### 合并后使用 git branch -d dev 删除此分支
> ##### git switch -c dev 创建并切换到dev分支  git switch master直接切换到已有的分值


#### 4.1 解决冲突

> ##### 若两个分值的相同文件都发生了更改， git merge后可以在文件内容中查看不同分支的内容，需要自己修改再git add

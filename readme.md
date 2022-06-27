# 笔记

> git

git 是版本控制工具。版本控制是开发过程中管理我们对文件、目录或工程等内容的修改，同时也方便我们查看更改记录、备份恢复的软件工程技术。简而言之就是管理多人协同开发项目的技术。

------

> 常见版本控制工具

- Git
- SVN
- CVS
- VSS
- TFS
- Visual Studio Online

------

> 版本控制分类

1. **本地版本控制**

   本地做好更新记录。适用于个人。

2. **集中版本控制**

   所有版本数据存放至中央服务器，协同开发者从服务器同步更新或上传修改。代表产品有SVN,CVS,VSS等。

3. **分布式版本控制**

   所有版本信息仓库全部同步到本地的每个用户，这样就可以在本地查看所有版本历史，可以离线在本地提交，只需在连网时push到相应的服务器或其他用户那里。由于每个用户那里保存的都是所有的版本数据，只要有一个用户的设备没有问题就可以恢复所有的数据，但这增加了本地存储空间的占用。

------

> SVN与Git的区别

SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而工作的时候，用的都是自己的电脑，所以首先要从中央服务器得到最新的版本，然后工作，完成工作后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，对网络带宽要求较高。

Git是分布式版本控制系统，没有中央服务器，每个人的电脑就是一个完整的版本库，工作的时候不需要联网了，因为版本都在自己电脑上。协同的方法是这样的：比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。Git可以直接看到更新了哪些代码和文件！

------

> 常见Linux命令

1）、cd : 改变目录。

2）、cd . . 回退到上一个目录，直接cd进入默认目录

3）、pwd : 显示当前所在的目录路径。

4）、ls(ll):  都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。

5）、touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。

6）、rm:  删除一个文件, rm index.js 就会把index.js文件删除。

7）、mkdir:  新建一个目录,就是新建一个文件夹。

8）、rm -r :  删除一个文件夹, rm -r src 删除src目录

rm -rf / 切勿在Linux中尝试！删除电脑中全部文件！
9）、mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下。

10）、reset 重新初始化终端/清屏。

11）、clear 清屏。

12）、history 查看命令历史。

13）、help 帮助。

14）、exit 退出。

15）、#表示注释

------

> Git相关设置

1. Git配置：

   - 查看配置 git config -l

     ```
     #查看系统config
     #git config --system --list　　
     #查看当前用户（global）配置
     #git config --global  --list
     ```

2. 设置用户名与邮箱（用户标识，必要）

   ```
   git config --global user.name "kuangshen"  #名称
   git config --global user.email 24736743@qq.com   #邮箱
   ```

------

> Git 核心基础

1. 工作区域：
   - 工作目录：就是你平时存放项目代码的地方。
   - 暂存区：用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息。
   - 本地仓库：就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本。
   - 远程仓库：托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换。

![image-20220627133825556](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220627133825556.png)

2. 文件的状态
   - Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过git add 状态变为Staged.
   - Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用git rm移出版本库, 则成为Untracked文件
   - Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用git checkout 则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改 !
   - Staged: 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified

3. 查看文件状态

   ~~~
   git status [filename]
   git status
   ~~~

4. 忽略文件

   ~~~~
   #为注释
   *.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
   !lib.txt     #但lib.txt除外
   /temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
   build/       #忽略build/目录下的所有文件
   doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
   ~~~~

5. 使用git

   ~~~
   #使用步骤 从本地创建
   git init
   git add README.md
   ~~~写入文件~~~
   git add .
   git commit -m "修改内容注明"
   git branch -M main
   git remote add origin URL
   git push -u origin main
   ~~~

   ~~~
   git remote add origin URL
   git branch -M main
   git push -u origin main
   ~~~

------

> 分支

可以理解为平行宇宙概念

git常用的分支指令

~~~
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
~~~

如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是我们可以修改冲突文件后重新提交！选择要保留他的代码还是你的代码！

2020年10月1日后，Github会将所有新建的仓库的默认分支从master修改为main。

[解决问题的方法](https://zhuanlan.zhihu.com/p/339370999)：

- 克隆原仓库
- 创建并推送`main`分支
- 修改默认分支
- 删除`master`分支


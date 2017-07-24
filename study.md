### 前言
仅仅是从廖大那里进行的git的学习笔记，把每章后面的总结纪录下来。详细学习还是看廖大教程，非常适合入门。[廖大网址](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
### 基础命令
1. 初始化一个Git仓库，使用git init命令。
2. 添加文件到Git仓库，分两步：
* 第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；
* 第二步，使用命令git commit，完成。
3. 要随时掌握工作区的状态，使用git status命令。
4. 如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

### 时光机穿梭
1. 要随时掌握工作区的状态，使用git status命令。
2. 如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
3. HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。git reset --hard HEAD^ 表示当前版本前一个版本
4. 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
5. 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

### 撤销修改
* 场景1：
当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
* 场景2：
当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
* 场景3：
已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

### 删除
命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

### 远程分支
#### 添加远程库
* 要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
* 关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
* 此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
* 分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

#### 从远程库克隆
要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

### 分支管理
#### 创建和合并分支
* Git鼓励大量使用分支：
* 查看分支：git branch
* 创建分支：git branch <name>
* 切换分支：git checkout <name>
* 创建+切换分支：git checkout -b <name>
* 合并某分支到当前分支：git merge <name>
* 删除分支：git branch -d <name>

#### 解决冲突
* 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交(git add)，合并完成。
* 用git log --graph命令可以看到分支合并图。

#### 分支管理策略
* Git分支十分强大，在团队开发中应该充分应用。
* 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

#### 多人协作
* 查看远程库信息，使用git remote -v；
* 本地新建的分支如果不推送到远程，对其他人就是不可见的；
* 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
* 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
* 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
* 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

### 使用GitHub
* 在GitHub上，可以任意Fork开源仓库；
* 自己拥有Fork后的仓库的读写权限；
* 可以推送pull request给官方仓库来贡献代码。

### 自定义Git
$ git config --global color.ui true

#### 忽略特殊文件
* 忽略某些文件时，需要编写.gitignore；
* .gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！
* 不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：[https://github.com/github/gitignore](https://github.com/github/gitignore)
* 忽略文件的原则（想起自己随便上传github，惭愧啊）
    1. 忽略操作系统自动生成的文件，比如缩略图等；
    2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
    3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

#### 配置别名
这是我最喜欢的功能，类似linux下的alias,ln。比如：git config --global alias.st status ， 输入git st相当于git status,两点注意：
* --global 参数表示对所有git 项目有效，去掉后表示仅对当前项目有效
* 每个仓库的Git配置文件都放在.git/config文件中
* 当前用户的Git配置文件放在用户目录下的.gitConfig中，比如Mac下是：~/.gitconfig

#### 搭建Git服务器





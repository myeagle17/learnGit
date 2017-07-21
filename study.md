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


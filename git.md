# git

------

## git 注意

> 1. 重要的git的代码回滚
> 2. 没有进行push之前，都是在本地仓库进行操作

### git 的基本使用

1. git init：初始化git仓库
2. git status：初始化git分支的状态

![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/41c1de14-5b63-4171-acb7-b90b02807ec0/index_files/41015240.png)

1. git add --all:把目录下的所有代码都添加要提交的事件，然后才能执行git commit命令

2. git clone username@host:/path/to/repository:检出代码

3. git commit -m "提交信息"：提交git版本，并带上提交信息

4. git push origin master :把改变的代码发送到远程库上的 master 分支上

   > origin :表示的是远程仓库的别名,另外orgin/master是指向一个remote branch（从那个branch我们clone数据到本地），然后orgin：表示远程，master：表示本地分支

5. git remote -v/ cat .git/config :查看所有远程的代码库列表

6. git diff ：查看分支合并后的不同之处

7. git log/reflog：查看提交的日志信息/引用日志

8. git grep "main()" : 在工作空间中搜索 mian() 方法

9. git branch : 查看分支

![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/41c1de14-5b63-4171-acb7-b90b02807ec0/index_files/41138128.png)

### 1. git commit （提交版本）

- git commit --amend :提交小修改

### 2. git branch <分支名>（创建分支）

- git checkout -b ：创建一个新的分支同时切换到新创建的分支

> checkout 是选择分支的意思

- git branch -D 分支名：删除本地分支名

### 3. git merge （分支与合并,并且新创建一个版本节点，添加到HEAD所指的分支上）

- git merge bugFix ：把bugFix的分支合并到master上，默认的checkout是master
- git checkout bugFix；git merge master

> merge 后面紧跟着的分支是要合并到checkout所选择的分支上的分支

### 4. git rebase（也是合并分支，并且合并到rebase后面的版本节点上，再有一个版本C1上有多个分支的时候，就会连带C1 版本一起合并到指定的版本节点上）

- git rebase bugFix

> Rebase 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去,rebase 后面的分支是要合并到checkout所选择的分支上

### 5. git fetch：从远程仓库获取数据

> git fetch 并不会改变你本地仓库的状态。它不会更新你的 master 分支，也不会修改你磁盘上的文件,git fetch 一共做了两个动作
>
> 1. 从远程仓库下载本地仓库缺失的提交记录
> 2. 更新远程分支的 origin/master 指针
>
> - git fetch origin foo //git会到远程仓库的foo分支，来获取本地没有的提交，放到本地的o/foo上
> - git fetch origin `<source>`:`<destination>` //表示将source所指的远程库在本地库中都没有的提交都下载到destination的本地分支上，如果source是空的话，就是在本地新创建分支

### 6. git pull：先抓取更新再合并到本地分支

> git pull 相当于 git fetch ；git merge；的缩写

-git pull --rebase;git push：就是先把远程库下载下来，然后和本地库进行合并，最后同步到远程库中

### 7. git push：负责将你的变更传到指定的远程仓库，并在远程仓库合并你新提交的记录

> git push 在处理历史偏移是不可以的，push默认会让你同步远程的代码后再允许你进行变更

- git push origin `<space>`
- git push origin master : origin master 表示把本地库中的master分支同步到远程库中,master，就是公式中的space，默认是同步HEAD指针所指的位置，进行同步
- git push origin `<source>`:`<destination>`
- source 是任何git能识别的位置，source表示的是本地库的分支名，destination是表示远程库的分支，如果source是空的话，就是把远程库的分支删除
- git push origin master:newBranch //表示把本地库的master分支同步到远程库的newBranch分支上，如果newBranch分支不存在就会新建立一个newBranch分支

#### 远程分支的创建和删除

- git push origin <远程分支名>:<本地分支名> // 把本地分支同步到远程仓库，远程仓库如果有就合并，如果没有就新创建一个 <远程分支名>
- git push origin : <本地分支名> // 向远程提交一个空的分支名，就相当于把远程的分支给删除了
- git push origin --delete dbg_lichen_star这两种方式都可以删除指定的远程分支 
  删除本地分支 
  如果想删除刚创建的本地分支，如下命令即可：
- git branch -D dbg_lichen_star 
  这样就把本地的分支删除了
- git pull --rebase;git push ：就是先把历史偏移处理好之后在进行push，来提交你本地所修改的代码

### 在提交树上进行移动

### HEAD （HEAD 是一个对当前检出记录的符号引用）

> HEAD 总是指向当前分支上最近一次提交记录

- 查看 HEAD：HEAD 是根据检出动作（checkout）来进行移动的

> cat .git/HEAD 来查看HEAD 
> git symbolic-ref HEAD 查看他的指向

- 分离 HEAD：

> HEAD -> master -> C1:HEAD指向master，master 指向C1

- git checkout master:通过checkout 来进行HEAD的移动

### git 相对引用

- ^：向上移动1个提交记录 eg: git checkout master^ ;向上移动一个位置 git checkout master^^ 向上移动两个位置
- ~：向上移动多个记录 eg:强制将分支移动num个位置 git branch -f master HEAD~3

> checkout 是选择分支 
> branch -f 是移动分支到指定位置（HEAD的相对位置）

### git 撤销变更

1. git reset：直接回滚到上一个版本（本地可以，远程无效）

   > git reset HEAD~1:回滚到上一个版本

2. git revert：表示在原版本的基础上又提交了一个原来的版本

### git 基本信息

1. 远程分支命名规范：`<remote name>/<branch name>`

## 不常用的命令

- git cherry-pick：选取要提交的分支版本进行提交(版本名-哈希值)

### 交互式rebase

- git rebase -i HEAD~4：将当前分支向上移动4个版本，然后在这4个版本中选择进行复制

> 在交互式界面中可以用鼠标进行拖动，并且可以调整顺序

### 本地栈式提交

- git commit --amend：对当期结点做简单的修改

## git tags（锚点的作用） 标签可以固定在某个版本不动，因为分支是很容易被人改动的

- git tag v1 C1：给C1版本起个表签名叫v1

> 默认指向HEAD所指的位置 eg： git tag v1

- git bisect：查找产生bug的提交记录的指令
- git describe <分支名/ref>：

> 输出结果解释 
> `<tag>`_`<numCommits>`_g`<hash>` 
> tag：表示的是离分支名（ref）最近的标签 
> numCommits：表示的是分支名与标签相差几个提交版本 
> hash：表示的是提交记录哈希值的前几位

### 两个父节点

> 也是使用~和^符号，当遇到分支版本时，这两个符号后面跟的数字是选择移动的分支的意思

- git checkout HEAD~2 :当遇到两个父节点的时候是选择第二条路径的意思
- git checkout HEAD~^2~2：表示的意思是先向上一个版本移动一个版本，然后选择第二条路径，再向上移动两个版本

### 远程追踪

- git checkout -b foo o/master：表示使用隐含目标来更新foo分支，然后就可以在foo分支上使用pull来进行下载远程分支了
- git checkout -b foo o/master：表示的是创建分支foo并且把o/master 隐含的移动到foo上，这样就可以使用push对远程进行更新了
- git branch -u o/master foo;git commit;git push; 直接可以在foo上直接进行push 与之前两个命令效果一样

## Rebase 与 Merge 的比较

### rebase

- 优点：Rebase 是你的提交树变的很干净，所有的提交都在一条线上
- 缺点：Rebase 修改了提交树的历史

### merge

- 优电就是可以保留提交历史
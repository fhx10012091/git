# git基本用法

### 作用

+ 管理不同版本，随时回退到任意时刻
+ 协同项目（自动合并代码）

### 使用

```
git init 初始化仓库，在文件目录中生成一个.git文件
```

```
git status 查看当前仓库的状态，只要对文件进行了修改，文件就会变红，红色文件代表有新的变更，就重新把文件从工作区到暂存区到仓库区
```

```
git仓库有工作区，暂存区，仓库区
git add */filename/.  把工作区的文件放入暂存区
```

```
把暂存区文件提交到仓库(本地仓库)，只提交哪些变绿的文件
git commit -m <message>
```

```
查看日志
git log // 可以看见什么人在什么时间提交了一个commit，并生成一个hash值，唯一的，相当于是commit的身份证
```

```
当已add文件后，但后悔提交了，可以回退，把绿色文件变成红色的（没有操作commit）
git reset <filename> 
```

```
git 四种状态
untracked(未被跟踪)
unmodified（未修改）
modified（已修改）
staged（在暂存区中）

当从github远程库中clone项目到本地后，该项目中所有文件状态为unmodified；在该项目中新建一个文件后，该文件的状态为untracked，通过git add文件状态变为unmodified(此时该文件的状态同时为staged，已经存在暂存区中了，其实git add的潜台词就是把目标文件加入暂存区域)，通过编辑，文件状态变为modified，被修改的文件未被放到暂存区域中，此时通过git status命令查看的话，会发现暂存区中和未暂存区同时存在该文件！！！为什么会这样呢？？？因为此时暂存区中的该文件是上次通过git add命令添加时候所处的状态，而未暂存区中该文件的状态是这次通过编辑后所处的状态，git记录了两种状态，如果这个时候用git commit命令提交该文件，只会把该文件的前一种状态保存到git仓库，修改后的状态不会保存到git仓库，要通过git add操作才能将修改后的文件状态加入到暂存区域中，然后可以通过git commit命令将修改后的文件提交到git仓库，有点啰嗦了==，能够理解就好^_^。
```

```
alias 
ad = add .
cmm = commit -m
lg = log
rlg = reflog
co = checkout
cob = checkout -b
cod = checkout develop
com = checkout master
fc = fetch
cm = commit
st = status
pl = pull
ps = push
```

```
已提交多次commit,但发现以前提交的版本好，想回退到以前的版本
git reset <commitID> --hard
默认
--hard 不保存所有变更 就是要变更到的hashID以后的commit全部删除，就当什么都没有改，文件里面的内容也变成要变更的hashID时的数据（数据要变）
--soft 保留变更且变更内容处于staged 保留变更就是内容不改，且存储到暂存区的，然后对内容进行修改
--mixed 保留变更且变更内容处于Modified 也在工作区
```

```
如果后悔了想回到最新的commit怎么办
git reflog 查看所有的操作记录
git reset <commitID>     // id长度不一样，hash值很长，但只需要前7位hash就可以锁定对应的commit操作，所有全称和前7位也是一样的

方法二
git pull 更方便

```

### 分支

```
如果要变更commit，要来回使用reset，且无规则，也要用id，记不住
可以用分支来解决
-b -branch 分支
git checkout -b <name><template>
name 分支的名字
template 那个分支为模板

新分支的记录(commit)会继承自模板分支
切完分支后，分支的改动与其他分支就没有任何关系了

git checkout 切换分支
git branch 查看所有分支
需要查看那个版本就可以切换相应的分支
git merge <branchname>合并分支变更 
```



```
git clone 尽量是https拷贝数据
```

```
小A
首先也是把远程仓库的项目克隆到本地，尽量新切分支
git clone
本地新切的一个分支
git checkout -b 分支
把本地分支上传至上流分支，在远程仓库新增一个分支
git push --set-upstream origin 分支
写项目，修改代码
git add .
git commit -m ''
git push
就可以把本地变更推送到远端了
小B
首先也是把远程仓库的项目克隆到本地
git clone
获取（知道而已，跟自己没关系）远程仓库的信息，比如分支，但本地还是没有，只是展示新分支
git fetch //必须进入项目文件夹，就相当于里面的文件才需要更改的
git checkout 分支 // 这里必须要执行上面一个步骤，否则就不能执行切换分支了，这个分支也是本地的，但是模板分支来自远程仓库 
这里也不需要再创建一个远程仓库了，因为这个分支就是来自远程仓库

如果没有git fetch ,git checkout 就会一直向远程仓库来切换分支，很浪费网络资源
git checkout -b 本地分支名 origin 远程仓库分支名

git pull 是先fetch 再merge
```

```
git rebase 分支
```


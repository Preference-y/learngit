# git的安装与基本使用方法

## 1.git的安装

### 1.1 在Windows上安装Git

msysgit是Windows版的Git，从[https://git-for-windows.github.io](https://link.jianshu.com?t=https://git-for-windows.github.io)下载（网速慢的同学请移步国内镜像），然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，设置自己的用户名和邮箱，在命令行输入：

```csharp
$ git config --global user.name "Your Name" (设置用户名)
$ git config --global user.email "email@example.com" （设置常用邮箱，最好与guihub用的邮箱一致）
```

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

### 1.2 在Mac OS X上安装Git

如果你正在使用Mac做开发，有两种安装Git的方法。

一是安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：[http://brew.sh/](https://link.jianshu.com?t=http://brew.sh/)。

第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

Xcode是Apple官方IDE，功能非常强大，是开发Mac和iOS App的必选装备，而且是免费的！

## 2.创建版本库

### 2.1版本库

版本库又名仓库，英文名repository,你可以简单的理解一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻还可以将文件”还原”。所以创建一个版本库也非常简单，如下我是E盘 目录下新建一个testgit版本库。

```ruby
$ cd E:(找到E盘)
$ cd www(假如在www文件夹下)
$ mkdir testgit（新建名叫testgit的文件夹）
$ cd testgit（找到testgit文件夹）
$ pwd （显示当前目录）
/e/testgit
```

pwd命令用于显示当前目录。在我的电脑上，这个仓库位于/e/testgit

如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。

第二步，通过git init命令把这个目录变成Git可以管理的仓库：

```jsx
$ git init
Initialized empty Git repository in E:/testgit/.git/
```

瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。
 也不一定必须在空目录下创建Git仓库，选择一个已经有东西的目录也是可以的。不过，不建议你使用自己正在开发的公司项目来学习Git，否则造成的一切后果概不负责。
 以上全部步骤在git上操作如下图：



![img](https:////upload-images.jianshu.io/upload_images/4889822-566528249b3593b9?imageMogr2/auto-orient/strip|imageView2/2/w/690/format/webp)

命令详细步骤

电脑磁盘下的.git



![img](https:////upload-images.jianshu.io/upload_images/4889822-0e3530d00062d921?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

这里写图片描述

### 2.2把文件添加到版本库中。

首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。

因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

**演示demo:**
 我在版本库testgit目录下新建一个记事本文件 readme.txt 内容如下：Git is a version control system.

一定要放到testgit目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。

**第一步，用命令git add告诉Git，把文件添加到仓库：**
 `$ git add readme.txt`

执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。

**第二步，用命令git commit告诉Git，把文件提交到仓库：**
 `$ git commit -m "wrote a readme file" [master (root-commit) cb926e7] wrote a readme file 1 file changed, 2 insertions(+) create mode 100644 readme.txt`

如下图：



![img](https:////upload-images.jianshu.io/upload_images/4889822-10d04edc48a5c1a3?imageMogr2/auto-orient/strip|imageView2/2/w/688/format/webp)

这里写图片描述

简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

嫌麻烦不想输入-m "xxx"行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。实在不想输入说明的童鞋请自行Google，我不告诉你这个参数。

`git commit`命令执行成功后会告诉你，1个文件被改动（我们新添加的readme.txt文件），插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：

```ruby
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

#### 小结:

初始化一个Git仓库，使用git init命令。

添加文件到Git仓库，分两步：

第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；

第二步，使用命令`git commit`，完成。

现在我们已经提交了一个readme.txt文件了，我们下面可以通过命令`git status`来查看是否还有文件未提交，如下：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-313e40d07476c8f2?imageMogr2/auto-orient/strip|imageView2/2/w/692/format/webp)

这里写图片描述

 说明没有任何文件未提交，但是我现在继续来改下readme.txt内容，比如我在下面添加一行123456内容，继续使用

```
git status
```

来查看下结果，如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-a18329365e661899?imageMogr2/auto-orient/strip|imageView2/2/w/690/format/webp)

这里写图片描述

 上面的命令告诉我们 readme.txt文件已被修改，但是未被提交的修改。



接下来我想看下readme.txt文件到底改了什么内容，如何查看呢？可以使用如下命令：

`git diff` readme.txt 如下：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-5a16ab9e49d7dc11?imageMogr2/auto-orient/strip|imageView2/2/w/690/format/webp)

这里写图片描述

 git diff顾名思义就是查看difference，显示的格式正是Unix通用的diff格式.



如上可以看到，readme.txt文件内容从两行Git is a version control system.Git is free software.改成 二行 添加了一行123456内容。

知道了对readme.txt文件做了什么修改后，我们可以放心的提交到仓库了，提交修改和提交文件是一样的2步(第一步是git add  第二步是：git commit。)

**小结：**

要随时掌握工作区的状态，使用`git status`命令。

如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-0bf7734ef4e3104f?imageMogr2/auto-orient/strip|imageView2/2/w/717/format/webp)

这里写图片描述



## 3.操作追踪

### 3.1 版本回退

如上，我们已经学会了修改文件，现在我继续对readme.txt文件进行修改，再修改一次内容为：
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 继续执行命令如下：

```csharp
$ git add readme.txt
$ git commit -m "append GPL"
[master 3628164] append GPL
 1 file changed, 1 insertion(+), 1 deletion(-)
```

不断对文件进行修改，然后不断提交修改到版本库里，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为commit。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个commit恢复，然后继续工作，而不是把几个月的工作成果全部丢失。
 现在我已经对readme.txt文件做了三次修改了，那么我现在想查看下历史记录，如何查呢？我们现在可以使用命令 `git log`演示如下所示：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-2c6a45bc29b17dea?imageMogr2/auto-orient/strip|imageView2/2/w/720/format/webp)

这里写图片描述

```
git log
```

命令显示从最近到最远的提交日志，我们可以看到2次提交，最近的一次是append GPL，最早的一次是wrote a readme file。.如果嫌上面显示的信息太多的话，我们可以使用命令 

```
git log –pretty=oneline
```

 演示如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-315486e990f59f48?imageMogr2/auto-orient/strip|imageView2/2/w/702/format/webp)

这里写图片描述



需要友情提示的是，你看到的一大串类似3628164...882e1e0的是commit id（版本号），和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。为什么commit id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。

现在我想使用版本回退操作，我想把当前的版本回退到上一个版本，要使用什么命令呢？可以使用如下2种命令，第一种是：`git reset –hard HEAD^`那么如果要回退到上上个版本只需把`HEAD^`改成 `HEAD^^`以此类推。那如果要回退到前100个版本的话，使用上面的方法肯定不方便，我们可以使用下面的简便命令操作：`git reset –hard HEAD~100`即可。
 未回退之前的readme.txt内容如下：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-865fe13c339e28ac?imageMogr2/auto-orient/strip|imageView2/2/w/462/format/webp)

这里写图片描述



如果想回退到上一个版本就可以使用`git reset`命令：

```ruby
$ git reset --hard HEAD^
```

再来查看下 readme.txt内容，通过命令`cat readme.txt`查看

最后我们用`git log`再看看现在版本库的状态。
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-d41387e8888127ce?imageMogr2/auto-orient/strip|imageView2/2/w/725/format/webp)

这里写图片描述



现在我想回退到**最新的版本**:只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个append GPL的commit id是fc632000db...，于是就可以指定回到未来的某个版本：
 $ git reset --hard  fc632000db
 HEAD is now at  fc632000db append GPL

版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。
 再看看readme.txt的内容：



![img](https:////upload-images.jianshu.io/upload_images/4889822-597efeb5db284896?imageMogr2/auto-orient/strip|imageView2/2/w/458/format/webp)

这里写图片描述

果然，我胡汉三又回来了。
 Git的版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，Git仅仅是把HEAD从指向append GPL.
 假如我已经关掉过一次命令行或者commit id内容的版本号我并不知道呢？要如何知道commit id内容的版本号呢？可以通过如下命令即可获取到版本号：`git reflog` 演示如下：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-df042ced1ec00618?imageMogr2/auto-orient/strip|imageView2/2/w/715/format/webp)

这里写图片描述



`git reflog`用来记录你的每一次命令.

**小结:**

1. HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
2. 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
3. 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

### 3.2 工作区与暂存区的区别

**工作区**：就是你在电脑上看到的目录，比如目录下testgit里的文件(.git隐藏目录版本库除外)。或者以后需要再新建的目录文件等等都属于工作区范畴。

**版本库(Repository)**：工作区有一个隐藏目录.git,这个不属于工作区，这是版本库。其中版本库里面存了很多东西，其中最重要的就是stage(暂存区)，还有Git为我们自动创建了第一个分支master,以及指向master的一个指针HEAD。

我们前面说过使用Git提交文件到版本库有两步：

第一步：是使用 git add 把文件添加进去，实际上就是把文件添加到暂存区。

第二步：使用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支上。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

现在，我们再练习一遍，先对readme.txt做个修改，比如加上一行内容：
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.

接着在目录下新建一个文件为test.txt 内容为test
 先用`git status`查看一下状态：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-24b60b85bf8ce80c?imageMogr2/auto-orient/strip|imageView2/2/w/716/format/webp)

这里写图片描述



Git非常清楚地告诉我们，readme.txt被修改了，而test还从来没有被添加过，所以它的状态是Untracked。
 现在我们先使用git add 命令把2个文件都添加到暂存区中，再使用git status来查看下状态，如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-0bec93edb9ed6a34?imageMogr2/auto-orient/strip|imageView2/2/w/698/format/webp)

这里写图片描述

接着我们可以使用`git commit`一次性提交到分支上，如下：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-60fec13304a913c5?imageMogr2/auto-orient/strip|imageView2/2/w/716/format/webp)

这里写图片描述



**小结**

- 暂存区是Git非常重要的概念，弄明白了暂存区，就弄明白了Git的很多操作到底干了什么。
- 没弄明白暂存区是怎么回事的童鞋，请向上滚动页面，再看一次。

### 3.3 Git管理修改操作。

Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。什么是修改？比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。
 为什么说Git管理的是修改，而不是文件呢？我们还是做实验。第一步，对readme.txt做一个修改，比如加一行内容：
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.
 Git tracks changes.
 查看readme.txt内容：



![img](https:////upload-images.jianshu.io/upload_images/4889822-904b6d9bdd285a45?imageMogr2/auto-orient/strip|imageView2/2/w/714/format/webp)

这里写图片描述

然后，添加：



![img](https:////upload-images.jianshu.io/upload_images/4889822-4b506aca7a22a2bb?imageMogr2/auto-orient/strip|imageView2/2/w/452/format/webp)

这里写图片描述

 然后，再修改readme.txt：



![img](https:////upload-images.jianshu.io/upload_images/4889822-ea6715f51e6b7188?imageMogr2/auto-orient/strip|imageView2/2/w/450/format/webp)

这里写图片描述

 提交后，然后查看状态：



![img](https:////upload-images.jianshu.io/upload_images/4889822-3e5bb4d536b4109e?imageMogr2/auto-orient/strip|imageView2/2/w/712/format/webp)

这里写图片描述

 我们回顾一下操作过程： 

第一次修改 -> git add -> 第二次修改 -> git commit

你看，我们前面讲了，Git管理的是修改，当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，git commit只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-a802c8ff35c82bfb?imageMogr2/auto-orient/strip|imageView2/2/w/546/format/webp)

这里写图片描述





![img](https:////upload-images.jianshu.io/upload_images/4889822-37b1bd974d899f63?imageMogr2/auto-orient/strip|imageView2/2/w/706/format/webp)

这里写图片描述

可见，第二次修改确实没有被提交。

那怎么提交第二次修改呢？你可以继续`git add`再`git commit`，也可以别着急提交第一次修改，先`git add`第二次修改，再`git commit`，就相当于把两次修改合并后一块提交了：

第一次修改 -> git add -> 第二次修改 -> git add -> git commit

好，现在，把第二次修改提交了。

**小结:**

现在，你又理解了Git是如何跟踪修改的，每次修改，如果不add到暂存区，那就不会加入到commit中。

### 3.4 Git撤销修改和删除文件操作。

#### **3.4.1  撤销修改**


最新版本的git已经使用git restore 代替了原来的reset和checkout命令了，如下：

git resotre readme //（使用 "git restore <文件>..." 丢弃工作区的改动） (use "git restore ..." to discard changes in working directory)

git restore --staged readme
//（使用 "git restore --staged <文件>..." 以取消暂存） (use "git restore --staged ..." to unstage)




 比如我现在在readme.txt文件里面增加一行 内容为My stupid boss still prefers SVN.我们先通过命令查看如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-46a64b9e1d8df2af?imageMogr2/auto-orient/strip|imageView2/2/w/693/format/webp)

这里写图片描述

在准备提交前，发现My stupid boss still prefers SVN这句话有错误，想恢复上一个版本的状态，有如下几种方法可以做修改：

1. 如果我知道要删掉那些内容的话，直接手动更改去掉那些需要的文件，然后add添加到暂存区，最后commit掉。
2. 我可以按以前的方法直接恢复到上一个版本。使用`git reset –hard HEAD^`

但是现在我不想使用上面的2种方法，我想直接想使用撤销命令该如何操作呢？首先在做撤销之前，我们可以先用 `git status`查看下当前的状态。如下所示：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-3a83e8b94f828e2f?imageMogr2/auto-orient/strip|imageView2/2/w/704/format/webp)

这里写图片描述

 可以发现，Git会告诉你，git checkout  — file 可以丢弃工作区的修改，如下命令：



`git checkout — readme.txt`,如下所示：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-4629625338190020?imageMogr2/auto-orient/strip|imageView2/2/w/694/format/webp)

这里写图片描述



命令 git checkout –readme.txt 意思就是，把readme.txt文件在工作区做的修改全部撤销，这里有2种情况，如下：

1. readme.txt自动修改后，还没有放到暂存区，使用 撤销修改就回到和版本库一模一样的状态。
2. 另外一种是readme.txt已经放入暂存区了，接着又作了修改，撤销修改就回到添加暂存区后的状态。

假如你不但写错了，还git add到暂存区了。

对于第二种情况，我想我们继续做demo来看下，假如现在我对readme.txt添加一行 内容为My stupid boss still prefers SVN.，我git add 增加到暂存区后，接着添加内容good jop see you，我想通过撤销命令让其回到暂存区后的状态。如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-2f4bc05b3394672d?imageMogr2/auto-orient/strip|imageView2/2/w/692/format/webp)

这里写图片描述

**注意：**命令`git checkout -- readme.txt` 中的`--` 很重要，如果没有`--`的话，那么命令变成创建分支了。

在commit之前。用git status查看一下，修改只是添加到了暂存区，还没有提交 ,并且Git还告诉我们，用命令`git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-9ecd1424585b5d39?imageMogr2/auto-orient/strip|imageView2/2/w/698/format/webp)

这里写图片描述

```
git reset
```

命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。



再用git status查看一下，现在暂存区是干净的，工作区有修改：
 



![img](https:////upload-images.jianshu.io/upload_images/4889822-bddf04ce06206151?imageMogr2/auto-orient/strip|imageView2/2/w/675/format/webp)

这里写图片描述

 下面，我们再丢弃工作区的修改：



![img](https:////upload-images.jianshu.io/upload_images/4889822-3603a7fd66240a55?imageMogr2/auto-orient/strip|imageView2/2/w/691/format/webp)

这里写图片描述

 现在，假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？还记得版本回退一节吗？可以回退到上一个版本。不过，这是有条件的，就是你还没有把自己的本地版本库推送到远程。还记得Git是分布式版本控制系统吗？我们后面会讲到远程版本库，一旦你把“stupid boss”提交推送到远程版本库，你就真的惨了……



**小结：**

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

#### **3.4.2 删除文件**

假如我现在版本库testgit目录添加一个文件b.txt,然后提交。如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-9319f7f3d0fd4ca5?imageMogr2/auto-orient/strip|imageView2/2/w/698/format/webp)

这里写图片描述

如上：一般情况下，可以直接在文件目录中把文件删了，或者使用如上rm命令：rm b.txt ，如果我想彻底从版本库中删掉了此文件的话，可以再执行commit命令 提交掉，现在目录是这样的:



![img](https:////upload-images.jianshu.io/upload_images/4889822-f33aafb72e848124?imageMogr2/auto-orient/strip|imageView2/2/w/800/format/webp)

这里写图片描述

只要没有commit之前，如果我想在版本库中恢复此文件如何操作呢？

可以使用如下命令 git checkout  — b.txt，如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-e836a2b17bf6aff3?imageMogr2/auto-orient/strip|imageView2/2/w/687/format/webp)

这里写图片描述

再来看看我们testgit目录，添加了1个文件了。如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-1a0564da4b2b198c?imageMogr2/auto-orient/strip|imageView2/2/w/802/format/webp)

这里写图片描述

## 4. 远程仓库

在了解之前，先注册github账号，由于你的本地Git仓库和github仓库之间的传输是通过SSH加密的，所以需要一点设置：

> 第一步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果有的话，直接跳过此如下命令，如果没有的话，打开命令行，输入如下命令：
>  `ssh-keygen -t rsa –C "youremail@example.com"`, 你需要把邮件地址换成你自己的邮件地址,并且必须要用双引号，不能用单引号。然后一路回车，使用默认值即可。由于我本地此前运行过一次，所以本地有，如下所示：

> ![img](https:////upload-images.jianshu.io/upload_images/4889822-11f7fdded330c67d?imageMogr2/auto-orient/strip|imageView2/2/w/994/format/webp)
>
> 文件显示
>
> id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
>
> 第二步：登录github,打开” settings”中的SSH Keys页面，然后点击“Add SSH Key”,填上任意title，在Key文本框里黏贴id_rsa.pub文件的内容。点击 Add Key，你就应该可以看到已经添加的key。
>
> 
>
> ![img](https:////upload-images.jianshu.io/upload_images/4889822-796b6e347a88caa7?imageMogr2/auto-orient/strip|imageView2/2/w/790/format/webp)
>
> 这里写图片描述

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。确保你拥有一个GitHub账号后，我们就即将开始远程仓库的学习。

### 4.1 添加远程仓库

现在的情景是：我们已经在本地创建了一个Git仓库后，又想在github创建一个Git仓库，并且希望这两个仓库进行远程同步，这样github的仓库可以作为备份，又可以其他人通过该仓库来协作。

首先，登录github上，然后在右上角找到“create a new repo”创建一个新的仓库。如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-e312b0700ce5c760?imageMogr2/auto-orient/strip|imageView2/2/w/1142/format/webp)

创建仓库页面

在Repository name填入testgit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库(**我的github被我汉化了，有兴趣的可以关注我的github账号，仓库里有插件，有安装教程**)：



![img](https:////upload-images.jianshu.io/upload_images/4889822-53526b368ed69dd1?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

仓库创建完成后页面

目前，在GitHub上的这个testgit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

现在，我们根据GitHub的提示，在本地的testgit仓库下运行命令：

```
git remote add origin https://github.com/tugenhua0707/testgit.git`或者
 `$ git remote add origin git@github.com:michaelliao/learngit.git
```



![img](https:////upload-images.jianshu.io/upload_images/4889822-76b129bd80017bd8?imageMogr2/auto-orient/strip|imageView2/2/w/1039/format/webp)

两种写法

所有的如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-76ecf5b5b90c39ed?imageMogr2/auto-orient/strip|imageView2/2/w/719/format/webp)

这里写图片描述

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

下一步，就可以把本地库的所有内容推送到远程库上：



![img](https:////upload-images.jianshu.io/upload_images/4889822-ca480fe62db1aa9c?imageMogr2/auto-orient/strip|imageView2/2/w/682/format/webp)

推送过程与报错解决

> 报错解释：git clone [git://github.com/username/testgit.git](https://link.jianshu.com?t=git://github.com/username/testgit.git) 这是使用 git 协议。

> [git@github.com](https://link.jianshu.com?t=mailto:git@github.com):username/testgit.git 这是使用 ssh 协议。ssh 会验证对方服务器的 key。它没办法确认服务器出示的 key 是受信的，所以问你这个 key 是不是真的是你要连接的那个服务器的。你没说「yes」所以 ssh 认为你不想继续连接，所以连接失败。

把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。

由于远程库是空的，我们第一次推送master分支时，加上了 –u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。推送成功后，可以立刻在github页面中看到远程库的内容已经和本地一模一样了:





![img](https:////upload-images.jianshu.io/upload_images/4889822-d7c6e00bad4fc097?imageMogr2/auto-orient/strip|imageView2/2/w/1044/format/webp)

推送

 从现在起，只要本地作了提交，就可以通过命令：



```
$ git push origin master
```

把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

**SSH警告**

当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established. RSA key fingerprint is xx.xx.xx.xx.xx. Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```

这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。

**小结**

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git；`

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

### 4.2 从远程库克隆

上次我们讲了先有本地库，后有远程库的时候，如何关联远程库。

现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

首先，登陆GitHub，创建一个新的仓库，名字叫testgit2（注意：仓库名是不能重名的）：



![img](https:////upload-images.jianshu.io/upload_images/4889822-9066a38a315ad060?imageMogr2/auto-orient/strip|imageView2/2/w/948/format/webp)

在远程仓库先创建仓库

我们勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到README.md文件：



![img](https:////upload-images.jianshu.io/upload_images/4889822-7556588dc6a5ef2d?imageMogr2/auto-orient/strip|imageView2/2/w/1015/format/webp)

这里写图片描述

现在，远程库已经准备好了，下一步是用命令`git clone`克隆一个本地库：



![img](https:////upload-images.jianshu.io/upload_images/4889822-517d73e971189ff7?imageMogr2/auto-orient/strip|imageView2/2/w/582/format/webp)

克隆本地仓库

接着在我本地testgit目录下 生成testgit2目录了，如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-a64630702b16b09f?imageMogr2/auto-orient/strip|imageView2/2/w/743/format/webp)

本地目录

如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。

你也许还注意到，GitHub给出的地址不止一个，还可以用[https://github.com/michaelliao/gitskills.git](https://link.jianshu.com?t=https://github.com/michaelliao/gitskills.git)这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。

使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。

**小结：**

要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。

Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

## 5.  分支管理

### 5.1 创建与合并分支

在版本回填退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

首先，我们来创建dev分支，然后切换到dev分支上。如下操作：



![img](https:////upload-images.jianshu.io/upload_images/4889822-24e6c367014247b6?imageMogr2/auto-orient/strip|imageView2/2/w/567/format/webp)

创建分支

git checkout 命令加上 –b参数表示创建并切换，相当于如下2条命令

```
git branch dev
git checkout dev
```

然后，用git branch命令查看当前分支，git branch命令会列出所有分支，当前分支前面会标一个*号。

然后，我们就可以在dev分支上正常提交，比如对readme.txt做个修改，加上一行：Creating a new branch is quick.
 首先我们先来查看下readme.txt内容，接着添加内容Creating a new branch is quick，如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-3c4eb67c54789528?imageMogr2/auto-orient/strip|imageView2/2/w/645/format/webp)

提交

现在dev分支工作已完成，现在我们切换到主分支master上，继续查看readme.txt内容如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-f064836ef1e22bef?imageMogr2/auto-orient/strip|imageView2/2/w/641/format/webp)

切换分支

切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变：



![img](https:////upload-images.jianshu.io/upload_images/4889822-47487064522a28b2?imageMogr2/auto-orient/strip|imageView2/2/w/452/format/webp)

详情

现在，我们把dev分支的工作成果合并到master分支上，使用如下命令 `git merge dev`如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-1975bb4ce0a36ba4?imageMogr2/auto-orient/strip|imageView2/2/w/640/format/webp)

合并分支

`git merge`命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和dev分支的最新提交是完全一样的。

注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。

当然，也不是每次合并都能Fast-forward，我们后面会讲其他方式的合并。

合并完成后，就可以放心地删除dev分支了,操作如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-fd8bf477d9f18223?imageMogr2/auto-orient/strip|imageView2/2/w/640/format/webp)

删除dev分支

删除后，查看branch，就只剩下master分支了。

**小结：**

查看分支：**git branch**

创建分支：**git branch**

切换分支：**git checkout**

创建+切换分支：**git checkout -b**

合并某分支到当前分支：**git merge**

删除分支：**git branch -d**

### 5.2 解决冲突

有时候合并分支并不会很顺利，会出现一些意外，下面我们先来创建一个新的分支叫做feature1，继续我们的新分支开发，并在readme.txt添加一行内容8888888，然后提交，如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-7bc746fd2a4de703?imageMogr2/auto-orient/strip|imageView2/2/w/683/format/webp)

创建新分支

同样，我们现在切换到master分支上来，也在最后一行添加内容，内容为99999999，如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-224d593a1d3ff472?imageMogr2/auto-orient/strip|imageView2/2/w/684/format/webp)

在master分支上修改

现在我们需要在master分支上来合并feature1，如下操作：



![img](https:////upload-images.jianshu.io/upload_images/4889822-60f1b23c7bbad071?imageMogr2/auto-orient/strip|imageView2/2/w/760/format/webp)

合并分支出现冲突

果然冲突了！Git告诉我们，readme.txt文件存在冲突，必须手动解决冲突后再提交。git status也可以告诉我们冲突的文件。

查看一下readme.txt文件：



![img](https:////upload-images.jianshu.io/upload_images/4889822-7bb0634851187507?imageMogr2/auto-orient/strip|imageView2/2/w/938/format/webp)

readme.txt文件

Git用`<<<<<<<，=======，>>>>>>>`标记出不同分支的内容，其中`<<<HEAD`是指主分支修改的内容，`>>>>>feature1` 是指feature1上修改的内容，我们可以修改下如下后保存，然后再提交：



![img](https:////upload-images.jianshu.io/upload_images/4889822-4ab9d93aff9ff56c?imageMogr2/auto-orient/strip|imageView2/2/w/762/format/webp)

修改再提交

如果我想查看分支合并的情况的话，需要使用命令 git log.命令行演示如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-75725d5f9b737239?imageMogr2/auto-orient/strip|imageView2/2/w/759/format/webp)

查看分支合并图

**小结：**

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

用git log --graph命令可以看到分支合并图。

### 5.3 分支管理策略

通常合并分支时，git一般使用”Fast forward”模式，在这种模式下，删除分支后，会丢掉分支信息，现在我们来使用带参数 –no-ff来禁用”Fast forward”模式。首先我们来做demo演示下，操作步骤如下：

1. 创建一个dev分支。
2. 修改readme.txt内容。
3. 添加到暂存区。
4. 切换回主分支(master)。
5. 合并dev分支，使用命令 git merge –no-ff  -m “注释” dev
6. 查看历史记录

截图如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-abaf831a513a5e0e?imageMogr2/auto-orient/strip|imageView2/2/w/762/format/webp)

管理分支

因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。可以看到，不使用Fast forward模式，merge后就像这样：



![img](https:////upload-images.jianshu.io/upload_images/4889822-cf4fa27a35cc74a0?imageMogr2/auto-orient/strip|imageView2/2/w/561/format/webp)



**分支策略：**

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

所以，团队合作的分支看起来就像这样：



![img](https:////upload-images.jianshu.io/upload_images/4889822-3a972df1557dcd6c?imageMogr2/auto-orient/strip|imageView2/2/w/533/format/webp)



**小结：**

Git分支十分强大，在团队开发中应该充分应用。

合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

### 5.4  bug分支

在开发中，会经常碰到bug问题，那么有了bug就需要修复，在Git中，分支是很强大的，每个bug都可以通过一个临时分支来修复，修复完成后，合并分支，然后将临时的分支删除掉。

比如我在开发中接到一个404 bug时候，我们可以创建一个404分支来修复它，但是，当前的dev分支上的工作还没有提交。比如如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-24796a47ffa305c7?imageMogr2/auto-orient/strip|imageView2/2/w/563/format/webp)



并不是我不想提交，而是工作进行到一半时候，我们还无法提交，比如我这个分支bug要2天完成，但是我issue-404 bug需要2个小时内完成。怎么办呢？还好，Git还提供了一个stash功能，可以把当前工作现场 ”隐藏起来”，等以后恢复现场后继续工作。如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-aef54f3df4a7e169?imageMogr2/auto-orient/strip|imageView2/2/w/565/format/webp)

保存工作现场

现在，用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。现在我可以通过创建issue-404分支来修复bug了。

首先我们要确定在那个分支上修复bug，假定需要在主分支master上来修复的，现在我要在master分支上创建一个临时分支，演示如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-fbd72b5fe6cbc239?imageMogr2/auto-orient/strip|imageView2/2/w/766/format/webp)

创建临时分支

bug修复完成后，切换到master分支上，并完成合并，最后删除issue-404分支。演示如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-82d50f5db24ccf6a?imageMogr2/auto-orient/strip|imageView2/2/w/764/format/webp)

删除临时分支issue-404

现在，我们回到dev分支上干活了。



![img](https:////upload-images.jianshu.io/upload_images/4889822-d999f0f6847e8220?imageMogr2/auto-orient/strip|imageView2/2/w/678/format/webp)

切换到dev分支

工作区是干净的，那么我们工作现场去哪里呢？我们可以使用命令 `git stash list`来查看下。如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-1013410a64e862c3?imageMogr2/auto-orient/strip|imageView2/2/w/525/format/webp)



工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，可以使用如下2个方法：

1.  `git stash apply`恢复，恢复后，stash内容并不删除，你需要使用命令`git stash drop`来删除。
2. 另一种方式是使用`git stash pop`,恢复的同时把stash内容也删除了。

演示如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-31480eab43759364?imageMogr2/auto-orient/strip|imageView2/2/w/660/format/webp)



你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：



![img](https:////upload-images.jianshu.io/upload_images/4889822-845638839ac673bf?imageMogr2/auto-orient/strip|imageView2/2/w/570/format/webp)

恢复指令

**小结：**

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场。

### 5.5 Feature分支

软件开发中，总有无穷无尽的新的功能要不断添加进来。

添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

现在，开始一个新任务：开发代号为Vulcan的新功能。开始开发：



![img](https:////upload-images.jianshu.io/upload_images/4889822-c4fa45765045704a?imageMogr2/auto-orient/strip|imageView2/2/w/662/format/webp)



切回dev，准备合并：一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。

但是，就在此时，接到上级命令，因经费不足，新功能必须取消！

虽然白干了，但是这个分支还是必须就地销毁：



![img](https:////upload-images.jianshu.io/upload_images/4889822-e763bb7770576ea6?imageMogr2/auto-orient/strip|imageView2/2/w/664/format/webp)

销毁失败

销毁失败。Git友情提醒，feature-vulcan分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用命令git branch -D feature-vulcan。

现在我们强行删除：



![img](https:////upload-images.jianshu.io/upload_images/4889822-d21d7987df68889d?imageMogr2/auto-orient/strip|imageView2/2/w/646/format/webp)

删除成功

**小结：**

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

### 5.6 多人协作

当你从远程库克隆时候，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且远程库的默认名称是origin。

要查看远程库的信息 使用 `git remote`
 要查看远程库的详细信息 使用 `git remote –v`

如下演示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-afc8d880a76cb4c1?imageMogr2/auto-orient/strip|imageView2/2/w/670/format/webp)



#### 5.6.1 推送分支

推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：使用命令 `git push origin master`,如果要推送其他分支，比如dev，就改成： `git push origin dev`

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

- master分支是主分支，因此要时刻与远程同步；
- dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！

比如我现在的github上的readme.txt代码如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-6bf211039b7aa721?imageMogr2/auto-orient/strip|imageView2/2/w/1005/format/webp)

github上的readme.txt代码

本地的readme.txt代码如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-803de4c49bfc96cf?imageMogr2/auto-orient/strip|imageView2/2/w/666/format/webp)

本地的readme.txt代码

现在我想把本地更新的readme.txt代码推送到远程库中，使用命令如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-d27bc277e31b309d?imageMogr2/auto-orient/strip|imageView2/2/w/671/format/webp)



我们可以看到如上，推送成功，我们可以继续来截图github上的readme.txt内容 如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-729bd564436d2701?imageMogr2/auto-orient/strip|imageView2/2/w/990/format/webp)



可以看到 推送成功了。

#### 5.6.2 抓取分支

多人协作时，大家都会往master分支上推送各自的修改。现在我们可以模拟另外一个同事，可以在另一台电脑上（注意要把SSH key添加到github上）或者同一台电脑上另外一个目录克隆，新建一个目录名字叫testgit3

但是我首先要把dev分支也要推送到远程去，如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-db04ae1653d7f48f?imageMogr2/auto-orient/strip|imageView2/2/w/612/format/webp)



接着进入testgit3目录，进行克隆远程的库到本地来，如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-3d1490e6ec47ba5a?imageMogr2/auto-orient/strip|imageView2/2/w/616/format/webp)



现在目录下生成有如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-804407b7aa1ce6c9?imageMogr2/auto-orient/strip|imageView2/2/w/709/format/webp)



现在我们的小伙伴要在dev分支上做开发，就必须创建远程origin的dev分支到本地，于是可以使用命令创建本地dev分支：`git checkout –b dev origin/dev`

现在小伙伴们就可以在dev分支上做开发了，开发完成后把dev分支推送到远程库。

如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-d0e6551ac128b60f?imageMogr2/auto-orient/strip|imageView2/2/w/685/format/webp)



小伙伴们已经向origin/dev分支上推送了提交，而我在我的目录文件下也对同样的文件同个地方作了修改，也试图推送到远程库时，如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-9266f310a0118bbd?imageMogr2/auto-orient/strip|imageView2/2/w/765/format/webp)



推送失败，因为我的小伙伴的最新提交和我试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：



![img](https:////upload-images.jianshu.io/upload_images/4889822-7eca9c4b19a0328b?imageMogr2/auto-orient/strip|imageView2/2/w/697/format/webp)



git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-14de1bb665c161c3?imageMogr2/auto-orient/strip|imageView2/2/w/565/format/webp)

git pull

这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：

我们可以先来看看readme.txt内容。



![img](https:////upload-images.jianshu.io/upload_images/4889822-7f1696e1eaae65fe?imageMogr2/auto-orient/strip|imageView2/2/w/548/format/webp)



现在手动已经解决完了，我接在需要再提交，再push到远程库里面去。如下所示：



![img](https:////upload-images.jianshu.io/upload_images/4889822-c27240ce3fe77f0b?imageMogr2/auto-orient/strip|imageView2/2/w/641/format/webp)

push成功

因此，多人协作的工作模式通常是这样：

首先，可以试图用`git push origin branch-name`推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！

如果`git pull`提示`“no tracking information”`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name。`

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

**小结:**

查看远程库信息，使用`git remote -v`；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；

在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；

从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

## 6. 标签管理

发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。

因为Git的commit号太长，所以要引入tag。所以，tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。

### 6.1 创建标签

在Git中打标签非常简单，首先，切换到需要打标签的分支上，然后打一个新标签，演示如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-6c3f66492b2ab6e5?imageMogr2/auto-orient/strip|imageView2/2/w/521/format/webp)



默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？

方法是找到历史提交的commit id，然后打上就可以了：



![img](https:////upload-images.jianshu.io/upload_images/4889822-aac732e1d75c404e?imageMogr2/auto-orient/strip|imageView2/2/w/598/format/webp)

版本号

比方说要对add merge这次提交打标签，它对应的commit id是5ca7559，敲入命令：$ git  tag v0.9 5ca7559，再用命令git tag查看标签：



![img](https:////upload-images.jianshu.io/upload_images/4889822-8ebfdb3aecbc5816?imageMogr2/auto-orient/strip|imageView2/2/w/641/format/webp)



注意，标签不是按时间顺序列出，而是按字母排序的。可以用`git show <tagname>`查看标签信息：



![img](https:////upload-images.jianshu.io/upload_images/4889822-0f91d60f17e87a59?imageMogr2/auto-orient/strip|imageView2/2/w/545/format/webp)



可以看到，v0.9确实打在add merge这次提交上。

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：





![img](https:////upload-images.jianshu.io/upload_images/4889822-a17d7f5abaabd7cd?imageMogr2/auto-orient/strip|imageView2/2/w/455/format/webp)



 用命令

```
git show <tagname>
```

可以看到说明文字：



![img](https:////upload-images.jianshu.io/upload_images/4889822-b4bf7386bc30534a?imageMogr2/auto-orient/strip|imageView2/2/w/515/format/webp)

用命令git show <tagname>可以看到说明文字：



**小结:**

命令`git tag <name>`用于新建一个标签，默认为HEAD，也可以指定一个commit id；

`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；

`git tag -s <tagname> -m "blablabla..."`可以用PGP签名标签；

命令`git tag`可以查看所有标签。

### 6.2 操作标签

如果标签打错了，也可以删除：



![img](https:////upload-images.jianshu.io/upload_images/4889822-878a839402a7e536?imageMogr2/auto-orient/strip|imageView2/2/w/543/format/webp)



因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令`git push origin <tagname>`：



![img](https:////upload-images.jianshu.io/upload_images/4889822-e8ec6b157943e347?imageMogr2/auto-orient/strip|imageView2/2/w/584/format/webp)

推送标签到远程

或者，一次性推送全部尚未推送到远程的本地标签：



![img](https:////upload-images.jianshu.io/upload_images/4889822-3bd1031afb1b5fe9?imageMogr2/auto-orient/strip|imageView2/2/w/578/format/webp)

全部推送

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除。然后，从远程删除。删除命令也是push，操作如下：



![img](https:////upload-images.jianshu.io/upload_images/4889822-ac2871d7fb7420a6?imageMogr2/auto-orient/strip|imageView2/2/w/635/format/webp)

删除远程标签

**小结：**

命令`git push origin <tagname>`可以推送一个本地标签；

命令`git push origin --tags`可以推送全部未推送过的本地标签；

命令`git tag -d <tagname>`可以删除一个本地标签；

命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

**最终总结：**

**Git基本常用命令如下：**

`mkdir`：         XX (创建一个空目录 XX指目录名)

`pwd`：          显示当前目录的路径。

`git init`         把当前的目录变成可以管理的git仓库，生成隐藏.git文件。

`git add XX`       把xx文件添加到暂存区去。

`git commit –m “XX”`:    提交文件 –m 后面的是注释。

`git status`       查看仓库状态

`git diff XX`     查看XX文件修改了那些内容

`git log`         查看历史记录

`git reset –hard HEAD^` 或者 `git reset –hard HEAD~`回退到上一个版本(如果想回退到100个版本，使用git reset –hard HEAD~100 )

`cat XX`         查看XX文件内容

`git reflog`      查看历史记录的版本号id

`git checkout — XX` 把XX文件在工作区的修改全部撤销。

`git rm XX`          删除XX文件

git remote add origin [https://github.com/tugenhua0707/testgit](https://link.jianshu.com?t=https://github.com/tugenhua0707/testgit) 关联一个远程库

`git push –u`(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库

git clone [https://github.com/tugenhua0707/testgit](https://link.jianshu.com?t=https://github.com/tugenhua0707/testgit)  从远程库中克隆

`git checkout –b dev`  创建dev分支 并切换到dev分支上

`git branch`  查看当前所有的分支

`git checkout master` 切换回master分支

`git merge dev`   在当前的分支上合并dev分支

`git branch –d dev` 删除dev分支

`git branch name` 创建分支

`git stash` 把当前的工作隐藏起来 等以后恢复现场后继续工作

`git stash list`    查看所有被隐藏的文件列表

`git stash apply`     恢复被隐藏的文件，但是内容不删除

`git stash drop`      删除文件

`git stash pop`      恢复文件的同时 也删除文件

`git remote`              查看远程库的信息

`git remote –v`    查看远程库的详细信息

`git push origin master`    Git会把master分支推送到远程库对应的远程分支上

作者：落魂灬

链接：https://www.jianshu.com/p/29b392fba2b9

来源：简书




# 1. 什么是 Git

到目前为止，Git 是世界上使用最为广泛的现代化版本控制系统。Git 最初由 Linux 系统内核的作者 Linus Torvalds 在 2005 年开始开发，目前已经是一个持续维护的成熟开源项目。如今，大量软件项目依赖 Git 进行版本管理，其中既有开源软件，也有商业软件。Git 在很多操作系统和集成开发环境（IDE）上都表现良好。绝大多数软件开发者或多或少都使用过 Git。

Git 是分布式版本管理（DVCS）的一种。CVS 和 Subversion（SVN）等集中式的版本管理软件将完整的版本历史存放在同一个地方。而在 Git 中，每个开发者的代码仓库都包含了所有变更历史。

除了分布式之外，Git 在设计之初也考虑了性能、安全性和灵活性。

##  Git与svn对比

`SVN`

SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话就不行了。

![](F:\course\JAVA_EE\14 Git\zhan-git-note\git-note-img\image-20200702094344172.png)

集中管理方式在一定程度上看到其他开发人员在干什么，而管理员也可以很轻松掌握每个人的开发权限。

但是相较于其优点而言，集中式版本控制工具缺点很明显：

l 服务器单点故障

l 容错性差



`GIT`

Git是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库，这样，工作的时候就不需要联网了，因为版本都是在自己的电脑上。既然每个人的电脑都有一个完整的版本库，那多个人如何协作呢？比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

![](F:\course\JAVA_EE\14 Git\zhan-git-note\git-note-img\8723486263.png)

## git的工作流程

般工作流程如下：

1．从远程仓库中克隆 Git 资源作为本地仓库。

2．从本地仓库中checkout代码然后进行代码修改

3．在提交前先将代码提交到暂存区。

4．提交修改。提交到本地仓库。本地仓库中保存修改的各个历史版本。

5．在修改完成后，需要和团队成员共享代码时，可以将代码push到远程仓库。

![](F:\course\JAVA_EE\14 Git\zhan-git-note\git-note-img\9817293.png)

# 2. Git 简易指南(上)



这节是完全面向入门者的，我假设你从零开始创建一个项目并且想用 Git 来进行版本控制，因此本文会避开分支这些相对复杂的概念。

在这节中，我会介绍如何在你的个人项目中使用 Git，我们会讨论 Git 最基本的操作——如何初始化你的项目，如何管理新的或者已有的文件，如何在远端仓库中储存你的代码。

## 安装 Git

- Mac 用户：Xcode Command Line Tools 自带 Git（`xcode-select --install`）

- Linux 用户：`sudo apt-get install git`

  - Windows 用户：下载 [Git SCM](git-for-windows.github.io)	地址2：https://git-scm.com/download

  ```
  - 对于 Windows 用户，安装后如果希望在全局的 cmd 中使用 Git，需要把 git.exe 加入 PATH 环境变量中，或在 Git Bash 中使用 Git。
  ```

## 检出仓库

执行如下命令以创建一个本地仓库的克隆版本：

`git clone /path/to/repository`

如果是远端服务器上的仓库，你的命令会是这个样子：

`git clone username@host:/path/to/repository` （通过 SSH）

或者：

`git clone https:/path/to/repository.git` （通过 https）

比如说 `git clone https://github.com/geeeeeeeeek/git-recipes.git` 可以将 git 教程 clone 到你指定的目录。

## 创建新仓库

创建新文件夹，打开，然后执行 `git init` 以创建新的 git 仓库。

> 下面每一步中，你都可以通过 `git status` 来查看你的git仓库状态。

## 工作流

你的本地仓库由 Git 维护的三棵「树」组成。第一个是你的 `工作目录`，它持有实际文件；第二个是 `缓存区（Index）`，它像个缓存区域，临时保存你的改动；最后是 `HEAD`，指向你最近一次提交后的结果。

![enter image description here](http://www.bootcss.com/p/git-guide/img/trees.png)

> 事实上，第三个阶段是 commit history 的图。HEAD 一般是指向最新一次 commit 的引用。现在暂时不必究其细节。

## 添加与提交

你可以计划改动（把它们添加到缓存区），使用如下命令：

```
git add < filename >
git add *
```

这是 Git 基本工作流程的第一步。使用如下命令以实际提交改动：

```
git commit -m "代码提交信息"
```

现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库。

> 在开发时，良好的习惯是根据工作进度及时 commit，并务必注意附上有意义的 commit message。创建完项目目录后，第一次提交的 commit message 一般为「Initial commit」。

## 推送改动

你的改动现在已经在本地仓库的 HEAD 中了。执行如下命令以将这些改动提交到远端仓库：

```
git push origin master
```

可以把 master 换成你想要推送的任何分支。

如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：

```
git remote add origin <server>
```

如此你就能够将你的改动推送到所添加的服务器上去了。

> - 这里 origin 是 &lt;server&gt; 的别名，取什么名字都可以，你也可以在 push 时将 &lt;jserver&gt; 替换为 origin。但为了以后 push 方便，我们第一次一般都会先 remote add。
> - 如果你还没有 Git 仓库，可以在 Github 等代码托管平台上创建一个空（不要自动生成 README.md）的仓库，然后将代码 push 到远端仓库。

# 2.1 创建代码仓库

> BY 童仲毅([geeeeeeeeek@github](https://github.com/geeeeeeeeek/git-recipes/))
>
> 这是一篇在[原文(BY atlassian)](https://www.atlassian.com/git/tutorials/setting-up-a-repository)基础上演绎的译文。除非另行注明，页面上所有内容采用知识共享-署名([CC BY 2.5 AU](http://creativecommons.org/licenses/by/2.5/au/deed.zh))协议共享。

这一章简要地带你了解一些最重要的 Git 命令。在这节中，我会向你介绍开始一个新的版本控制项目需要的所有工具，后面的几节包含了你每天都会用到的Git操作。

在这节之后，你应该能够创建一个新的 Git 仓库，缓存你的项目以免丢失，以及查看你项目的历史。

## git init

`git init` 命令创建一个新的 Git 仓库。它用来将已存在但还没有版本控制的项目转换成一个 Git 仓库，或者创建一个空的新仓库。大多数Git命令在未初始化的仓库中都是无法使用的，所以这就是你运行新项目的第一个命令了。

运行 `git init` 命令会在你项目的根目录下创建一个新的 `.git` 目录，其中包含了你项目必需的所有元数据。除了 `.git` 目录之外，已经存在的项目不会被改变（就像 SVN 一样，Git 不强制每个子目录中都有一个 `.git` 目录）。

**用法**

``` shell
git init
```

将当前的目录转换成一个 Git 仓库。它在当前的目录下增加了一个 `.git` 目录，于是就可以开始记录项目版本了。

``` shell
git init <directory>
```

在指定目录创建一个空的 Git 仓库。运行这个命令会创建一个名为 `directory`，只包含 `.git` 子目录的空目录。

``` shell
git init --bare <directory>
```

初始化一个裸的 Git 仓库，但是忽略工作目录。共享的仓库应该总是用 `--bare` 标记创建（见下面的讨论）。一般来说，用 `—bare` 标记初始化的仓库以 `.git` 结尾。比如，一个叫`my-project`的仓库，它的空版本应该保存在 `my-project.git` 目录下。

**讨论**

和 SVN 相比，`git init` 命令是一个创建新的版本控制项目非常简单的途径。Git 不需要你创建仓库，导入文件，检查正在修改的拷贝。你只需要 `cd` 到你的项目目录下，运行 `git init`，你就有了一个功能强大的 Git 仓库。

但是，对大多数项目来说，`git init` 只需要在创建中央仓库时执行一次——开发者通常不会使用 `git init` 来创建他们的本地仓库。他们往往使用 `git clone` 来将已存在的仓库拷贝到他们的机器中去。

**裸仓库**

`-—bare` 标记创建了一个没有工作目录的仓库，这样我们在仓库中更改文件并且提交了。中央仓库应该总是创建成裸仓库，因为向非裸仓库推送分支有可能会覆盖已有的代码变动。将`-—bare`看成是用来将仓库标记为储存设施，而不是一个开发环境。也就是说，对于所有的 Git 工作流，中央仓库是裸仓库，开发者的本地仓库是非裸仓库。

![](https://www.atlassian.com/dam/jcr:88f08a3d-f34e-4c8e-974c-a01f25b2eca1/01.svg)

**栗子**

因为 `git clone` 创建项目的本地拷贝更为方便，`git init` 最常见的使用情景就是用于创建中央仓库：

``` shell
ssh <user>@<host>

cd path/above/repo

git init --bare my-project.git
```

首先，你用SSH连入存放中央仓库的服务器。然后，来到任何你想存放项目的地方，最后，使用 `-—bare` 标记来创建一个中央存储仓库。开发者会将 `my-project.git` 克隆到本地的开发环境中。

## git clone

`git clone` 命令拷贝整个 Git 仓库。这个命令就像 `svn checkout` 一样，除了「工作副本」是一个完备的Git仓库——它包含自己的历史，管理自己的文件，以及环境和原仓库完全隔离。

为了方便起见，`clone` 自动创建了一个名为 `origin` 的远程连接，指向原有仓库。这让和中央仓库之间的交互更加简单。

**用法**

``` shell
git clone <repo>
```

将位于 `<repo>` 的仓库克隆到本地机器。原仓库可以在本地文件系统中，或是通过 HTTP 或 SSH 连接的远程机器。

``` shell
git clone <repo> <directory>
```

将位于 `<repo>` 的仓库克隆到本地机器上的 `<directory>` 目录。

**讨论**

如果项目在远程仓库已经设置完毕，`git clone` 是用户获取开发副本最常见的方式。和  `git init`相似，`clone` 通常也是一次性的操作——只要开发者获得了一份工作副本，所有版本控制操作和协作管理都是在本地仓库中完成的。

**仓库间协作**

这一点很重要，你要理解 Git 中「工作副本」的概念和 SVN 仓库 check out 下来的「工作副本」是很不一样的。和 SVN 不同的是，Git 不会区分工作副本和中央仓库——它们都是功能完备的 Git 仓库。

这就使得 Git 的协作和 SVN 截然不同。SVN 依赖于中央仓库和工作副本之间的关系，而 Git 协作模型是基于仓库和仓库之间的交互的。相对于 SVN 的提交流程，你可以在 Git 仓库之间 `push` 或 `pull` 提交。

![](https://www.atlassian.com/dam/jcr:e5228129-76b1-4b2c-8f10-af789f2ea6c0/03.svg)

![](https://www.atlassian.com/dam/jcr:5d68ce55-59a7-4840-a896-eb2014a9f17b/02.svg)

当然，你也完全可以给予某个特定的仓库一些特殊的含义。比如，指定某个 Git 仓库为中央仓库，你就可以用 Git 进行中央化的工作流。重点是，这是通过约定实现的，而不是写死在版本控制系统本身。

**栗子**

下面这个例子演示用 SSH 用户名 john 连接到 example.com，获取远程服务器上中央仓库的本地副本：

``` shell
git clone ssh://john@example.com/path/to/my-project.git

cd my-project

# 开始工作
```

第一行命令在本地机器的 `my-project` 目录下初始化了一个新的 Git 仓库，并且导入了中央仓库中的文件。接下来，你 `cd` 到项目目录，开始编辑文件、缓存提交、和其它仓库交互。同时注意 `.git` 拓展名克隆时会被去除。它表明了本地副本的非裸状态。

``` shell
git config
```

`git config` 命令允许你在命令行中配置你的 Git 安装（或是一个独立仓库）。这个命令定义了所有配置，从用户信息到仓库行为等等。一些常见的配置命令如下所列。

**用法**

``` shell
git config user.name <name>
```

定义当前仓库所有提交使用的作者姓名。通常来说，你希望使用 `--global` 标记设置当前用户的配置项。

``` sh
git config --global user.name <name>
```

定义当前用户所有提交使用的作者姓名。

``` sh
git config --global user.email <email>
```

定义当前用户所有提交使用的作者邮箱。

``` sh
git config --global alias.<alias-name> <git-command>
```

为Git命令创建一个快捷方式（别名）。

``` sh
git config --system core.editor <editor>
```

定义当前机器所有用户使用命令时用到的文本编辑器，如 `git commit`。`<editor>` 参数用编辑器的启动命令（如 vi）替代。

``` sh
git config --global --edit
```

用文本编辑器打开全局配置文件，手动编辑。

**讨论**

所有配置项都储存在纯文本文件中，所以 `git config` 命令其实只是一个提供便捷的命令行接口。通常，你只需要在新机器上配置一次 Git 安装，以及，你通常会想要使用 `--global` 标记。

Git 将配置项保存在三个单独的文件中，允许你分别对单个仓库、用户和整个系统设置。

- <repo>/.git/config – 特定仓库的设置。


- ~/.gitconfig – 特定用户的设置。这也是 `--global` 标记的设置项存放的位置。


- $(prefix)/etc/gitconfig – 系统层面的设置。

当这些文件中的配置项冲突时，本地仓库设置覆盖用户设置，用户设置覆盖系统设置。如果你打开期中一份文件，你会看到下面这些：

``` sh
[user]

name = John Smith

email = john@example.com

[alias]

st = status

co = checkout

br = branch

up = rebase

ci = commit

[core]

editor = vim
```

你可以用 `git config` 手动编辑这些值。

**栗子**

你在安装 Git 之后想要做的第一件事是告诉它你的名字和邮箱，个性化一些默认设置。一般初始的设置过程看上去是这样的：

``` sh
# 告诉Git你是谁

git config --global user.name "John Smith"

git config --global user.email john@example.com

# 选择你喜欢的文本编辑器

git config --global core.editor vim

# 添加一些快捷方式(别名)

git config --global alias.st status

git config --global alias.co checkout

git config --global alias.br branch

git config --global alias.up rebase

git config --global alias.ci commit
```

它会生成上一节中所说的 `~/.gitconfig` 文件。

# 2.2 保存你的更改



***git add / git commit / git diff / git stash / .gitignore***

“保存”这个概念在 Git 等版本控制系统和 Word 等文本编辑应用中不太一样。传统软件里的“保存”在 Git 里被叫做“提交”（commit）。 我们常说的的保存可以理解成在文件系统中覆盖一个已有的文件或者创建一个新的文件。而在 Git 中，提交这个操作作用于若干个文件和目录。

在 Git 和 SVN 里保存更改也不一样。SVN 提交或检入（check-in）将会推送到远端的中央服务器。也就是说 SVN 的提交需要联网才能完全“保存”项目更改。Git 提交可以在本地完成，然后再使用`git push -u origin master`命令推送到远端服务器。这两种方法的区别体现了两种架构设计的本质区别。Git 是一个分布式的应用，而 SVN 是一个中心化的应用。分布式应用一般来说更可靠，因为它们不存在中央服务器这样的单点故障。

`git add`、`git status`和`git commit`这三个命令通常一起使用，将 Git 项目当前的状态保存成一份快照。

Git 还有另一个保存机制：“储藏”（stash）。储藏是一个临时的储存区域，保存还没准备好提交的更改。储藏操作作用于工作目录，三个文件树中的第一棵。它有很多用法，访问 git stash 页面了解更多。

Git 仓库可以通过设置忽略一些文件或目录。Git 将不会保存这些文件的任何更改。Git 有多种方式管理忽略文件列表。访问 git ignore 页面了解更多 Git 忽略文件设置。

## git add

`git add` 命令将工作目录中的变化添加到暂存区。它告诉 Git 你想要在下一次提交时包含这个文件的更新。但是，`git add` 不会实质上地影响你的仓库——在你运行 `git commit` 前更改都还没有真正被记录。

使用这些命令的同时，你还需要 `git status` 来查看工作目录和暂存区的状态。

### 用法

```
git add <file>
```

将 `<file>` 中的更改加入下次提交的缓存。

```
git add <directory>
```

将 `<directory>` 下的更改加入下次提交的缓存。

```
git add -i
```

开始交互式的缓存，你可以选择文件的一部分加入到下次提交缓存。它会向你展示一堆更改，等待你输入一个命令。`y` 将这块更改加入缓存，`n` 忽略这块更改，`s` 将它分割成更小的块，`e` 手动编辑这块更改，以及 `q` 退出。

### 讨论

`git add` 和 `git commit` 这两个命令组成了最基本的 Git 工作流。每一个 Git 用户都需要理解这两个命令，不管他们团队的协作模型是如何的。我有一千种方式可以将项目版本记录在仓库的历史中。

在一个只有编辑、缓存、提交这样基本流程的项目上开发。首先，你要在工作目录中编辑你的文件。当你准备备份项目的当前状态时，你通过 `git add` 来缓存更改。当你对缓存的快照满意之后，你通过 `git commit` 将它提交到你的项目历史中去。

![Git Tutorial: git add Snapshot](https://wac-cdn.atlassian.com/dam/jcr:0f27e004-f2f5-4890-921d-65fa77ba2774/01.svg)

`git add` 命令不能和 `svn add` 混在一起理解，后者将文件添加到仓库中。而 `git add` 发生于更抽象的 *更改* 层面。也就是说，`git add` 在每次你修改一个文件时都需要被调用，而 `svn add` 只需要每个文件调用一次。这听上去很多余，但这样的工作流使得一个项目更容易组织。

#### 缓存区

缓存区是 Git 更为独特的地方之一，如果你是从 SVN（甚至是 Mercurial）迁移而来，那你可得花点时间理解了。你可以简单地把它想成是工作目录和项目历史之间的缓冲区。

缓存允许你在实际提交到项目历史之前，将相关的更改组合成一份高度专注的快照，而不是将你上次提交以后产生的所有更改一并提交。也就是说你可以更改各种不相关的文件，然后回过去将它们按逻辑切分，将相关的更改添加到缓存，一份一份提交。在任何修改控制系统中，很重要的一点是提交必须是原子性的，以便于追踪 bug，并用最小的代价回滚更改。

### 栗子

当你开始新项目的时候，`git add` 和 `svn import` 类似。为了创建当前目录的初始提交，使用下面两个命令：

```
git add .
git commit
```

当你项目设置好之后，新的文件可以通过路径传递给 `git add` 来添加：

```
git add hello.py
git commit
```

上面的命令同样可以用于记录已有文件的更改。重复一次，Git 不会区分缓存的更改来自新文件，还是仓库中已有的文件。

## git commit

`git commit`命令将缓存的快照提交到项目历史。提交的快照可以认为是项目安全的版本，Git 永远不会改变它们，除非你这么要求。和 `git add` 一样，这是最重要的 Git 命令之一。

尽管和它和 `svn commit` 名字一样，但实际上它们毫无关联。快照被提交到本地仓库，不会和其他 Git 仓库有任何交互。

### 用法

```
git commit
```

提交已经缓存的快照。它会运行文本编辑器，等待你输入提交信息。当你输入信息之后，保存文件，关闭编辑器，创建实际的提交。

```
git commit -m "<message>"
```

提交已经缓存的快照。但将 `<message>` 作为提交信息，而不是运行文本编辑器。

```
git commit -a
```

提交一份包含工作目录所有更改的快照。它只包含跟踪过的文件的更改（那些之前已经通过 `git add` 添加过的文件）。

### 讨论

快照总是提交到 *本地* 仓库。这一点和 SVN 截然不同，后者的工作拷贝提交到中央仓库。而 Git 不会强制你和中央仓库进行交互，直到你准备好了。就像缓存区是工作目录和项目历史之间的缓冲地带，每个开发者的本地仓库是他们贡献的代码和中央仓库之间的缓冲地带。

这一点改变了 Git 用户基本的开发模型。Git 开发者可以在本地仓库中积累一些提交，而不是一发生更改就直接提交到中央仓库。这对于 SVN 风格的协作有着诸多优点：更容易将功能切分成原子性的提交，让相关的提交组合在一起，发布到中央仓库之前整理好本地的历史。开发者得以在一个隔离的环境中工作，直到他们方便的时候再整合代码。

#### 记录快照，而不是记录差异

SVN 和 Git 除了使用上存在巨大差异，它们底层的实现同样遵循截然不同的设计哲学。SVN 追踪文件的 *变化* ，而 Git 的版本控制模型基于 *快照* 。比如说，一个 SVN 提交由仓库中原文件相比的差异（diff）组成。而 Git 在每次提交中记录文件的 *完整内容* 。

![Git Tutorial: Snapshots, Not Differences](https://www.atlassian.com/dam/jcr:7406fe56-d36d-44cf-92e3-b28e4bae36f8/02.svg)

这让很多 Git 操作比 SVN 来的快得多，因为文件的某个版本不需要通过版本间的差异组装得到——每个文件完整的修改能立刻从 Git 的内部数据库中得到。

Git 的快照模型对它版本控制模型的方方面面都有着深远的影响，从分支到合并工具，再到协作工作流，以至于影响了所有特性。

### 栗子

下面这个栗子假设你编辑了 `hello.py` 文件的一些内容，并且准备好将它提交到项目历史。首先，你需要用 `git add` 缓存文件，然后提交缓存的快照。

```
git add hello.py
git commit
```

它会打开一个文件编辑器（可以通过 `git config` 设置) 询问提交信息，同时列出将被提交的文件。

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
# (use "git reset HEAD <file>..." to unstage)
#
#modified: hello.py
```

Git 对提交信息没有特定的格式限制，但约定俗成的格式是：在第一行用 50 个以内的字符总结这个提交，留一空行，然后详细阐述具体的更改。比如：

```
Change the message displayed by hello.py

- Update the sayHello() function to output the user's name
- Change the sayGoodbye() function to a friendlier message
```

注意，很多开发者倾向于在提交信息中使用一般现在时态。这样看起来更像是对仓库进行的操作，让很多改写历史的操作更加符合直觉。

# 2.3 检查仓库状态

## git status

`git status` 命令显示工作目录和缓存区的状态。你可以看到哪些更改被缓存了，哪些还没有，以及哪些还未被 Git 追踪。status 的输出 *不会* 告诉你任何已提交到项目历史的信息。如果你想看的话，应该使用 `git log` 命令。

### 用法

```
git status
```

列出已缓存、未缓存、未追踪的文件。

### 讨论

`git status` 是一个相对简单的命令。 它告诉你 `git add` 和 `git commit` 的进展。status 信息还包括了添加缓存和移除缓存的相关指令。样例输出显示了三类主要的 `git status` 输出：

```
# On branch master
# Changes to be committed:
# (use "git reset HEAD <file>..." to unstage)
#
#modified: hello.py
#
# Changes not staged for commit:
# (use "git add <file>..." to update what will be committed)
# (use "git checkout -- <file>..." to discard changes in working directory)
#
#modified: main.py
#
# Untracked files:
# (use "git add <file>..." to include in what will be committed)
#
#hello.pyc
```

#### 忽略文件

未追踪的文件通常有两类。它们要么是项目新增但还未提交的文件，要么是像 `.pyc`、`.obj`、`.exe` 等编译后的二进制文件。显然前者应该出现在 `git status` 的输出中，而后者会让我们困惑究竟发生了什么。

因此，Git 允许你完全忽略这些文件，只需要将路径放在一个特定的 `.gitignore` 文件中。所有想要忽略的文件应该分别写在单独一行，`*` 字符用作通配符。比如，将下面这行加入项目根目录的`.gitignore`文件可以避免编译后的Python模块出现在`git status`中：

```
*.pyc
```

### 栗子

在提交更改前检查仓库状态是一个良好的实践，这样你就不会不小心提交什么奇怪的东西。这个例子显示了缓存和提交快照前后的仓库状态：

```
# Edit hello.py
git status
# hello.py is listed under "Changes not staged for commit"
git add hello.py
git status
# hello.py is listed under "Changes to be committed"
git commit
git status
# nothing to commit (working directory clean)
```

第一个 status 的输出显示文件还未缓存。`git add` 操作会影响第二个 `git status`，最后的 status 输出告诉你已经没有可以提交的东西了——工作目录和最近的提交一致。一些 Git 命令（比如 `git merge`）需要工作目录整洁，以免意外覆盖更改。

## git log

`git log` 命令显示已提交的快照。你可以列出项目历史，筛选，以及搜索特定更改。`git status` 允许你查看工作目录和缓存区，而 `git log` 只作用于提交的项目历史。

![Git Tutorial: git status vs. git log](https://wac-cdn.atlassian.com/dam/jcr:52d530ce-7f51-48e3-920b-a18f776048d3/01.svg)

log 输出可以有很多种自定义的方式，从简单地筛选提交，到用完全自定义的格式显示。其中一些最常用的 `git log` 配置如下所示。

### 用法

```
git log
```

使用默认格式显示完整地项目历史。如果输出超过一屏，你可以用 `空格键` 来滚动，按 `q` 退出。

```
git log -n <limit>
```

用 `<limit>` 限制提交的数量。比如 `git log -n 3` 只会显示 3 个提交。

```
git log --oneline
```

将每个提交压缩到一行。当你需要查看项目历史的上层情况时这会很有用。

```
git log --stat
```

除了 `git log` 信息之外，包含哪些文件被更改了，以及每个文件相对的增删行数。

```
git log -p
```

显示代表每个提交的一堆信息。显示每个提交全部的差异（diff），这也是项目历史中最详细的视图。

```
git log --author="<pattern>"
```

搜索特定作者的提交。`<pattern>` 可以是字符串或正则表达式。

```
git log --grep="<pattern>"
```

搜索提交信息匹配特定 `<pattern>` 的提交。`<pattern>` 可以是字符串或正则表达式。

```
git log <since>..<until>
```

只显示发生在 `<since>` 和 `<until>` 之间的提交。两个参数可以是提交 ID、分支名、`HEAD` 或是任何一种引用。

```
git log <file>
```

只显示包含特定文件的提交。查找特定文件的历史这样做会很方便。

```
git log --graph --decorate --oneline
```

还有一些有用的选项。`--graph` 标记会绘制一幅字符组成的图形，左边是提交，右边是提交信息。`--decorate` 标记会加上提交所在的分支名称和标签。`--oneline` 标记将提交信息显示在同一行，一目了然。

### 讨论

`git log` 命令是 Git 查看项目历史的基本工具。当你要寻找项目特定的一个版本或者弄明白合并功能分支时引入了哪些变化，你就会用到这个命令。

```
commit 3157ee3718e180a9476bf2e5cab8e3f1e78a73b7
Author: John Smith
```

大多数时候都很简单直接。但是，第一行需要解释下。`commit` 后面 40 个字的字符串是提交内容的 SHA-1 校验总和（checksum）。它有两个作用。一是保证提交的正确性——如果它被损坏了，提交会生成一个不同的校验总和。第二，它是提交唯一的标识 ID。

这个 ID 可以用于 `git log` 这样的命令中来引用具体的提交。比如，`git log 3157e..5ab91` 会显示所有ID在 `3157e` 和 `5ab91` 之间的提交。除了校验总和之外，分支名、HEAD 关键字也是常用的引用提交的方法。`HEAD` 总是指向当前的提交，无论是分支还是特定提交也好。

~字符用于表示提交的父节点的相对引用。比如，`3157e~1` 指向 `3157e` 前一个提交,`HEAD~3` 是当前提交的回溯3个节点的提交。

所有这些标识方法的背后都是为了让你对特定提交进行操作。`git log` 命令一般是这些交互的起点，因为它让你找到你想要的提交。

### 栗子

*用法* 一节提供了 `git log` 很多的栗子，但请记住，你可以将很多选项用在同一个命令中：

```
git log --author="John Smith" -p hello.py
```

这个命令会显示 `John Smith` 作者对 `hello.py` 文件所做的所有更改的差异比较（diff）。

..句法是比较分支很有用的工具。下面的栗子显示了在 `some-feature` 分支而不在 `master` 分支的所有提交的概览。

```
git log --oneline master..some-feature
```

> 这篇文章是[**「git-recipes」**](https://github.com/geeeeeeeeek/git-recipes/)的一部分，点击 [**目录**](https://github.com/geeeeeeeeek/git-recipes/wiki/) 查看所有章节。
>
> 如果你觉得文章对你有帮助，欢迎点击右上角的 **Star** :star2: 或 **Fork** :fork_and_knife:。
>
> 如果你发现了错误，或是想要加入协作，请参阅 [Wiki 协作说明](https://github.com/geeeeeeeeek/git-recipes/issues/1)。

# 2.4 检出之前的提交

`git checkout` 这个命令有三个不同的作用：检出文件、检出提交和检出分支。在这一章中，我们只关心前两种用法。

检出提交会使工作目录和这个提交完全匹配。你可以用它来查看项目之前的状态，而不改变当前的状态。检出文件使你能够查看某个特定文件的旧版本，而工作目录中剩下的文件不变。

### 用法

```
git checkout master
```

回到 master 分支。分支会在下一节中讲到，而现在，你只需要将它视为回到项目「当前」状态的一种方式。

```
git checkout <commit> <file>
```

查看文件之前的版本。它将工作目录中的 `<file>` 文件变成 `<commit>` 中那个文件的拷贝，并将它加入缓存区。

```
git checkout <commit>
```

更新工作目录中的所有文件，使得和某个特定提交中的文件一致。你可以将提交的哈希字串，或是标签作为 `<commit>` 参数。这会使你处在分离 HEAD 的状态。

### 讨论

版本控制系统背后的思想就是「安全」地储存项目的拷贝，这样你永远不用担心什么时候不可复原地破坏了你的代码库。当你建立了项目历史之后，`git checkout` 是一种便捷的方式，来将保存的快照「加载」到你的开发机器上去。

检出之前的提交是一个只读操作。在查看旧版本的时候绝不会损坏你的仓库。你项目「当前」的状态在	`master` 上不会变化。在开发的正常阶段，`HEAD` 一般指向 master 或是其他的本地分支，但当你检出之前提交的时候，`HEAD` 就不再指向一个分支了——它直接指向一个提交。这被称为「分离 `HEAD`」状态 ，可以用下图可视化：

![Git Tutorial: Checking out a previous commit](https://www.atlassian.com/git/images/tutorials/getting-started/viewing-old-commits/01.svg)

在另一方面，检出旧文件不影响你仓库的当前状态。你可以在新的快照中像其他文件一样重新提交旧版本。所以，在效果上，`git checkout` 的这个用法可以用来将单个文件回滚到旧版本 。

![Git Training: Checking out a previous version of a file](https://www.atlassian.com/git/images/tutorials/getting-started/viewing-old-commits/02.svg)

### 栗子

#### 查看之前的版本

这个栗子假定你开始了一个疯狂的实验，但你不确定你是否想要保留它。为了帮助你决定，你想看一看你开始实验之前的项目状态。首先，你需要找到你想要看的那个版本的 ID。

```
git log --oneline
```

假设你的项目历史看上去和下面一样：

```
b7119f2 继续做些丧心病狂的事
872fa7e 做些丧心病狂的事
a1e8fb5 对 hello.py 做了一些修改
435b61d 创建 hello.py
9773e52 初始导入
```

你可以这样使用 `git checkout` 来查看「对 hello.py 做了一些修改」这个提交：

```
git checkout a1e8fb5
```

这让你的工作目录和 `a1e8fb5` 提交所处的状态完全一致。你可以查看文件，编译项目，运行测试，甚至编辑文件而不需要考虑是否会影响项目的当前状态。你所做的一切 *都不会* 被保存到仓库中。为了继续开发，你需要回到你项目的「当前」状态：

```
git checkout master
```

这里假定了你默认在 master 分支上开发，我们会在以后的分支模型中详细讨论。

一旦你回到 master 分支之后，你可以使用 `git revert` 或 `git reset` 来回滚任何不想要的更改。

#### 检出文件

如果你只对某个文件感兴趣，你也可以用 `git checkout` 来获取它的一个旧版本。比如说，如果你只想从之前的提交中查看 `hello.py` 文件，你可以使用下面的命令：

```
git checkout a1e8fb5 hello.py
```

记住，和检出提交不同，这里 *确实* 会影响你项目的当前状态。旧的文件版本会显示为「需要提交的更改」，允许你回滚到文件之前的版本。如果你不想保留旧的版本，你可以用下面的命令检出到最近的版本：

```
git checkout HEAD hello.py
```

# 2.5 回滚错误的修改

这章教程提供了和项目旧版本打交道所需要的所有技巧。首先，你会知道如何浏览旧的提交，然后了解回滚项目历史中的公有提交和回滚本地机器上的私有更改之间的区别。

## git checkout

见上一章[「2.5 检出之前的提交」](https://github.com/geeeeeeeeek/git-recipes/wiki/2.5-%E6%A3%80%E5%87%BA%E4%B9%8B%E5%89%8D%E7%9A%84%E6%8F%90%E4%BA%A4)。

## git revert

`git revert` 命令用来撤销一个已经提交的快照。但是，它是通过搞清楚如何撤销这个提交引入的更改，然后在最后加上一个撤销了更改的 *新* 提交，而不是从项目历史中移除这个提交。这避免了Git丢失项目历史，这一点对于你的版本历史和协作的可靠性来说是很重要的。

![Git Tutorial: git revert](https://wac-cdn.atlassian.com/dam/jcr:b6fcf82b-5b15-4569-8f4f-a76454f9ca5b/03%20(7).svg)

### 用法

```
git revert <commit>
```

生成一个撤消了 `<commit>` 引入的修改的新提交，然后应用到当前分支。

### 讨论

撤销（revert）应该用在你想要在项目历史中移除一整个提交的时候。比如说，你在追踪一个 bug，然后你发现它是由一个提交造成的，这时候撤销就很有用。与其说自己去修复它，然后提交一个新的快照，不如用 `git revert`，它帮你做了所有的事情。

#### 撤销（revert）和重设（reset）对比

理解这一点很重要。`git revert` 回滚了「单独一个提交」，它没有移除后面的提交，然后回到项目之前的状态。在 Git 中，后者实际上被称为 `reset`，而不是 `revert`。

![Git Tutorial: Revert vs Reset](https://wac-cdn.atlassian.com/dam/jcr:a6a50d78-48e3-4765-8492-9e48dec8fd2f/04%20(2).svg)

撤销和重设相比有两个重要的优点。首先，它不会改变项目历史，对那些已经发布到共享仓库的提交来说这是一个安全的操作。至于为什么改变共享的历史是危险的，请参阅 `git reset` 一节。

其次，`git revert` 可以针对历史中任何一个提交，而 `git reset` 只能从当前提交向前回溯。比如，你想用 `git reset` 重设一个旧的提交，你不得不移除那个提交后的所有提交，再移除那个提交，然后重新提交后面的所有提交。不用说，这并不是一个优雅的回滚方案。

### 栗子

下面的这个栗子是 `git revert` 一个简单的演示。它提交了一个快照，然后立即撤销这个操作。

```
# 编辑一些跟踪的文件

# 提交一份快照
git commit -m "Make some changes that will be undone"

# 撤销刚刚的提交
git revert HEAD
```

这个操作可以用下图可视化：

![Git Tutorial: git revert Example](https://www.atlassian.com/git/images/tutorials/getting-started/undoing-changes/05.svg)

注意第四个提交在撤销后依然在项目历史中。`git revert` 在后面增加了一个提交来撤销修改，而不是删除它。 因此，第三和第五个提交表示同样的代码，而第四个提交依然在历史中，以备以后我们想要回到这个提交。

## git reset

如果说 `git revert` 是一个撤销更改安全的方式，你可以将 `git reset` 看做一个 *危险* 的方式。当你用 `git reset` 来重设更改时(提交不再被任何引用或引用日志所引用)，我们无法获得原来的样子——这个撤销是永远的。使用这个工具的时候务必要小心，因为这是少数几个可能会造成工作丢失的命令之一。

和 `git checkout` 一样，`git reset` 有很多种用法。它可以被用来移除提交快照，尽管它通常被用来撤销缓存区和工作目录的修改。不管是哪种情况，它应该只被用于 *本地* 修改——你永远不应该重设和其他开发者共享的快照。

**用法**

```
git reset <file>
```

从缓存区移除特定文件，但不改变工作目录。它会取消这个文件的缓存，而不覆盖任何更改。

```
git reset
```

重设缓冲区，匹配最近的一次提交，但工作目录不变。它会取消 *所有* 文件的缓存，而不会覆盖任何修改，给你了一个重设缓存快照的机会。

```
git reset --hard
```

重设缓冲区和工作目录，匹配最近的一次提交。除了取消缓存之外，`--hard` 标记告诉 Git 还要重写所有工作目录中的更改。换句话说：它清除了所有未提交的更改，所以在使用前确定你想扔掉你所有本地的开发。

```
git reset <commit>
```

将当前分支的末端移到 `<commit>`，将缓存区重设到这个提交，但不改变工作目录。所有 `<commit>` 之后的更改会保留在工作目录中，这允许你用更干净、原子性的快照重新提交项目历史。

```
git reset --hard <commit>
```

将当前分支的末端移到 `<commit>`，将缓存区和工作目录都重设到这个提交。它不仅清除了未提交的更改，同时还清除了 `<commit>` 之后的所有提交。

**讨论**

上面所有的调用都是用来移除仓库中的修改。没有 `--hard` 标记时 `git reset` 通过取消缓存或取消一系列的提交，然后重新构建提交来清理仓库。而加上 `--hard` 标记对于作了大死之后想要重头再来尤其方便。

撤销(revert)被设计为撤销 *公开* 的提交的安全方式，`git reset`被设计为重设 *本地* 更改。因为两个命令的目的不同，它们的实现也不一样：重设完全地移除了一堆更改，而撤销保留了原来的更改，用一个新的提交来实现撤销。

![Git Tutorial: Revert vs Reset](https://www.atlassian.com/git/images/tutorials/getting-started/undoing-changes/06.svg)

**不要重设公共历史**

当有 `<commit>` 之后的提交被推送到公共仓库后，你绝不应该使用 `git reset`。发布一个提交之后，你必须假设其他开发者会依赖于它。

移除一个其他团队成员在上面继续开发的提交在协作时会引发严重的问题。当他们试着和你的仓库同步时，他们会发现项目历史的一部分突然消失了。下面的序列展示了如果你尝试重设公共提交时会发生什么。`origin/master` 是你本地 `master` 分支对应的中央仓库中的分支。

![Git Tutorial: Resetting an Public Commit](https://wac-cdn.atlassian.com/dam/jcr:b616f03d-5257-4ea8-a6eb-db1a0207a78a/07%20(1).svg)

一旦你在重设之后又增加了新的提交，Git 会认为你的本地历史已经和 `origin/master` 分叉了，同步你的仓库时的合并提交（merge commit）会使你的同事困惑。

重点是，确保你只对本地的修改使用 `git reset`，而不是公共更改。如果你需要修复一个公共提交，`git revert` 命令正是被设计来做这个的。

**栗子**

**取消文件缓存**

`git reset` 命令在准备缓存快照时经常被用到。下面的例子假设你有两个文件，`hello.py` 和 `main.py`它们已经被加入了仓库中。

```
# 编辑了hello.py和main.py

# 缓存了目录下所有文件
git add .

# 意识到hello.py和main.py中的修改
# 应该在不同的快照中提交

# 取消main.py缓存
git reset main.py

# 只提交hello.py
git commit -m "Make some changes to hello.py"

# 在另一份快照中提交main.py
git add main.py
git commit -m "Edit main.py"
```

如你所见，`git reset` 帮助你取消和这次提交无关的修改，让提交能够专注于某一特定的范围。

**移除本地修改**

下面的这个栗子显示了一个更高端的用法。它展示了你作了大死之后应该如何扔掉那几个更新。

```
# 创建一个叫`foo.py`的新文件，增加代码

# 提交到项目历史
git add foo.py
git commit -m "Start developing a crazy feature"

# 再次编辑`foo.py`，修改其他文件

# 提交另一份快照
git commit -a -m "Continue my crazy feature"

# 决定废弃这个功能，并删除相关的更改
git reset --hard HEAD~2
```

`git reset HEAD~2` 命令将当前分支向前倒退两个提交，相当于在项目历史中移除刚创建的这两个提交。记住，这种重设只能用在 *非公开* 的提交中。绝不要在将提交推送到共享仓库之后执行上面的操作。

## git clean

`git clean` 命令将未跟踪的文件从你的工作目录中移除。它只是提供了一条捷径，因为用 `git status` 查看哪些文件还未跟踪然后手动移除它们也很方便。和一般的 `rm` 命令一样，`git clean` 是无法撤消的，所以在删除未跟踪的文件之前想清楚，你是否真的要这么做。

`git clean` 命令经常和 `git reset --hard` 一起使用。记住，reset 只影响被跟踪的文件，所以还需要一个单独的命令来清理未被跟踪的文件。这个两个命令相结合，你就可以将工作目录回到之前特定提交时的状态。

**用法**

```
git clean -n
```

执行一次git clean的『演习』。它会告诉你那些文件在命令执行后会被移除，而不是真的删除它。

```
git clean -f
```

移除当前目录下未被跟踪的文件。`-f`（强制）标记是必需的，除非 `clean.requireForce` 配置项被设为了 `false`（默认为 `true`）。它 *不会* 删除 `.gitignore` 中指定的未跟踪的文件。

```
git clean -f <path>
```

移除未跟踪的文件，但限制在某个路径下。

```
git clean -df
```

移除未跟踪的文件，以及目录。

```
git clean -xf
```

移除当前目录下未跟踪的文件，以及 Git 一般忽略的文件。

**讨论**

如果你在本地仓库中作死之后想要毁尸灭迹，`git reset --hard` 和 `git clean -f` 是你最好的选择。运行这两个命令使工作目录和最近的提交相匹配，让你在干净的状态下继续工作。

`git clean` 命令对于 build 后清理工作目录十分有用。比如，它可以轻易地删除 C 编译器生成的 `.o` 和 `.exe` 二进制文件。这通常是打包发布前需要的一步。`-x` 命令在这种情况下特别方便。

请牢记，和 `git reset` 一样， `git clean` 是仅有的几个可以永久删除提交的命令之一，所以要小心使用。事实上，它太容易丢掉重要的修改了，以至于 Git 厂商 *强制* 你用 `-f` 标志来进行最基本的操作。这可以避免你用一个 `git clean` 就不小心删除了所有东西。

**栗子**

下面的栗子清除了工作目录中的所有更改，包括新建还没加入缓存的文件。它假设你已经提交了一些快照，准备开始一些新的实验。

```
# 编辑了一些文件
# 新增了一些文件
# 『糟糕』

# 将跟踪的文件回滚回去
git reset --hard

# 移除未跟踪的文件
git clean -df
```

在执行了 reset/clean 的流程之后，工作目录和缓存区和最近一次提交看上去一模一样，而  `git status`会认为这是一个干净的工作目录。你可以重新来过了。

注意，不像 `git reset` 的第二个栗子，新的文件没有被加入到仓库中。因此，它们不会受到 `git reset --hard` 的影响，需要 `git clean` 来删除它们。

# 2.6 重写项目历史

Git 的主要职责是保证你不会丢失提交的修改。但是，它同样被设计成让你完全掌控开发工作流。这包括了让你自定义你的项目历史，而这也创造了丢失提交的可能性。Git 提供了可以重写项目历史的命令，但也警告你这些命令可能会让你丢失内容。

这份教程讨论了重写提交快照的一些常见原因，并告诉你如何避免不好的影响。

## git commit --amend

`git commit --amend` 命令是修复最新提交的便捷方式。它允许你将缓存的修改和之前的提交合并到一起，而不是提交一个全新的快照。它还可以用来简单地编辑上一次提交的信息而不改变快照。

![Git Tutorial: git commit --amend](https://wac-cdn.atlassian.com/dam/jcr:a4de784b-3572-4d23-8c68-cea9ad4f205f/01.svg)

但是，amend 不只是修改了最新的提交——它进行了一次替换。对于 Git 来说，这看上去像一个全新的提交，即上图中用星号表示的那一个。在公共仓库工作时一定要牢记这一点。

**用法**

```
git commit --amend
```

合并缓存的修改和上一次的提交，用新的快照替换上一个提交。缓存区没有文件时运行这个命令可以用来编辑上次提交的提交信息，而不会更改快照。

**讨论**

仓促的提交在你日常开发过程中时常会发生。很容易就忘记了缓存一个文件或者弄错了提交信息的格式。`--amend` 标记是修复这些小意外的便捷方式。

**不要修复公共提交**

在[`git reset`](https://github.com/geeeeeeeeek/git-recipes/wiki/2.6-%E5%9B%9E%E6%BB%9A%E9%94%99%E8%AF%AF%E7%9A%84%E4%BF%AE%E6%94%B9#git-reset)这节中，我们说过永远不要重设和其他开发者共享的提交。对于修复也是一样：永远不要修复一个已经推送到公共仓库中的提交。

修复过的提交事实上是全新的提交，之前的提交会被移除出项目历史。这和重设公共快照的后果是一样的。如果你修复了其他开发者在之后继续开发的一个提交，看上去他们的工作基础从项目历史中消失了一样。对于在这上面的开发者来说这是很困惑的，而且很难恢复。

**栗子**

下面这个🌰展示了 Git 开发工作流中的一个常见情形。我们编辑了一些希望在同一个快照中提交的文件，但我们忘记添加了其中的一个。修复错误只需要缓存那个文件并且用 `--amend` 标记提交：

```
# 编辑 hello.py 和 main.py
git add hello.py
git commit

# 意识到你忘记添加 main.py 的更改
git add main.py
git commit --amend --no-edit
```

编辑器会弹出上一次提交的信息，加入 `--no-edit` 标记会修复提交但不修改提交信息。需要的话你可以修改，不然的话就像往常一样保存并关闭文件。完整的提交会替换之前不完整的提交，看上去就像我们在同一个快照中提交了 `hello.py` 和 `main.py`。

## git rebase

变基（rebase, 事实上这个名字十分诡异, 所以在大多数时候直接用英文术语）是将分支移到一个新的基提交的过程。过程一般如下所示：

![Git Tutorial: Rebase to maintain a linear project history.](https://wac-cdn.atlassian.com/dam/jcr:e4a40899-636b-4988-9774-eaa8a440575b/02.svg)

从内容的角度来看，rebase 只不过是将分支从一个提交移到了另一个。但从内部机制来看，Git 是通过在选定的基上创建新提交来完成这件事的——它事实上重写了你的项目历史。理解这一点很重要，尽管分支看上去是一样的，但它包含了全新的提交。

**用法**

```
git rebase <base>
```

将当前分支 rebase 到 `<base>`，这里可以是任何类型的提交引用（ID、分支名、标签，或是 `HEAD` 的相对引用）。

**讨论**

rebase 的主要目的是为了保持一个线性的项目历史。比如说，当你在 feature 分支工作时 master 分支取得了一些进展：

![Git Rebase Branch onto Master](https://wac-cdn.atlassian.com/dam/jcr:d3b2abde-d06a-47b6-8955-5f3ef34e0237/03.svg)

要将你的 feature 分支整合进 `master` 分支，你有两个选择：直接 merge，或者先 rebase 后 merge。前者会产生一个三路合并（3-way merge）和一个合并提交，而后者产生的是一个快速向前的合并以及完美的线性历史。下图展示了为什么 rebase 到 `master` 分支会促成一个快速向前的合并。

![Git Tutorial: Fast-forward merge](https://www.atlassian.com/git/images/tutorials/getting-started/rewriting-history/04.svg)

rebase 是将上游更改合并进本地仓库的通常方法。你每次想查看上游进展时，用 `git merge` 拉取上游更新会导致一个多余的合并提交。在另一方面，rebase 就好像是说「我想将我的更改建立在其他人的进展之上」。

**不要 rebase 公共历史**

和我们讨论过的 `git commit --amend` 和 `git reset` 一样，你永远不应该 rebase 那些已经推送到公共仓库的提交。rebase 会用新的提交替换旧的提交，你的项目历史会像突然消失了一样。

**栗子**

下面这个🌰同时使用 git rebase 和 git merge 来保持线性的项目历史。这是一个确认你的合并都是快速向前的方法。

```
# 开始新的功能分支
git checkout -b new-feature master
# 编辑文件
git commit -a -m "Start developing a feature"
```

在 feature 分支开发了一半的时候，我们意识到项目中有一个安全漏洞:

```
# 基于master分支创建一个快速修复分支
git checkout -b hotfix master
# 编辑文件
git commit -a -m "Fix security hole"
# 合并回master
git checkout master
git merge hotfix
git branch -d hotfix
```

将 hotfix 分支并回之后 master，我们有了一个分叉的项目历史。我们用 rebase 整合 feature 分支以获得线性的历史，而不是使用普通的 git merge。

```
git checkout new-feature
git rebase master
```

它将 new-feature 分支移到了 master 分支的末端，现在我们可以在 master 上进行标准的快速向前合并了:

```
git checkout master
git merge new-feature
```

## git rebase -i

用 `-i` 标记运行 `git rebase` 开始交互式 rebase。交互式 rebase 给你在过程中修改单个提交的机会，而不是盲目地将所有提交都移到新的基上。你可以移除、分割提交，更改提交的顺序。它就像是打了鸡血的 `git commit --amend` 一样。

**用法**

```
git rebase -i <base>
```

将当前分支 rebase 到 `base`，但使用可交互的形式。它会打开一个编辑器，你可以为每个将要 rebase 的提交输入命令（见后文）。这些命令决定了每个提交将会怎样被转移到新的基上去。你还可以对这些提交进行排序。

**讨论**

交互式 rebase 给你了控制项目历史的完全掌控。它给了开发人员很大的自由，因为他们可以提交一个「混乱」的历史而只需专注于写代码，然后回去恢复干净。

大多数开发者喜欢在并入主代码库之前用交互式 rebase 来完善他们的 feature 分支。他们可以将不重要的提交合在一起，删除不需要的，确保所有东西在提交到「正式」的项目历史前都是整齐的。对其他人来说，这个功能的开发看上去是由一系列精心安排的提交组成的。

**栗子**

下面这个🌰是 `非交互式rebase` 一节中🌰的可交互升级版本。

```
# 开始新的功能分支
git checkout -b new-feature master
# 编辑文件
git commit -a -m "Start developing a feature"
# 编辑更多文件
git commit -a -m "Fix something from the previous commit"

# 直接在 master 上添加文件
git checkout master
# 编辑文件
git commit -a -m "Fix security hole"

# 开始交互式 rebase
git checkout new-feature
git rebase -i master
```

最后的那个命令会打开一个编辑器，包含 new-feature 的两个提交，和一些指示：

```
pick 32618c4 Start developing a feature
pick 62eed47 Fix something from the previous commit
```

你可以更改每个提交前的 pick 命令来决定在 rebase 时提交移动的方式。在我们的例子中，我们只需要用 squash 命令把两个提交并在一起就可以了：

```
pick 32618c4 Start developing a feature
squash 62eed47 Fix something from the previous commit
```

保存并关闭编辑器以开始 rebase。另一个编辑器会打开，询问你合并后的快照的提交信息。在定义了提交信息之后，rebase 就完成了，你可以在 `git log` 输出中看到那个提交。整个过程可以用下图可视化：

![Git Tutorial: git rebase -i example](https://www.atlassian.com/git/images/tutorials/getting-started/rewriting-history/05.svg)

注意缩并的提交和原来的两个提交的 ID 都不一样，告诉我们这确实是个新的提交。

最后，你可以执行一个快速向前的合并，来将完善的 feature 分支整合进主代码库：

```
git checkout master
git merge new-feature
```

交互式 rebase 强大的能力可以从整合后的 master 分支看出——额外的 `62eed47` 提交找不到了。对其他人来说，你就像是一个天才，用完美数量的提交完成了 `new-feature`。这就是交互式提交如何保持项目历史干净和合意。

## git reflog

Git 用引用日志这种机制来记录分支顶端的更新。它允许你回到那些不被任何分支或标签引用的更改。在重写历史后，引用日志包含了分支旧状态的信息，有需要的话你可以回到这个状态。

**用法**

```
git reflog
```

显示本地仓库的引用日志。

```
git reflog --relative-date
```

用相对的日期显示引用日志。(如 2 周前）。

**讨论**

每次当前的 HEAD 更新时（如切换分支、拉取新更改、重写历史或只是添加新的提交），引用日志都会添加一个新条目。

**栗子**

为了理解 `git reflog`，我们来看一个🌰。

```
0a2e358 HEAD@{0}: reset: moving to HEAD~2
0254ea7 HEAD@{1}: checkout: moving from 2.2 to master
c10f740 HEAD@{2}: checkout: moving from master to 2.2
```

上面的引用日志显示了 master 和 2.2 的 branch 之间的相互切换。还有对一个更老的提交的强制重设。最近的活动用 `HEAD@{0}` 标记在上方显示。

如果事实上你是不小心切换回去的，引用日志包含了你意外地丢掉两个提交之前 master 指向的提交 0254ea7。

```
git reset --hard 0254ea7
```

使用 [`git reset`](https://github.com/geeeeeeeeek/git-recipes/wiki/2.6-%E5%9B%9E%E6%BB%9A%E9%94%99%E8%AF%AF%E7%9A%84%E4%BF%AE%E6%94%B9#git-reset)，就有可能能将master变回之前的那个提交。它提供了一张安全网，以防历史发生意外更改。

务必记住，引用日志提供的安全网只对提交到本地仓库的更改有效，而且只有移动操作会被记录。

#  3. 保持同步

SVN 使用唯一的中央仓库作为开发者之间沟通的桥梁，在开发者的工作拷贝和中央仓库之间传递变更集合（changeset），协作得以发生。这和Git的协作模型有所不同，Git 给予每个开发者一份自己的仓库拷贝，拥有自己完整的本地历史和分支结构。用户通常共享一系列的提交而不是单个变更集合。Git 允许你在仓库间共享整个分支，而不是从工作副本提交一个差异集合到中央仓库。

下面的命令让你管理仓库之间的连接，将分支「推送」到其他仓库来发布本地历史，或是将分支「拉取」到本地仓库来查看其它开发者的贡献。

## git remote

`git remote` 命令允许你创建、查看和删除和其它仓库之间的连接。远程连接更像是书签，而不是直接跳转到其他仓库的链接。它用方便记住的别名引用不那么方便记住的 URL，而不是提供其他仓库的实时连接。

例如，下图显示了你的仓库和中央仓库以及另一个开发者仓库之间的远程连接。你可以向 Git 命令传递 origin 和 john 的别名来引用这些仓库，替代完整的 URL。

![Git Tutorial: git remote](https://www.atlassian.com/dam/jcr:df13d351-6189-4f0b-94f0-21d3fcd66038/01.svg)

**用法**

```
git remote
```

列出你和其他仓库之间的远程连接。

```
git remote -v
```

和上个命令相同，但同时显示每个连接的 URL。

```
git remote add <name> <url>
```

创建一个新的远程仓库连接。在添加之后，你可以将 `<name>` 作为 `<url>` 便捷的别名在其他 Git 命令中使用。

```
git remote rm <name>
```

移除名为<name>的远程仓库的连接。

```
git remote rename <old-name> <new-name>
```

将远程连接从 `<old-name>` 重命名为 `<new-name>`。

**讨论**

Git 被设计为给每个开发者提供完全隔离的开发环境。也就是说信息并不是自动地在仓库之间传递。开发者需要手动将上游提交拉取到本地，或手动将本地提交推送到中央仓库中去。`git remote` 命令正是将 URL 传递给这些「共享」命令的快捷方式。

**名为 origin 的远程连接**

当你用 `git clone` 克隆仓库时，它自动创建了一个名为 origin 的远程连接，指向被克隆的仓库。当开发者创建中央仓库的本地副本时非常有用，因为它提供了拉取上游更改和发布本地提交的快捷方式。这也是为什么大多数基于 Git 的项目将它们的中央仓库取名为 origin。

**仓库的 URL**

Git 支持多种方式来引用一个远程仓库。其中两种最简单的方式便是 HTTP 和 SSH 协议。HTTP 是允许匿名、只读访问仓库的简易方式。比如：

```
http://host/path/to/repo.git
```

但是，直接将提交推送到一个 HTTP 地址一般是不可行的（你不太可能希望匿名用户也能随意推送）。如果希望对仓库进行读写，你需要使用 SSH 协议：

```
ssh://user@host/path/to/repo.git
```

你需要在托管的服务器上有一个有效的 SSH 账户，但不用麻烦了，Git 支持开箱即用的 SSH 认证连接。

**栗子**

除了 origin 之外，添加你同事的仓库连接通常会带来一些便利。比如，如果你的同事 John 在 `dev.example.com/john.git` 上维护了一个公开的仓库，你可以这样添加连接：

```
git remote add john http://dev.example.com/john.git
```

通过这种方式访问每个开发者的仓库，中央仓库之外的协作变得可能。这给维护大项目的小团队带来了极大的便利。

## git fetch

`git fetch` 命令将提交从远程仓库导入到你的本地仓库。拉取下来的提交储存为远程分支，而不是我们一直使用的普通的本地分支。你因此可以在整合进你的项目副本之前查看更改。

**用法**

```
git fetch <remote>
```

拉取仓库中所有的分支。同时会从另一个仓库中下载所有需要的提交和文件。

```
git fetch <remote> <branch>
```

和上一个命令相同，但只拉取指定的分支。

**讨论**

当你希望查看其他人的工作进展时，你需要 fetch。fetch 下来的内容表示为一个远程分支，因此不会影响你的本地开发。这是一个安全的方式，在整合进你的本地仓库之前，检查那些提交。类似于 svn update，你可以看到中央仓库的历史进展如何，但它不会强制你将这些进展合并入你的仓库。

**远程分支**

远程分支和本地分支一样，只不过它们代表这些提交来自于其他人的仓库。你可以像查看本地分支一样查看远程分支，但你会处于分离 HEAD 状态（就像查看旧的提交时一样）。你可以把它们视作只读的分支。如果想要查看远程分支，只需要向 `git branch` 命令传入 `-r` 参数。远程分支拥有 remote 的前缀，所以你不会将它们和本地分支混起来。比如，下面的代码片段显示了从 origin 拉取之后，你可能想要查看的分支：

```
git branch -r
# origin/master
# origin/develop
# origin/some-feature
```

同样，你可以用寻常的 `git checkout` 和 `git log` 命令来查看这些分支。如果你接受远程分支包含的更改，你可以使用 `git merge` 将它并入本地分支。所以，不像 SVN，同步你的本地仓库和远程仓库事实上是一个分两步的操作：先 fetch，然后 merge。`git pull` 命令是这个过程的快捷方式。

**栗子**

这个例子回顾了同步本地和远程仓库 `master` 分支的常见工作流：

```
git fetch origin
```

它会显示会被下载的分支：

```
a1e8fb5..45e66a4 master -> origin/master
a1e8fb5..9e8ab1c develop -> origin/develop
* [new branch] some-feature -> origin/some-feature
```

在下图中，远程分支中的提交显示为方块，而不是圆圈。正如你所见，`git fetch` 让你看到了另一个仓库完整的分支结构。



![Git Tutorial: git fetch](https://wac-cdn.atlassian.com/dam/jcr:0718ae20-0dc5-482c-a38c-25e4f1a1a3b0/02.svg)



若想查看添加到上游 master 上的提交，你可以运行 `git log`，用 `origin/master` 过滤：

```
git log --oneline master..origin/master
```

用下面这些命令接受更改并并入你的本地 `master` 分支：

```
git checkout master
git log origin/master
```

我们可以使用 `git merge origin/master`：

```
git merge origin/master
```

origin/master 和 master 分支现在指向了同一个提交，你已经和上游的更新保持了同步。

## git pull

在基于 Git 的协作工作流中，将上游更改合并到你的本地仓库是一个常见的工作。我们已经知道应该使用 `git fetch`，然后是 `git merge`，但是 `git pull` 将这两个命令合二为一。

**用法**

```
git pull <remote>
```

拉取当前分支对应的远程副本中的更改，并立即并入本地副本。效果和 `git fetch` 后接 `git merge origin/.` 一致。

```
git pull --rebase <remote>
```

和上一个命令相同，但使用 `git rebase` 合并远程分支和本地分支，而不是使用 `git merge`。

**讨论**

你可以将 `git pull` 当做 Git 中对应 `svn update` 的命令。这是同步你本地仓库和上游更改的简单方式。下图揭示了 pull 过程中的每一步。

![Git Tutorial: git pull](https://www.atlassian.com/dam/jcr:60943ee2-bec2-4433-8216-885c4bd3c2b9/03.svg)

你认为你的仓库已经同步了，但 `git fetch` 发现 origin 中 `master` 的版本在上次检查后已经有了新进展。 接着 `git merge` 立即将 `remote master` 并入本地的分支。

**基于 Rebase 的 Pull**

`--rebase` 标记可以用来保证线性的项目历史，防止合并提交（merge commits）的产生。很多开发者倾向于使用 rebase 而不是 merge，因为「我想要把我的更改放在其他人完成的工作之后」。在这种情况下，与普通的 `git pull` 相比而言，使用带有 `--rebase` 标记的 `git pull` 甚至更像 svn update。

事实上，使用 `--rebase` 的 pull 的工作流是如此普遍，以致于你可以直接在配置项中设置它：

```
git config --global branch.autosetuprebase always # In git < 1.7.9
git config --global pull.rebase true              # In git >= 1.7.9
```

在运行这个命令之后，所有的 `git pull` 命令将使用 `git rebase` 而不是 `git merge`。

**栗子**

下面的栗子演示了如何和一个中央仓库的 `master branch` 同步：

```
git checkout master
git pull --rebase origin
```

简单地将你本地的更改放到其他人已经提交的更改之后。

## git push

Push 是你将本地仓库中的提交转移到远程仓库中时要做的事。它和 `git fetch` 正好相反，fetch 将提交导入到本地分支，而 push 将提交导出到远程分支。它可以覆盖已有的更改，所以你需要小心使用。这些情况请见下面的讨论。

**用法**

```
git push <remote> <branch>
```

将指定的分支推送到 `<remote>` 上，包括所有需要的提交和提交对象。它会在目标仓库中创建一个本地分支。为了防止你覆盖已有的提交，如果会导致目标仓库非快速向前合并时，Git 不允许你 push。

```
git push <remote> --force
```

和上一个命令相同，但即使会导致非快速向前合并也强制推送。除非你确定你所做的事，否则不要使用 `--force` 标记。

```
git push <remote> --all
```

将所有本地分支推送到指定的远程仓库。

```
git push <remote> --tags
```

当你推送一个分支或是使用 `--all` 选项时，标签不会被自动推送上去。`--tags` 将你所有的本地标签推送到远程仓库中去。

**讨论**

`git push` 最常见的用法是将你的本地更改发布到中央仓库。在你积累了一些本地提交，准备和同事们共享时，你（可以）用交互式 rebase 来清理你的提交，然后推送到中央仓库去。



![Git Tutorial: git push](https://www.atlassian.com/dam/jcr:f148974e-7d4d-4c0e-bd31-8ac5467d1e6a/04.svg)



上图显示了当你本地的 master 分支进展超过了中央仓库的 `master` 分支，当你运行 `git push origin master` 发布更改时发生的事情。注意，`git push` 和在远程仓库内部运行 `git merge master` 事实上是一样的。

**强制推送**

Git 为了防止你覆盖中央仓库的历史，会拒绝你会导致非快速向前合并的推送请求。所以，如果远程历史和你本地历史已经分叉，你需要将远程分支 pull 下来，在本地合并后再尝试推送。这和 SVN 让你在提交更改集合之前要和中央仓库同步是类似的。

`--force` 这个标记覆盖了这个行为，让远程仓库的分支符合你的本地分支，删除你上次 pull 之后可能的上游更改。只有当你意识到你刚刚共享的提交不正确，并用 `git commit --amend` 或者交互式 rebase 修复之后，你才需要用到强制推送。但是，你必须绝对确定在你使用 `--force` 标记前你的同事们都没有 pull 这些提交。

**只推送到裸仓库**

此外，你只应该推送到那些用 `--bare` 标记初始化的仓库。因为推送会弄乱远程分支结构，很重要的一点是，永远不要推送到其他开发者的仓库。但因为裸仓库没有工作目录，不会发生打断别人的开发之类的事情。

**栗子**

下面的栗子描述了将本地提交推送到中央仓库的一些标准做法。首先，确保你本地的 `master` 和中央仓库的副本是一致的，提前 fetch 中央仓库的副本并在上面 rebase。交互式 rebase 同样是共享之前清理提交的好机会。接下来，`git push` 命令将你本地 `master` 分支上的所有提交发送给中央仓库.

```
git checkout master
git fetch origin master
git rebase -i origin/master
# Squash commits, fix up commit messages etc.
git push origin master
```

因为我们已经确信本地的 `master` 分支是最新的，它应该导致快速向前的合并，`git push` 不应该抛出非快速向前之类的问题。


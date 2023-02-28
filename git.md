# 第一章、版本控制

## 1、文件的版本

![image-20230227183418074](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227183418074.png)

## 2、版本控制软件

![image-20230227184411136](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227184411136.png)

## 3、使用版本控件软件的好处

![image-20230227184448772](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227184448772.png)

## 4、版本控制系统的分类

![image-20230227184528268](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227184528268.png)

### 4.1、本地版本控制系统

![image-20230227184601679](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227184601679.png)

特点：

使用软件来记录文件的不同版本，提高了工作效率，

降低了手动维护版本的出错率

缺点：

① **单机运行，不支持多人协作开发**

② 版本数据库故障后，所有历史更新记录会丢失

### 4.2、集中化的版本控制系统

![image-20230227184711384](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227184711384.png)

特点：基于**服务器、客户端**的运行模式

① 服务器保存文件的所有更新记录

② 客户端**只保留最新的文件版本**

优点：联网运行，支持多人协作开发

缺点：

① 不支持离线提交版本更新

② 中心服务器崩溃后，所有人无法正常工作

③ 版本数据库故障后，所有历史更新记录会丢失

典型代表：SVN

### 4.3、分布式版本系统

![image-20230227184854147](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227184854147.png)

特点：基于**服务器、客户端**的运行模式

+ 服务器保存文件的所有更新版本

+ **客户端是服务器的完整备份**，并不是只保留文件的最新版本

优点：

① 联网运行，支持多人协作开发

② 客户端**断网后支持离线本地提交**版本更新

③ 服务器故障或损坏后，可使用任何一个客户端的备份进行恢复

典型代表：Git

# 第二章、Git

## 1、什么是Git

Git 是一个**开源的分布式版本控制系统**，是目前世界上最先进、最流行的版本控制系统。可以快速高效地处理

从很小到非常大的项目版本管理。

特点：项目越大越复杂，协同开发者越多，越能体现出 Git 的**高性能和高可用性**！

## 2、Git的特性

Git 之所以快速和高效，主要依赖于它的如下两个特性：

① 直接记录快照，而非差异比较

② 近乎所有操作都是本地执行

### 2.1、SVN的差异比较

传统的版本控制系统（例如 SVN）是**基于差异**的版本控制，它们存储的是**一组基本文件和每个文件随时间逐步累积的差异**

![image-20230227185215273](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227185215273.png)

好处：节省磁盘空间

缺点：**耗时、效率低**

在每次切换版本的时候，都需要在基本文件的基础上，应用每个差异，从而生成目标版本对应的文件

### 2.2、Git的记录快照

Git 快照是在原有文件版本的基础上重新生成一份新的文件，**类似于备份**。为了效率，如果文件没有修改，Git 

不再重新存储该文件，而是只保留一个链接指向之前存储的文件。

![image-20230227185321404](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227185321404.png)

缺点：占用磁盘空间较大

优点：**版本切换时非常快**，因为每个版本都是完整的文件快照，切换版本时直接恢复目标版本的快照即可。

特点：==空间换时间==

### 2.3、近乎所有操作都是本地执行

![image-20230227185417596](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227185417596.png)

在 Git 中的绝大多数操作都**只需要访问本地文件和资源**，一般不需要来自网络上其它计算机的信息。

特性：

① 断网后依旧可以在本地对项目进行版本管理

② 联网后，把本地修改的记录同步到云端服务器即可

## 3、Git的三个区域

使用 Git 管理的项目，拥有三个区域，分别是==工作区、暂存区、Git 仓库==。

+ 工作区：处理工作的区域
+ 暂存区：已完成的工作的**临时存放区域，等待被提交。**
+ Git仓库：最终存放区域

## 4、Git中的三种状态

![image-20230227185653170](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227185653170.png)

注意：

+ 工作区的文件被修改了，但还没有放到暂存区，就是**已修改**状态。
+ 如果文件已修改并放入暂存区，就属于**已暂存**状态。
+ 如果 Git 仓库中**保存着特定版本**的文件，就属于**已提交**状态。

## 5、基本的Git工作流程

![image-20230227185807306](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230227185807306.png)

基本的 Git 工作流程如下：

① 在工作区中修改文件

② 将你想要下次提交的更改进行暂存

③ 提交更新，找到暂存区的文件，将快照永久性

存储到 Git 仓库

# 第三章、Git的基本操作

## 1、安装并配置Git

### 1.1、下载Git

在开始使用 Git 管理项目的版本之前，需要将它安装到计算机上。可以使用浏览器访问如下的网址，根据自己

的操作系统，选择下载对应的 Git 安装包：

https://git-scm.com/downloads

### 1.2、配置用户信息

安装完 Git 之后，要做的第一件事就是设置自己的用户名和邮件地址。因为通过 Git 对项目进行版本管理的时

候，Git 需要使用这些基本信息，来记录是谁对项目进行了操作：

```
git config -global user.name "lsy"
git config -global user.eamil "3086603619@qq.com"
```

注意：如果使用了 ==--global== 选项，那么该命令只需要运行一次，即可永久生效

通过 git config --global user.name 和 git config --global user.email 配置的用户名和邮箱地址，会被写

入到 **C:/Users/用户名文件夹/.gitconfig** 文件中。这个文件是 Git 的**全局配置文件**，**配置一次即可永久生效**。

可以使用记事本打开此文件，从而查看自己曾经对 Git 做了哪些全局性的配置。

### 1.3、检查配置信息

除了使用记事本查看全局的配置信息之外，还可以运行如下的终端命令，快速的查看 Git 的全局配置信息：

![image-20230228162411942](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228162411942.png)

### 1.4、获取帮助信息

可以使用 git help <verb> 命令，无需联网即可在浏览器中打开帮助手册，例如：

![image-20230228162446069](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228162446069.png)

如果不想查看完整的手册，那么可以用 -h 选项获得更简明的“help”输出：

![image-20230228162459489](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228162459489.png)

## 2、Git的基本操作

### 2.1、获取Git仓库的两种方式

① 将尚未进行版本控制的本地目录**转换**为 Git 仓库

② 从其它服务器**克隆**一个已存在的 Git 仓库

以上两种方式都能够在自己的电脑上得到一个可用的 Git 仓库

### 2.2、在现有目录中初始化仓库

如果自己有一个尚未进行版本控制的项目目录，想要用 Git 来控制它，需要执行如下两个步骤：

① 在项目目录中，通过鼠标右键打开“Git Bash”

② 执行 ==git init== 命令将当前的目录转化为 Git 仓库

git init 命令会创建一个名为 .git 的隐藏目录，**这个 .git 目录就是当前项目的 Git 仓库**，里面包含了初始的必要

文件，这些文件是 Git 仓库的必要组成部分。

### 2.3、工作区中文件的4种状态

工作区中的每一个文件可能有 4 种状态，这四种状态共分为两大类，如图所示：

![image-20230228162858661](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228162858661.png)

Git 操作的终极结果：让工作区中的文件都处于“==未修改==”的状态。

### 2.4、检查文件的状态

可以使用 ==git status== 命令查看文件处于什么状态，例如：

![image-20230228163506661](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228163506661.png)

在状态报告中可以看到新建的 index.html 文件出现在 **Untracked files**（未跟踪的文件） 下面。

未跟踪的文件意味着 G**it 在之前的快照（提交）中没有这些文件**；Git 不会自动将之纳入跟踪范围，除非明确

地告诉它“我需要使用 Git 跟踪管理该文件”。

### 2.5、以精简的方式显示文件状态

使用 ==git status== 输出的状态报告很详细，但有些繁琐。如果希望以精简的方式显示文件的状态，可以使用如下

两条完全等价的命令，其中 **-s** 是 **--short** 的简写形式：

![image-20230228163644529](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228163644529.png)

未跟踪文件前面有**红色的 ??** 标记，例如：

![image-20230228163752084](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228163752084.png)

### 2.6、跟踪新文件

使用命令 ==git add== 开始跟踪一个文件。 所以，要跟踪 index.html 文件，运行如下的命令即可：

![image-20230228163830378](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228163830378.png)

此时再运行 git status 命令，会看到 index.html 文件在 Changes to be committed 这行的下面，说明已被

跟踪，并处于暂存状态：

![image-20230228163848027](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228163848027.png)

### 2.7、提交更新

现在暂存区中有一个 index.html 文件等待被提交到 Git 仓库中进行保存。可以执行 ==git commit== 命令进行提交,

其中 **-m 选项**后面是本次的**提交消息**，用来**对提交的内容做进一步的描述**：

![image-20230228163956046](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228163956046.png)

提交成功之后，会显示如下的信息：

![image-20230228164009902](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228164009902.png)

![image-20230228164305420](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228164305420.png)

### 2.8、对已提交的文件进行修改

目前，index.html 文件**已经被 Git 跟踪**，并且**工作区和 Git 仓库中**的 index.html 文件内容保持一致。当我们修改了工作区中 index.html 的内容之后，再次运行 gi**t status 和 git status -s** 命令，会看到如下的内容：

![image-20230228164427662](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228164427662.png)

文件 index.html 出现在 Changes not staged for commit 这行下面，说明**已跟踪文件的内容发生了变化，**

**但还没有放到暂存区**。

注意：修改过的、没有放入暂存区的文件前面有**红色的 M** 标记。

### 2.9、暂存已修改的文件

目前，工作区中的 index.html 文件已被修改，如果要暂存这次修改，需要再次运行 git add 命令，这个命令是个多功能的命令，主要有如下 3 个功效：

① 可以用它开始跟踪新文件

② 把**已跟踪的、且已修改**的文件放到暂存区

③ 把有冲突的文件标记为已解决状态

![image-20230228164558401](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228164558401.png)

### 2.10、提交已暂存的文件

再次运行 ==git commit -m "提交消息"==命令，即可将暂存区中记录的 index.html 的快照，提交到 Git 仓库中进行保存：

![image-20230228164825036](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228164825036.png)

### 2.11、撤销对文件的修改

撤销对文件的修改指的是：把对工作区中对应文件的修改，**还原**成 Git 仓库中所保存的版本。

操作的结果：所有的修改会丢失，且无法恢复！**危险性比较高，请慎重操作！**

![image-20230228165020794](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228165020794.png)

==撤销操作的本质：用 Git 仓库中保存的文件，覆盖工作区中指定的文件。==

### 2.12、向暂存区中一次性添加多个文件

如果需要被暂存的文件个数比较多，可以使用如下的命令，一次性将所有的新增和修改过的文件加入暂存区：

```
git add .
```

==今后在项目开发中，会经常使用这个命令，将新增和修改过后的文件加入暂存区==

### 2.13、取消暂存的文件

如果需要从暂存区中移除对应的文件，可以使用如下的命令：

```
git reset HEAD 要移除的文件名称
```

### 2.14、跳过使用暂存区域

Git 标准的工作流程是**工作区 → 暂存区 → Git 仓库**，但有时候这么做略显繁琐，此时可以跳过暂存区，直接将

工作区中的修改提交到 Git 仓库，这时候 Git 工作的流程简化为了**工作区 → Git 仓库。**

Git 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 **git commit 加上 -a** 选项，Git 就会自动把

所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤：

```
git commit -a -m "描述消息"
```

### 2.15、移除文件

从 Git 仓库中移除文件的方式有两种：

① 从 Git 仓库和工作区中**同时移除**对应的文件

② 只从 Git 仓库中移除指定的文件，但保留工作区中对应的文件

![image-20230228165921071](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228165921071.png)

### 2.16、忽略文件

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。 在这种情况下，我们可

以创建一个名为 **.gitignore** 的配置文件，列出要忽略的文件的匹配模式。

文件 .gitignore 的格式规范如下：

① 以 **# 开头**的是注释

② 以 **/ 结尾**的是目录

③ 以 **/ 开头**防止递归

④ 以 **! 开头**表示取反

⑤ 可以使用 **glob 模**式进行文件和文件夹的匹配（glob 指简化了的正则表达式）

==注意：.gitignore文件需要提交到仓库中==

### 2.17、global模式

所谓的 glob 模式是指简化了的正则表达式：

① **星号 \*** 匹配零个或多个任意字符

② **[abc]** 匹配任何一个列在方括号中的字符 （此案例匹配一个 a 或匹配一个 b 或匹配一个 c）

③ **问号 ?** 只匹配一个任意字符

④ 在方括号中使用**短划线**分隔两个字符， 表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配

所有 0 到 9 的数字）

⑤ **两个星号 \**** 表示匹配任意中间目录（比如 a/**/z 可以匹配 a/z 、 a/b/z 或 a/b/c/z 等）

### 2.18、.gitignore文件的例子

![image-20230228170200559](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228170200559.png)

### 2.19、查看提交记录

如果希望回顾项目的提交历史，可以使用 ==git log== 这个简单且有效的命令。

![image-20230228170243690](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228170243690.png)

### 2.20、回退到指定的版本

![image-20230228170440157](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230228170440157.png)

### 2.21、 小结

① 初始化 Git 仓库的命令

+ **git init**

② 查看文件状态的命令

+ **git status 或 git status -s**

③ 一次性将文件加入暂存区的命令

+ **git add .**

④ 将暂存区的文件提交到 Git 仓库的命令

+ **git commit -m "提交消息“**

# 第四章、GitHub

如果代码已经提交到github上，第二次无需执行GitHub上面的命令，只需输入git push，就可以将新增内容同步到GitHub上

```
git push
```


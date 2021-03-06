# Git由浅入深之版本控制系统

现在最高效的版本控制工具是什么？你最喜欢使用的版本控制工具是什么？

毫无疑问，Git是首选。本人从15年开始，无论是工作还是日常使用，均已全面转向Git。

## 前言 

版本控制系统（Version Control System）是一个可以记录单个或一系列文件在不同时间发生的变化的系统，版本控制系统操作的文件可以是计算机上任意文件。

通过该系统，我们可以在之后将文件恢复到发生某次改变前的状态；可以找回删除的文件；可以比较不同时间文件的差别；可以查看每一次修改的相关信息。

## 历史

### 原始的版本控制

版本控制的需求一直存在，在版本控制工具出现之前，人们通常通过将文件拷贝到另外的目录进行版本备份，这是最简单但也是很不稳定的方法，比如，我们有可能忘记或者修改错误文件，这时候是无法找回之前文件的；而且不定时的拷贝文件是件极其乏味的事情，同时随着文件越来越多，其拷贝一次的耗费时间也越来越长。

### 本地版本控制（Local Version Control System）

为了解决原始的版本控制诸多问题，程序员们在很久以前就开发了一个本地版本控制系统，该系统使用一个小型数据库保存所有的文件变化。

![本地版本控制](http://blog.codingplayboy.com/wp-content/uploads/2017/01/git-local-vcs.png)

 

### 集中版本控制系统（Centralized Version Control System）

使用版本控制系统的遇到的一个主要问题是如何与其他开发者合作。为了解决这个问题，开发者们开发了集中版本控制系统（CVCS）。

这类版本控制系统，如CVS,Subversion和Perforce使用一个单独的服务器，保存所有的文件版本，所有的客户端都从这里检出（check out）文件。

这种方式流行了很多年，至今还是有很多个人或企业使用。

![集中版本控制系统](http://blog.codingplayboy.com/wp-content/uploads/2017/01/git-centralized-vcs.png)

 

这类系统对比本地版本控制系统有很多优势，诸如：

- 开发者之间可以了解不同的开发进度；
- 管理员可以细粒度的控制哪些开发者可以拥有哪些权限；
- 相对于在每个客户端都安装配置本地数据库，只需要集中管理一个控制中心。

当然，没有什么是绝对完美的，CVCS也有很多问题，

- 最突出的问题就是，由于集中控制，一旦控制中心瘫痪，所有开发者开发进程都会受影响；
- 一旦控制中心服务器文件丢失，且没有备份，我们无法找回（除非在某客户端本地恰好还保存着未删除）；

针对这类问题，后来有了分布式版本控制系统。

### 分布式版本控制系统（Distributed Version Control System）

对于分布式版本控制系统（DVCS），如Git,Mercurial,Darcs，客户端不是只从服务器检出（check out）最新版本文件，而是克隆出整个代码库，即使服务器出问题了，我们也能从客户端找回文件，而且每个客户端依然可以在本地进行版本控制，等待服务器修复后，再上传。

![分布式版本控制系统](http://blog.codingplayboy.com/wp-content/uploads/2017/01/git-distributed-vcs.png)

实践证明，DVCS在处理不同开发者同时合作一个或多个项目时表现很好，最典型的就是Git了。

## Git

自诞生以来，引起过很多争议，但这并不影响开发者们对Git的青睐，一个好的分布式版本控制系统优化方向主要从以下几点着手，就像Git一样：

- 速度（Speed）
- 简单 （Simple Design）
- 平行式开发（parallel development）
- 完全分布式（Fully distributed）
- 稳定高效（efficient）

自从2005年推出以来，Git已经成长为一个简单易用，稳定高效（尤其在处理大型项目上的表现），支持多分支平行开发的版本控制系统。

关于版本控制系统及Git的特性，已经略有所知，接下来是时候进入主题：Git由浅入深。

**图片来源git-scm**
[更多请查阅https://git-scm.com/doc](https://git-scm.com/doc)

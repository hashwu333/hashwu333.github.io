---
title: Linux学习笔记（一）：基本命令
date: 2021-05-17 17:55:07
tags:
  - Linux
  - Ubuntu
  - C
  - 笔记
catagories:
  - 技术力小本本
---
# Linux学习笔记（一）：基本命令

### 1.前言

这个月租了个阿里的云服务器，打算跑跑程序，看能不能把学校要求的每天健康打卡给自动化了。调整配置的时候决定安装Ubuntu系统（Linux系统的其中一个较为主流的发行版），然后就是怎么从零开始学会使用Linux了。不得不说，纯图形化界面是真的有点酸爽...

本文主要命令分类来源于MSU的[CSE 251 Programming in C](https://www.cse.msu.edu/~cse251/index.html)。



### 2.正文

#### 1.Some Unix commands

###### pwd

该命令将打印当前的目录。在服务器窗口输入,返回 /root。



###### ls

返回当前目录的内容。我这里返回了 python。/root/python 这个文件夹是我之前建立好的，后面会提到如何建立文件夹。

文件夹里这时候好像没有什么东西，我们来创建一个吧。

输入 touch MyFirstFile 命令，正如其名，这个命令将会去touch一个叫做“MyFirstFile”的文件，并将这个文件的修改时间改变为现在的时间。如果要touch的这个文件不存在的话，这个命令会创建一个空的新文件。

好了，现在我们想要了解一下当前的文件信息，输入 ls -l 看看。

返回了一个list，包括文件的名称，以及它们的日期与时间。

~~~c
root@iZ2ze3k4u650foe8tgu5r9Z:~# ls -l
total 4
-rw-r--r-- 1 root root    0 Mar 12 20:15 MyFirstFile
drwxr-xr-x 3 root root 4096 Mar 12 09:25 python
~~~

再介绍另外两个ls命令。第一个，ls -a。这个命令会返回all文件的list，其中包括系统使用的、被hidden的文件。我这里返回如下：

~~~c
root@iZ2ze3k4u650foe8tgu5r9Z:~# ls -a
.  ..  .bash_history  .bashrc  .cache  MyFirstFile  .pip  .profile  .pydistutils.cfg  python  .ssh
~~~

第二个，ls -F。This lists directories with a trailing "/". This makes it easier to tell directories from files.

我不确定这里怎么翻译更合适，反正...能意会就行。

~~~c
root@iZ2ze3k4u650foe8tgu5r9Z:~# ls -F
MyFirstFile  python/
~~~



###### rm

rm命令，即remove。

我们可以把刚刚的文件删除试试。输入rm MyFirstFile。这里要注意，系统命令是大小写敏感的。

~~~c
root@iZ2ze3k4u650foe8tgu5r9Z:~# rm Myfirstfile
rm: cannot remove 'Myfirstfile': No such file or directory
root@iZ2ze3k4u650foe8tgu5r9Z:~# rm MyFirstFile
root@iZ2ze3k4u650foe8tgu5r9Z:~# ls
python
~~~



###### mkdir & rmdir

分别是创造一个新的目录（make a new directory)和移除一个目录。



###### cd

就像我们在命令行中得知的那样，cd改变当前的文件夹。我创建了一个 cse251，再cd进去。如下。

~~~c
root@iZ2ze3k4u650foe8tgu5r9Z:~# mkdir cse251
root@iZ2ze3k4u650foe8tgu5r9Z:~# ls
cse251  python
root@iZ2ze3k4u650foe8tgu5r9Z:~# cd cse251
root@iZ2ze3k4u650foe8tgu5r9Z:~/cse251# ls
~~~

cd下面还有三个命令需要介绍。

第一个：

~~~
cd ..
~~~

这个命令的作用是回到父文件目录。

第二个：

~~~
cd .
~~~

The special directory name "." means the current directory. We just told it to change to the current directory. It didn't do anything, of course, since we are already in the current directory. But, we'll use this later on for other things.

第三个：

~~~
cd ~
~~~

这个命令是回到首页文件夹。



#### 2.Paths

~~~c
cd ~/cse251
~~~

输入这个命令之后，我们就进入了相应路径下的文件夹。

~~~c
cd ../cse251
~~~

这个命令后我们进入父文件夹的子文件夹cse251（其实还是那个文件夹）

~~~c
cd ../cse251/.././cse251
~~~

".."意味着父文件夹，"."意味着子文件夹。所以这个命令我们可以想象为在文件夹中反复横跳hhh。



#### 3.Files

###### cp

cp命令是复制一个文件。

~~~c
root@iZ2ze3k4u650foe8tgu5r9Z:~# ls
cse251  python
root@iZ2ze3k4u650foe8tgu5r9Z:~/cse251# cp ~/cse251/Hello.c ~/
root@iZ2ze3k4u650foe8tgu5r9Z:~/cse251# ls
Hello.c
root@iZ2ze3k4u650foe8tgu5r9Z:~/cse251# cd ~
root@iZ2ze3k4u650foe8tgu5r9Z:~# ls
cse251  Hello.c  python
~~~

复制后使用ls命令可以看到，cp命令成功了。

###### mv

mv命令用于移动或重命名一个文件。

~~~c
root@iZ2ze3k4u650foe8tgu5r9Z:~# mv Hello.c Myhello.c
root@iZ2ze3k4u650foe8tgu5r9Z:~# ls
cse251  Myhello.c  python
~~~

###### less and cat

cat命令展示一个文件的内容。

less命令将进入一个程序界面来显示文件内容，按q退出。



#### 4.Help

~~~c
man ls
~~~

man命令用来获取一个命令的细节。会进入一个和less命令后一样的新窗口。退出方式一样。

~~~c
yelp &
~~~

This starts a program that makes it easier to view available help. The & at the end tells it to run as another process. This means the command starts it and immediately returns, while yelp continues to run in another process on its own.

（这里贴的原文，因为阿里云服务器居然没有yelp，很淦。这就是轻量级服务器吗。）



#### 5.ps and kill

~~~c
ps u
~~~

这个命令可以让我们看到一个正在运行的进程的list，每个list都有一个process id（PID)。使用PID可以用来杀掉进程，像下面那样：

~~~c
kill 15507
~~~



#### 总结

| pwd   | Displays the current directory | pwd                                                          |
| ----- | ------------------------------ | ------------------------------------------------------------ |
| ls    | List the current directory     | ls ls -l ls -a -l : Include file details, -a : Include hidden files, -F : show directories |
| rm    | Remove a file                  | rm filetonuke.c                                              |
| mkdir | Create a new directory         | mkdir cse251                                                 |
| rmdir | Remove a directory             | rmdir cse251 Or rm -r if the directory is not empty.         |
| cd    | Change current directory       | cd ~/cse251                                                  |
| cp    | Copy a file                    | cp souce destination                                         |
| mv    | Move or rename a file          | mv hello.c newname.c                                         |
| cat   | Display the contents of a file | cat hello.c                                                  |
| less  | Display file contents nicely   | less hello.c                                                 |
| man   | Manual pages                   | man ls                                                       |
| yelp  | Nicer help display             | yelp &                                                       |
| top   | Displays CPU usage             | top q to quit                                                |
| ps    | Lists processes                | ps u                                                         |
| kill  | Kills a process                | kill 15577                                                   |






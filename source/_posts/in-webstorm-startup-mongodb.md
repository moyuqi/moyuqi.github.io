title: 在WebStorm中启动MongoDB
date: 2013-07-14 22:27:41
tags:
- WebStorm
- MongoDB
categories: 软件技巧
---

最近刚好找到一个学nodejs的教程是教[如何用nodejs和mongodb搭建博客的](https://github.com/nswbmw/N-blog/wiki/_pages)。教程通俗易懂，能快速了解nodejs和mongodb。

呵呵，前奏说的有点长。

学习mongodb都知道启动mongodb时需要打开 cmd，切换到 \mongodb\bin 目录下，在命令行中输入 mongod -dbpath "数据库路径" 设置 某个文件夹作为我们工程的存储目录，这样数据库就成功启动了。

省事的做法就是直接创建一个bat文件，并写入`d:\mongodb\bin\mongod.exe -dbpath d:\mongodb\blog` ，这样我们以后只需要运行这个bat就能启动数据库了 。

我平常的开发工具是WebStorm，如果按照上面的做法还需要切出去启动一下，觉得挺麻烦的。尝试在开发工具中配置命令直接启动，最好还配个快捷键更方便了。

经过研究，终于知道方法了：

<!--more-->

1. 第一步:

在工程跟路径下创建mongodb.bat，输入`D:\DevTools\mongodb\bin\mongod.exe -dbpath F:\NodeJsProjects\webstorm\blogdb`

2. 第二步：

打开settings-> External Tools,点+号，在tool setting里填空：

![mongdb设置](/images/2013/0714/in-webstorm-startup-mongodb-setting.png)

说明：

[Program]:外部命令所在位置，填入mongo.bat的路径，'$ProjectFileDir$\mongodb.bat'表示运行当前项目根目录下的mongodb.bat文件。

[Working Directory]:在哪个目录下运行这条命令，输入$ProjectFileDir$表示在当前项目的根目录下运行。

关于$ProjectFileDir$等参数可以点右边的insert macro查看详细说明。

3.最后给这个命令起个名字，比方叫mongodb，保存关闭。

在顶部菜单找到tools就可以看到刚保存的比方叫mongodb。点击它后就启动monggodb啦~

![mongdb设置结果](/images/2013/0714/in-webstorm-startup-mongodb-show.png)

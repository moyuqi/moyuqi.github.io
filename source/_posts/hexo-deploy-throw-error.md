title: Hexo deploy时报"Error: spawn ENOENT"的解决办法
date: 2013-07-09 22:30:56
tags:
categories:
---
把blog从octopress转到hexo，顺便学习了一下nodejs。<br />
在进行deploy时，抛出了如下异常：
```
Clearing
Copying files from public folder.

events.js:72
        throw er; // Unhandled 'error' event
              ^
Error: spawn ENOENT
    at errnoException (child_process.js:980:11)
    at Process.ChildProcess._handle.onexit (child_process.js:771:34)
```

通过google "hexo child_process"后，在 hexo 项目的 issue中找到了  [#156](https://github.com/tommy351/hexo/issues/156) 中找到了解决办法。<br />
原因是：
>我在cmd中敲命令导致无法上传github，改为在git bash中deploy 后正常。因为可能当初装git时只使用 git bash，导致cmd中无法使用git命令。

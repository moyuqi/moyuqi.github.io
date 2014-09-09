title: "VirtualBox4.1下为Debian6.0安装增强功能"
id: 59
date: 2012-02-18 12:36:43
tags: 
- Debian
- VirtualBox
categories: 
- Linux学习
---

<span style="color: #000000; font-family: 宋体; font-size: small;">操作系统： Win7
虚拟机：VirtualBox 4.1.6
虚拟机系统：debian-6.0.4-i386-DVD-1</span>

<!--more-->

<span style="color: #000000; font-family: 宋体; font-size: small;">在虚拟机中装完Debian6.0后，桌面分辨率默认为800*600，需要调整分辨率，这就需要安装VirtualBox的增强功能。按照如下步骤操作：</span>

<span style="color: #000000; font-family: 宋体; font-size: small;">1、进入虚拟机的Debian系统，用新立得软件包管理器，安装以下软件包：gcc, make, linux-headers-<span style="color: #00b0f0;">kernel_version</span>，关于内核版本可以在终端下通过[<span style="text-decoration: underline;">命令</span>](http://www.linuxso.com/command/)“[<span style="text-decoration: underline;">uname</span>](http://www.linuxso.com/command/uname.html) -r”获得。</span>

<span style="color: #000000; font-family: 宋体; font-size: small;">2、在虚拟机运行窗口上，点菜单“设备”---&gt;“安装增强功能”，系统会自动加载VBOXADDITIONS_4.1.4镜像，执行自动运行会提示自动运行软件出错</span>

<span style="color: #000000; font-family: 宋体; font-size: small;">3、打开Debian系统“应用程序”---&gt;“附件”---&gt;“Root 终端”，输入 [<span style="text-decoration: underline;">cd</span>](http://www.linuxso.com/command/cd.html) /media/cdrom，这是为了更改当前目录为cdrom下，然后接着输入 [<span style="text-decoration: underline;">su</span>](http://www.linuxso.com/command/su.html)do sh ./VBoxLinuxA[<span style="text-decoration: underline;">dd</span>](http://www.linuxso.com/command/dd.html)itions.run</span>

<span style="color: #000000; font-family: 宋体; font-size: small;">至此，增强软件包安装完毕，重启虚拟机即可自动调整窗口大小及分辨率，还能实现鼠标在虚拟OS和宿主OS之间自由切换。</span>
<div>[通过 Wiz 发布](http://www.wiz.cn/ "Wiz")</div>
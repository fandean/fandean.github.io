---
layout: post
title: "update-alternatives"
description: "update-alternatives命令的使用；更改Ubuntu默认程序"
date: 2017-07-22
tags: [Linux命令]
category: Linux
last_updated: 2017-07-23
comments: true
chare: true
---

* Kramdown table of contents
{:toc .toc}




# update-alternatives 命令

`update-alternatives --help` 命令输出：
```
用法：update-alternatives [<选项> ...] <命令>

命令：
  --install <链接> <名称> <路径> <优先级>
    [--slave <链接> <名称> <路径>] ...
                           在系统中加入一组候选项。
  --remove <名称> <路径>   从 <名称> 替换组中去除 <路径> 项。
  --remove-all <名称>      从替换系统中删除 <名称> 替换组。
  --auto <名称>            将 <名称> 的主链接切换到自动模式。
  --display <名称>         显示关于 <名称> 替换组的信息。
  --query <名称>           机器可读版的 --display <名称>.
  --list <名称>            列出 <名称> 替换组中所有的可用候选项。
  --get-selections         列出主要候选项名称以及它们的状态。
  --set-selections         从标准输入中读入候选项的状态。
  --config <名称>          列出 <名称> 替换组中的可选项，并就使用其中
                           哪一个，征询用户的意见。
  --set <名称> <路径>      将 <路径> 设置为 <名称> 的候选项。
  --all                    对所有可选项一一调用 --config 命令。

<链接> 是指向 /etc/alternatives/<名称> 的符号链接。
    (如 /usr/bin/pager)
<名称> 是该链接替换组的主控名。
    (如 pager)
<路径> 是候选项目标文件的位置。
    (如 /usr/bin/less)
<优先级> 是一个整数，在自动模式下，这个数字越高的选项，其优先级也就越高。

选项：
  --altdir <目录>          改变候选项目录。
  --admindir <目录>        设置 statoverride 文件的目录。
  --log <文件>             改变日志文件。
  --force                  就算没有通过自检，也强制执行操作。
  --skip-auto              在自动模式中跳过设置正确候选项的提示
                           (只与 --config 有关)
  --verbose                启用详细输出。
  --quiet                  安静模式，输出尽可能少的信息。不显示输出信息。
  --help                   显示本帮助信息。
  --version                显示版本信息。
```


## update-alternatives简介
必看的三篇介绍：  
- [update-alternatives - William DeMeo](http://williamdemeo.github.io/linux/update-alternatives.html "update-alternatives - William DeMeo")    
- [alternatives - Manages alternative programs for common commands — Ansible Documentation](http://docs.ansible.com/ansible/latest/alternatives_module.html "alternatives - Manages alternative programs for common commands — Ansible Documentation")   
- [update-alternatives学习笔记 - - CSDN博客](http://blog.csdn.net/HEYUTAO007/article/details/5441482 "update-alternatives学习笔记 - - CSDN博客")

update-alternatives实用程序的目的是：
可以在同一个系统上安装满足相同或相似功能的多个程序。 Debian的 alternative system 旨在管理这种情况。


- 使用“update-alternatives”工具管理符号链接
- 当安装了多个提供类似功能的程序时很有用

通用名称不是所选alternative的直接符号链接；而是替代目录(alternatives directory)中的一个名称的符号链接，而该目录又是一个引用的实际文件的符号链接。这样做是为了使系统管理员的更改可以被限制在/ etc目录中。


parameter参数 | required必须 | default默认值 | choices | comments描述
------- | ------- | ------- | ------- | -------
link | no |  |  | The path to the symbolic link that should point to the real executable.(指向实际可执行文件的符号链接的路径)
name | yes |  |  | The generic name of the link.(链接的通用名称)
path | yes |  |  | The path to the real executable that the link should point to.(链接应该指向的真实可执行文件的路径)
priority(added in 2.2) | no | 50 |  | The priority(优先级) of the alternative


- alternative 指一个可选程序所在的绝对路径  
- link是符号链接  
- name则是通用名称  
- path是执行文件的路径  
- priority则表示优先级  

> Linux 发展到今天，可用的软件已经非常多了。这样自然会有一些软件的功能大致上相同。例如，同样是编辑器，就有 nvi、vim、emacs、nano，而且我说的这些还只是一部分。大多数情况下，这样的功能相似的软件都是同时安装在系统里的，可以用它们的名称来执行。例如，要执行 vim，只要在终端下输入 vim 并按回车就可以了。不过，有些情况下我们需要用一个相对固定的命令调用这些程序中的一个。例如，当我们写一个脚本程序时，只要写下 editor，而不希望要为“编辑器是哪个”而操心。Debian 提供了一种机制来解决这个问题，而 update-alternatives 就是用来实现这种机制的。  
[update-alternatives学习笔记 - - CSDN博客](http://blog.csdn.net/HEYUTAO007/article/details/5441482 "update-alternatives学习笔记 - - CSDN博客")


## Eclipse示例

> 翻译 [update-alternatives - William DeMeo](http://williamdemeo.github.io/linux/update-alternatives.html "update-alternatives - William DeMeo")  

有三个版本的Eclipse，并且分别创建了三个启动脚本：  

版本一： `$HOME/opt/Eclipse/luna/eclipse-luna` ，脚本内容： 
```shell
#!/bin/bash
export UBUNTU_MENUPROXY=0
$HOME/opt/Eclipse/luna/eclipse
```
版本二： `$HOME/opt/Eclipse/kepler/eclipse-kepler` ，脚本内容： 
```shell
#!/bin/bash
export UBUNTU_MENUPROXY=0
$HOME/opt/Eclipse/kepler/eclipse
```
版本三： `$HOME/opt/Eclipse/scala/eclipse-scala` ，脚本内容： 
```shell
#!/bin/bash
export UBUNTU_MENUPROXY=0
$HOME/opt/Eclipse/scala/eclipse
```
这里使用脚本而不是直接使用`$HOME/opt/Eclipse/***/eclipse`，是为了添加启动参数。


现在可以通过在命令行中调用以下命令来配置Eclipse的各种版本：
```shell
sudo update-alternatives --install /usr/bin/eclipse eclipse $HOME/opt/Eclipse/scala/eclipse-scala 400
sudo update-alternatives --install /usr/bin/eclipse eclipse $HOME/opt/Eclipse/luna/eclipse-luna 300
sudo update-alternatives --install /usr/bin/eclipse eclipse $HOME/opt/Eclipse/kepler/eclipse-kepler 200
```
eclipse-scala 优先级为 400 是最高值，所以他就是默认程序。

你可以删除任何 alternative: 
```shell
sudo update-alternatives --remove eclipse $HOME/opt/Eclipse/scala/eclipse-scala
```
The command `update-alternatives --query eclipse` should now print something like this:
```shell
Name: eclipse
Link: /usr/bin/eclipse                                      # 1个 符号链接
Status: auto
Best: /home/williamdemeo/opt/Eclipse/scala/eclipse-scala
Value: /home/williamdemeo/opt/Eclipse/scala/eclipse-scala

Alternative: /home/williamdemeo/opt/Eclipse/kepler/eclipse-kepler   # 可选的程序所在的路径
Priority: 200

Alternative: /home/williamdemeo/opt/Eclipse/luna/eclipse-luna     # 可选的程序所在的路径
Priority: 300

Alternative: /home/williamdemeo/opt/Eclipse/scala/eclipse-scala   # 可选的程序所在的路径
Priority: 400
```

可通过如下命令来手动选择候选项：`update-alternatives --config eclipse`，命令输出：
```
There are 3 choices for the alternative eclipse (providing /usr/bin/eclipse).

  Selection    Path                                                  Priority   Status
------------------------------------------------------------
* 0            /home/williamdemeo/opt/Eclipse/scala/eclipse-scala     400       auto mode
  1            /home/williamdemeo/opt/Eclipse/kepler/eclipse-kepler   200       manual mode
  2            /home/williamdemeo/opt/Eclipse/luna/eclipse-luna       300       manual mode
  3            /home/williamdemeo/opt/Eclipse/scala/eclipse-scala     400       manual mode
```
前面加`*`号的表示当前选择的程序。然后可根据命令提示进行更改。

> 在使用`--config`选项之前，可以先使用`--display`替换该参数，先进行查看。  

如果你想为它们创建应用启动器(application launcher)可使用如下方法(也可以通过创建相关文档创建)：
```shell
mkdir -p ~/.local/share/applications
gnome-desktop-item-edit --create-new ~/.local/share/applications/
```

## Java示例
java就比较麻烦了点，因为java相关的命令比较多，要改的地方多。

还好有个`update-java-alternatives`命令。

可以查看另一篇文章: 《ubuntu安装jdk》




## 图形工具 Gnome alternatives
 Gnome Alternatives 
 ```
 sudo apt-get install galternatives
 ```

不推荐。


## 更改优先级

使用root权限编辑`/var/lib/dpkg/alternatives`下的相关文件，更改优先级后保存。

然后运行如下命令` sudo update-alternatives --auto 名称`，将“名称”替换成相应值。


比如： 
- 修改某网页浏览器的优先级，编辑文件`/var/lib/dpkg/alternatives/x-www-browser`然后运行如下命令` sudo update-alternatives --auto x-www-browser`使其生效。
- 修改编辑器的优先级，编辑文件`/var/lib/dpkg/alternatives/editor`然后运行如下命令` sudo update-alternatives --auto editor`使其生效。


> `--auto`选项，根据优先级设置回默认值(优先级最高的候选项)。 
> 
> 命令输出（在确实更改了editor后）：
> ```
> [fan 11:06:00]~$ update-alternatives --auto editor 
> update-alternatives: 使用 /usr/bin/vim.basic 来在自动模式中提供 /usr/bin/editor (editor)
> update-alternatives: 错误: 新建符号链接 /etc/alternatives/editor.dpkg-tmp 时出错: 权限不够
> [fan 11:07:39]~$ sudo update-alternatives --auto editor 
> [sudo] fan 的密码： 
> update-alternatives: 使用 /usr/bin/vim.basic 来在自动模式中提供 /usr/bin/editor (editor)
> ```


## 参考

[update-alternatives学习笔记](http://blog.csdn.net/HEYUTAO007/article/details/5441482)   
[使用update-alternatives工具配置可选系统](http://man.chinaunix.net/linux/debian/debian_learning/ch08s21.html)   
[使用update-alternatives切换Ubuntu默认java命令](http://blog.csdn.net/xyzxyzxz/article/details/6920346)     
[update-alternatives命令详解](http://coolnull.com/3339.html)   
[update-alternatives - William DeMeo](http://williamdemeo.github.io/linux/update-alternatives.html "update-alternatives - William DeMeo")    
[alternatives - Manages alternative programs for common commands — Ansible Documentation](http://docs.ansible.com/ansible/latest/alternatives_module.html "alternatives - Manages alternative programs for common commands — Ansible Documentation")     




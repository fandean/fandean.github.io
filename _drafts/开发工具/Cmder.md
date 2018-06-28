# Cmder

> 已发布

Cmder是一个用于替换windows自带的cmd的，包含各种软件包（比如 git）并且非常好用的终端模拟器。

![Cmde](http://cmder.net/img/main.png)



## 安装

在官网[Cmder](http://cmder.net/ "Cmder | Console Emulator")下载cmder压缩包，解压即可。这里**注意**解压路径不能位于需要管理员访问权限的地方。



- 添加环境变量：

  新建环境变量`%cmder_root%` 将其值设置为 `cmder.exe`所在路径，再将`%cmder_root%`添加到系统的`PATH`环境变量中。

- 将cmder添加到文件夹右键菜单：

  以管理员权限打开 cmd ；切换到 cmder 的解压路径；执行 `.\cmder.exe /REGISTER ALL`，即可添加。

- 为cmder创建桌面快捷方式。





## 常用操作



### 粘贴复制

复制：只需选中一段文字那么该段文字就会被复制到剪贴板

粘贴：直接`鼠标右键`即可粘贴，或者使用 `Ctrl + v` 进行粘贴.



### cmd模式和bash模式

主要是经常再cmd模式下输入bash相关的命令格式，导致相关错误。



### alias别名机制

**Cmder增加了alias功能：** 
它让你用短短的指令执行一些常见但指令超长又难以记忆的语法; 
在其控制台输入`alias`可以查看。



**自定义aliases：**  打开Cmder目录下的config文件夹，里面的aliases文件就是我们可以配置的别名文件。



> 补充： 锁定视窗 ，可以让视窗无法再输入 



## Cmder启动选项

相关介绍

- 进入seting界面：点击Cmder窗口左上角的图标 或者 右下角的 `三`图标，然后选择 `setting`

- 在Startup处设置cmder启动时需要执行的任务

  默认选择的启动项应该是 “ Specified named task” 而该启动项默认选择的应该是 `{cmd::Cmder}` 这个命名任务，我们可以更改成其它的命令任务或者直接切换到其它的启动项。单词都很简单，仔细看一下就懂。

  当选中某个命名任务时，下面的 "Selected task contents(选中的任务内容)"下会显示该任务执行的具体内容

  > 这里`cmd::Cmder`前面的cmd标明它是cmd模式，我们可以看到还有 bash 和 PowerShell等模式

- 我们也可以在`startup -> tasks`处更改和添加 “ Specified named task” 下的命名任务。





### 自定义启动目录



下面就来仿照现有的`{cmd::Cmder}`添加一个设置自定义的启动目录的任务(Task)：

- 添加一个任务：切换到 `startup -> tasks` 后点击 `➕`，这里任务的名称为 `cmd::diy1`
- 设置命令：复制`{cmd::Cmder}`最下面的命令 `cmd /k ""%ConEmuDir%\..\init.bat" "`粘贴到 `cmd::diy1`相同的位置即可
- 设置参数（在此处设置目录）：下面来看 “Task parameters”命令参数，阅读实例可知参数 `/icon`指定图标位置，`/dir` 指定启动目录，所以我们可以添加下面的参数：` /icon "%CMDER_ROOT%\icons\cmder.ico"  /dir "C:\Users\Fan Dean"`其中`/icon`参数内容就借鉴 `{cmd::Cmder}` 的 `/dir`后的参数值就是你自行设置的路径。
- 然后在 `startup` 的“ Specified named task” 处选择 `cmd::diy1`
- 保存设置，退出，重新打开cmder查看效果



> 还有更高级的配置，还不会



>  具体配置和使用可见：[cmder: Lovely console emulator package for Windows](https://github.com/cmderdev/cmder "cmderdev/cmder: Lovely console emulator package for Windows") 。




## 其它问题



### cmder无法切换路径?

一次想切换到C盘，我输入下面的命令：

```shell
λ cd C:
C:\

D:\Portable Software\cmder
λ cd ~
系统找不到指定的路径。

D:\Portable Software\cmder
λ pwd
D:\Portable Software\cmder

D:\Portable Software\cmder
λ cd C:\Users\Fan Dean\Documents

D:\Portable Software\cmder
λ pwd
```

怎么切换不了路径？在网上查询了一下原来是这样：

如果是用默认的`bash`, 可以直接 `cd /d/myworkstation`
如果用的是`cmd`模式, 需要先输入 `d:`来切换到d盘

```
d:
cd myworkstation
```

 Windows 里，可以用 /? 获取详细的用法，比如： 

输入下面命令来了解一下cmd中cd的用法：

```shell
help cd
# 或者
cd /?
```



### 智能路径切换？

看下面的操作：

```shell
# 再当前路径输入 git status， 发现没有 git 仓库
D:\Portable Software\cmder
λ git status
fatal: not a git repository (or any of the parent directories): .git

# 切换到 c 盘
D:\Portable Software\cmder
λ C:
# 然后自动就给我切换到了包含git仓库的路径？？
C:\Users\Fan Dean\Documents\fandean.github.io (master -> origin)
λ 
```



> 还没搞懂


# Package manager for Windows (包管理工具)





在下载node时发现了两款用于Windows的包管理工具：

- [Chocolatey - The package manager for Windows](https://chocolatey.org/ "Chocolatey - The package manager for Windows")
- [Scoop](https://scoop.sh/ "Scoop")





## PortableApp

之前我一直使用PortableApp来安装一些简单的程序，主要优势是可以 

- 自动更新。
- 可以自定义安装路径（安装到C盘之外）。
- 绿色软件，当重装系统后可以更方便的迁移。



现在有了cmder、WSL、Docker





## Chocolatey

Chocolatey有 Open Source、Pro(Personal)和Business(C4B)三个版本，其中Open Source是免费的。



另外需要说明的是， Chocolatey 只是把官方下载路径封装到了 Chocolatey 中，所以下载源都是其官方路径 。



[Installation](https://chocolatey.org/install "Installation") Chocolatey自身安装在默认位置即可。



更改使用Chocolatey安装的软件的安装目录：  

**chocolatey免费版本**，本人已验证过可行：

```
choco install jdk10 -ia "INSTALLDIR=""D:\DevPrograms\Java\JDK\jdk10.0.1-x64"""
```


参考官方文档：
<https://chocolatey.org/docs/getting-started#overriding-default-install-directory-or-other-advanced-install-concepts>

如果是pro或business版本，可以使用`--install-directory`参数，参见文档：<https://chocolatey.org/docs/commands-install#installarguments>
`--dir, --directory, --installdir, --installdirectory, --install-dir, --install-directory=VALUE`





> [Windows 神器 Cmder Scoop Chocolatey Listary Seer - CSDN博客](https://blog.csdn.net/u013205877/article/details/78993311 "Windows 神器 Cmder Scoop Chocolatey Listary Seer - CSDN博客")



## Scoop

运行于 PowerShell  之中。在 cmder 中运行没有问题。

Github页面： [lscoop: A command-line installer for Windows.](https://github.com/lukesampson/scoop "lukesampson/scoop: A command-line installer for Windows.")

Scoop更专注于开源的命令行开发人员工具 。





Scoop支持的软件：[scoop/bucket](https://github.com/lukesampson/scoop/tree/master/bucket "scoop/bucket at master · lukesampson/scoop")

虽然 Scoop 的作者在项目的 GitHub Wiki 中谈到， Scoop 只是一个安装工具（installer），不应该被称为包管理器（package manager）。但是对于使用者而言，它与我们一般认为的软件包管理工具其实很是相似。 

总的来说， Chocolatey 能更加全面地包办绝大多数的软件安装，适应重度需求；而 Scoop 则更加简单利落，容易自定义软件包，适应中低需求。而我恰是后者，对于像 VirtualBox、Docker for Windows 这些需要高权限的软件还是会用安装包在用户界面下自定义安装。更特殊的用户倒是更可以将 Chocolatey 和 Scoop 结合使用。 

Chocolatey 的安装脚本默认要求管理员权限安装，同时非管理员安装默认路径是 `C:\ProgramData\chocoportable`，这对于非高权限用户来说不太友好（比如没有管理员权限的工作机安装会比较折腾），而 Scoop 默认仅需普通用户权限，安装路径是 `%USERPROFILE%\scoop` 则显得比较清新，不过这都是可以根据需求修改的了。 

其实如果你是偏重度的用户，想尽量多的软件可以用命令行管理，又不在乎我前文说的 Chocolatey 的软件包描述文件相对复杂等缺点的话，其实可以去试试使用 Chocolatey。而如果你没那么强烈的需求，只是像我一样有一点点 “绿色软件洁癖”，同时想用命令行管理部分软件包，并且以此构建一个相对轻量的命令行环境的话，不妨可以尝试一下 PowerShell + Scoop + Cmder 这套组合。或者，Chocolatey 和 Scoop 二者一起用也是可以的。 



> [再谈谈 Scoop 这个 Windows 下的软件包管理器 · Chawye Hsu, H404bi](https://h404bi.com/blog/2018/05/12/talk-about-scoop-the-package-manager-for-windows-again.html "再谈谈 Scoop 这个 Windows 下的软件包管理器 · Chawye Hsu, H404bi")





由于Scoop更容易配置，这里选择 Scoop



默认设置已配置为用户级别**安装的程序**和Scoop本身都位于 `C:\Users\<user>\scoop `

全局安装的程序（所有用户可用）（`--global`）位于`C\ProgramData\scoop`中。可以通过环境变量更改这些设置 。



#### Install Scoop to a Custom Directory

```
[environment]::setEnvironmentVariable('SCOOP','D:\Scoop','User')
$env:SCOOP='D:\Scoop'
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```

> 相当于在用户变量中设置  `SCOOP=D:\Scoop`

#### Configure Scoop to install global programs to a Custom Directory

```
[environment]::setEnvironmentVariable('SCOOP_GLOBAL','D:\Scoop\GlobalScoopApps','Machine')
$env:SCOOP_GLOBAL='D:\Scoop\GlobalScoopApps'
```

> 相当于在系统变量中设置： `SCOOP_GLOBAL=D:\Scoop\GlobalScoopApps`





Scoop可以安装哪些应用程序？ 

使用Scoop安装最佳的应用程序通常称为“便携式”应用程序：即在解压缩时独立运行的压缩程序文件，不存在更改注册表或将文件放在程序目录之外的副作用。 



常用命令：

```shell
scoop help #查看帮助
scoop install #安装 APP
scoop uninstall #卸载 APP
scoop list #列出已安装的 APP
scoop search #搜索 APP
scoop update #更新 APP 和 Scoop 自身
```





**安装 curl 、grep**

```
scoop install curl grep
```

我们发现，下载的过程中自动下载了依赖7zip。这说明scoop会帮助我们管理程序之间的依赖。不仅如此，**下载之后的内容会自动将加入到（Path）环境变量中**。十分方便！





### 已安装软件列表



添加额外的bucket：

```shell
λ scoop bucket add extras
Checking repo... ok
The extras bucket was added successfully.
```





离线文档查看 zeal ：可集成到 idea 等

First you need to enable Scoop's [extras](https://github.com/lukesampson/scoop-extras/) bucket, if that wasn't done before:

```
> scoop bucket add extras
```

To install Zeal run the following command:

```
> scoop install zeal
```

```shell
λ scoop install zeal
Installing '7zip' (18.05) [64bit]
7z1805-x64.msi (1.7 MB) [=========================================================================================================================] 100%
Checking hash of 7z1805-x64.msi... ok.
Extracting... done.
Linking D:\Scoop\Applications\apps\7zip\current => D:\Scoop\Applications\apps\7zip\18.05
Creating shim for '7z'.
Creating shortcut for 7-Zip (7zFM.exe)
'7zip' (18.05) was installed successfully!
Installing 'zeal' (0.5.0) [64bit]
zeal-portable-0.5.0-windows-x64.7z (20.0 MB) [====================================================================================================] 100%
Checking hash of zeal-portable-0.5.0-windows-x64.7z... ok.
Extracting... done.
Linking D:\Scoop\Applications\apps\zeal\current => D:\Scoop\Applications\apps\zeal\0.5.0
Creating shim for 'zeal'.
Creating shortcut for Zeal (zeal.exe)
Persisting zeal.ini
系统找不到指定的文件。
Persisting cache
Persisting docsets
'zeal' (0.5.0) was installed successfully!
```



视频播放器 mpv 

```shell
λ scoop install mpv
Installing 'mpv' (2018-07-31) [64bit]
mpv-x86_64-20180731.7z (15.3 MB) [================================================================================================================] 100%
Checking hash of mpv-x86_64-20180731.7z... ok.
Extracting... done.
Linking D:\Scoop\Applications\apps\mpv\current => D:\Scoop\Applications\apps\mpv\2018-07-31
Creating shim for 'mpv'.
Creating shortcut for mpv (mpv.exe)
Persisting portable_config
Running post-install script...
'mpv' (2018-07-31) was installed successfully!
Notes
-----
To set up file type associations and AutoPlay handlers use https://github.com/rossy/mpv-install
'mpv' suggests installing 'youtube-dl'.
```



文件同步工具 syncthing，在GitHub上超级火爆

```shell
λ scoop install syncthing
Installing 'syncthing' (0.14.49) [64bit]
syncthing-windows-amd64-v0.14.49.zip (7.1 MB) [===================================================================================================] 100%
Checking hash of syncthing-windows-amd64-v0.14.49.zip... ok.
Extracting... done.
Linking D:\Scoop\Applications\apps\syncthing\current => D:\Scoop\Applications\apps\syncthing\0.14.49
Creating shim for 'syncthing'.
'syncthing' (0.14.49) was installed successfully!
Notes
-----
To start syncthing automatically, use a method described at https://github.com/syncthing/docs/blob/master/users/autostart.rst#windows
```





ImageMagick 看图软件:

```shell
λ scoop install ImageMagick
Installing 'ffmpeg' (4.0.2) [64bit]
ffmpeg-4.0.2-win64-static.zip (62.7 MB) [====================================================================================================================] 100%
Checking hash of ffmpeg-4.0.2-win64-static.zip... ok.
Extracting... done.
Linking D:\Scoop\Applications\apps\ffmpeg\current => D:\Scoop\Applications\apps\ffmpeg\4.0.2
Creating shim for 'ffmpeg'.
Creating shim for 'ffplay'.
Creating shim for 'ffprobe'.
'ffmpeg' (4.0.2) was installed successfully!
Installing 'ImageMagick' (7.0.8-8) [64bit]
远程服务器返回错误: (404) 未找到。
URL https://www.imagemagick.org/download/binaries/ImageMagick-7.0.8-8-portable-Q16-x64.zip is not valid
```

远程服务器返回错误: (404) 未找到，看来需要手动更改 配置文件来更改可用的软件包下载地址。
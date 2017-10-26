## 通用设置

### 通过授权服务器激活



[JetBrains激活](http://www.imsxm.com/jetbrains-license-server.html "JetBrains激活 - 成都没有派对")

JetBrains 授权服务器(License Server URL): http://idea.imsxm.com

**使用方法：** 激活时选择License server 填入 `http://idea.imsxm.com`  点击Active即可。

**在线激活有一个过期时间**，这个时间一过就必须再次联网授权服务器请求激活。




### 同步设置


> 发现 Android Studio 中也有这个功能



**Setting Repository:**

[Settings Repository - Help - WebStorm](https://www.jetbrains.com/help/webstorm/settings-repository.html)

当开启Settings Repository plugin 时可以看到该选项。Use this page to configure the Settings Repository feature that allows you to **share your IDE settings** between different instances of WebStorm (**or other IntelliJ platform-based**) products installed on different computers.



**Sharing Your IDE Settings:**

[Sharing Your IDE Settings - Help - WebStorm](https://www.jetbrains.com/help/webstorm/sharing-your-ide-settings.html)

确保开启了Settings Repository插件。

配置Settings repository： 选择使用https协议的仓库URL 

将当前IDE的配置同步到远程仓库：

- 在服务器中创建一个Git仓库（比如在GitHub或 GitLab中创建）
- 导航到 File -> Settings Repository打开对话框；或者在欢迎界面通过 Configure ->Settings Repository打开对话框。 在对话框中 指定仓库的URL，并且点击 Overwrite **Remote**。

从远程仓库中获取配置并应用到本地IDE：

- 同样打开Settings Repository对话框，填写仓库的URL，但这次是点击 Overwrite **Local** 。如果你想合并远程和本地现有配置，可以选择点击 **Merge** 进行合并配置。
- 你还可以通过 Setings -> Tools -> Settings Respository -> Read-only Sources下添加多个仓库；或者在这里取消自动同步设置。



设置相关：

导出设置时的默认导出文件 `~/.AndroidStudio2.3/config/settings.jar`



### 代码提示(补全)

参考: [Code Completion](https://www.jetbrains.com/help/idea/2016.1/code-completion-2.html)

代码提示： 在 Editor标签中选择 Code Completion 选项，在"Code Sensitive completion"后的下拉列表中选择"None"，即提示不区分大小写（好吧在Webstorm中设置为None时没有提示，还是设置为First letter）。(默认为First letter)。



### 字体设置

**编辑器字体设置：** Editor > Font : 

最棒的字体 mononoki

Size ：16、18、17(感觉大小合适)

Line Spacing：1.1



其它字体还有： Monospaced，Consolas，



**界面字体设置：**Appearance & Behavior > Appearance： Name: "Arial Unicode MS"  Size: 12



### 主题

可选的自带主题：Monokai 



下载 "Material Theme UI" 主题插件，然后进行修改：

在 Editor > Color Scheme > Color Scheme Font > 选择 Material Default > 然后选择 Duplicate...  复制该主题，将复制后的主题命名为 "DIY Material Default copy"；按此方法将所有Material相关的主题都复制下来。

接下来禁用"Material Theme UI" 主题插件。

最后修改字体。

> 这里主要就是为了复制"Material Theme UI" 主题插件的代码配色方案，然后更改为自己想要的字体。〔强烈推荐〕











### 自动保存

**使用星号标记未保存的文件：** Editor > General > Editor Tabls > 勾选“Mark modified tabs with asterisk”

**自动保存：** Appearance & Behavior > System Settings > Synchronization 

下面讲解该处的4个选项：

* Synchronize file on frame or editor tab activation：激活当前窗口时保存
* Save files on frame deactivation：切换到其它窗口时保存
* Save files automatically if application is idle for [15] sec.：程序闲置15秒后保存
* Use "safe write"(save changes to a temporary file first)：...






### 部署到远程服务器

我们可以在IDE中配置FTP，以手动或自动上传代码到远程服务器。

1. 先设置远程服务器主机：Tools > Deployment > Browse Remote Host > 点击`...`来添加Server > Type可选：FTP、SFTP、FTPS、Local or mounted folder
2. 如果出现目录一直递归显示的情况，更改一下 Advanced Options ，勾选Passive mode 和 Compatibility mode
3. 手动上传：右键选中文件 > Deployment > Upload to xxx
4. 自动上传：Tools > Deployment > Options 更改“Upload changed files automatically to the default server”为非Never的其它选项。







### 通用插件



* .ignore：生成各种.ignore文件
* keypromoter：你用鼠标进行某项操作时，如果有快捷键，会提示你快捷键，如果没有，操作超过三次以后会提示你设置快捷键。
* CodeGlance：minimap








webstorm minimap对应的插件：

- CodeGlance

* Code Outline 2




## WebStorm

WebStorm 是收费软件，不过这不是大问题，我们有一些免费使用的方案：



[WebStorm，你一直在寻找的前端开发 IDE · Issue #6 · cssmagic/blog](https://github.com/cssmagic/blog/issues/6 "WebStorm，你一直在寻找的前端开发 IDE · Issue #6 · cssmagic/blog")

官方下载的版本都是可以 30 天免费试用的。到期之后还可以继续安装更新的 **EAP** 预览版  <http://confluence.jetbrains.com/display/WI/WebStorm+EAP>  ，继续合法免费试用。只要自己勤快一点儿，备份好个人设置，基本上可以一直免费用下去。所以，我完全不建议你去找什么破解版或盗版序列号。

**好像该方法不管用了**。



[【程序员小助手】免费获得WebStorm正式版 - 程序员联盟 frogoscar - 51CTO技术博客](http://4526621.blog.51cto.com/4516621/1597570)



[JavaScript开发工具WebStorm教程：用户界面简介](https://www.evget.com/article/2013/6/24/19100.html "JavaScript开发工具WebStorm教程：用户界面简介-控件新闻-慧都控件网")

[Introduction - webstorm 入门指南](http://book.apebook.org/minghe/webstorm/index.html "Introduction - webstorm 入门指南")








### Run/Debug Configurations

在某些工程，比如node.js项目中，run按钮是灰色的无法点击；这时候需要通过旁边的下拉按钮选择“Edit Configurations”来打开“Run/Debug Configurations”对话框来进行配置。

IDE自带了些默认的配置，在打开的对话框中点击左边的 “+” 会发现有很多种类的默认配置。这里以node.js为例，那么就选择"Node.js"，再为该配置文件起一个名字，然后在 JavaScript file 处指定要运行的 JavaScript文件。





### Usage Scope使用范围

[JavaScript. Usage Scope - Help  WebStorm](https://www.jetbrains.com/help/webstorm/javascript-usage-scope.html)

使用此对话框定义JavaScript库应用于代码补全、高亮显示和导航的范围。范围可能涵盖整个项目，目录甚至个别文件。这有助于使JavaScript的代码补全更精确，并避免太长的建议列表。

| Item           | Description                              |
| -------------- | ---------------------------------------- |
| File/Directory | This column displays the project tree view. |
| Library        | This column displays libraries for a file or directory, if applicable.If a library can be specified for a certain node of the project tree view, click the Library column for a selected file or directory, and choose the desired library from the list of available libraries.If JavaScript libraries are not applicable to a particular node, 'N/A' is shown in grey font.    ( If JavaScript libraries are not applicable to a particular node, 'N/A' is shown in grey font. ) |





### 设置 JavaScript 语言版本

设置 JavaScript 语言版本 ：File -> Setting -> Languages & Frameworks -> JavaScript ，选择语言版本。



**在本地运行js文件**，右键点击 `run **.js`。事先需要安装好node.js并在webstorm中进行配置（File -> Setting -> Languages & Frameworks -> node.js）



### 打开内嵌的终端

 open the built-in WebStorm Terminal 

press `Alt+F12` （不管用）or choose `View > Tool Windows > Terminal` （可以打开）on the main menu。



### 添加对jQuery的支持

项目中添加对jQuery的支持。

`File -> settings -> Javascript Libraries -> Add`

在files中添加路径，在documentations urls中添加文档支持。这里边需要注意一下的是，要添加原始未压缩的代码，`*.min.js`版的方法是不会被提示。

添加完成后，右边菜单中还有一 download 按钮，单击之后，他会自动选择最新版的js库进行搜索，然后在弹出的列表中，再单击选择一个后，点击Download and Install之后，才会被下载。这块体验不是太好，没有checkbox，也没有radio，只是选中后整行变暗。 

如果添加多个版本的jQuery，就可以直观的看到各个版本之间新方法的差别了。

\* 在这项的子菜单中 Usage Scope 右边 Project 第二栏Library下单击，选择新添加的jQuery，使其对整个项目进行覆盖。



### Vue.js支持

WebStorm默认已经支持Vue.js，请确保 Vue.js 插件处于开启状态。

额外设置：

[intellij idea - How to integrate WebStorm with Vue.js - Stack Overflow](https://stackoverflow.com/questions/36929395/how-to-integrate-webstorm-with-vue-js "intellij idea - How to integrate WebStorm with Vue.js - Stack Overflow")


**Improve HTML-tag's attributes highlighting**

Open `Settings(Preferences)` => `Editor` => `Inspection` => `HTML` => select `Unknown HTML tag attributes` => click `Custom HTML tag attributes`. Add your attributes.

For example, my list:

```
v-on,v-on:click,v-on:change,v-on:focus,v-on:blur,v-on:keyup,:click,@click,v-model,v-text,v-bind,:disabled,@submit,v-class,:class,v-if,:value,v-for,scoped,@click.prevent,number,:readonly,@input,@click,v-show,v-else,readonly,v-link,:title,:for,tab-index,:name,:id,:checked,transition,@submit.prevent,autocapitalize,autocorrect,slot,v-html,:style
```



### Node.js支持

**Enable Node.js Coding Assistance:**

Open `Settings(Preferences)` => `Languages & Frameworks` => `Node.js and NPM`



> If "Node.js core library is not enabled", click button `Enabled`
>
> [Node.js - Help ](https://www.jetbrains.com/help/webstorm/node-js.html )



Node interperter(解释器)： node安装路径。（还不知道是否是这样设置）

Coding Assistance：点击 enable 来下载Node.js的 。如有必要再点击 Usage scope(使用范围)。

[前端开发利器webStorm 3.0配置使用 - 豪情 - 博客园](http://www.cnblogs.com/jikey/archive/2012/01/16/2323590.html "前端开发利器webStorm 3.0配置使用 - 豪情 - 博客园")





[WebStorm开发工具设置React Native智能提示 - CSDN博客](http://blog.csdn.net/xiangzhihong8/article/details/52224527 "WebStorm开发工具设置React Native智能提示 - CSDN博客")





## 一些技巧

* 可以直接拖动文件到编辑器中。比如引入jquery.js，我们先将该文件添加到项目中，再直接拖动该文件到html文档中就会直接生成类似下面的语句`<script src="../build/jquery.js"></script>`。
* 善用“Settings”对话框中的**搜索**功能（直接搜索相关设置）。







## PyCharm

PyCharm有免费社区版。PyCharm Community Edition



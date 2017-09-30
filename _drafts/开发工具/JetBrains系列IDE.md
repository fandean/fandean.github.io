

## 激活



### 通过授权服务器激活



[JetBrains激活](http://www.imsxm.com/jetbrains-license-server.html "JetBrains激活 - 成都没有派对")

JetBrains 授权服务器(License Server URL): http://idea.imsxm.com

**使用方法：** 激活时选择License server 填入 `http://idea.imsxm.com`  点击Active即可。

**在线激活有一个过期时间**，这个时间一过就必须再次联网授权服务器请求激活。





## 同步设置


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




## PyCharm

PyCharm有免费社区版。PyCharm Community Edition





## WebStorm

WebStorm 是收费软件，不过这不是大问题，我们有一些免费使用的方案：



[WebStorm，你一直在寻找的前端开发 IDE · Issue #6 · cssmagic/blog](https://github.com/cssmagic/blog/issues/6 "WebStorm，你一直在寻找的前端开发 IDE · Issue #6 · cssmagic/blog")

官方下载的版本都是可以 30 天免费试用的。到期之后还可以继续安装更新的 **EAP** 预览版  <http://confluence.jetbrains.com/display/WI/WebStorm+EAP>  ，继续合法免费试用。只要自己勤快一点儿，备份好个人设置，基本上可以一直免费用下去。所以，我完全不建议你去找什么破解版或盗版序列号。

好像该方法不管用了。



[【程序员小助手】免费获得WebStorm正式版 - 程序员联盟 frogoscar - 51CTO技术博客](http://4526621.blog.51cto.com/4516621/1597570)



[JavaScript开发工具WebStorm教程：用户界面简介](https://www.evget.com/article/2013/6/24/19100.html "JavaScript开发工具WebStorm教程：用户界面简介-控件新闻-慧都控件网")

[Introduction - webstorm 入门指南](http://book.apebook.org/minghe/webstorm/index.html "Introduction - webstorm 入门指南")



### 设置 JavaScript 语言版本

设置 JavaScript 语言版本 ：File -> Setting -> Languages & Frameworks -> JavaScript ，选择语言版本。



在本地运行js文件，右键点击 `run **.js`。事先需要安装好node.js并在webstorm中进行配置（File -> Setting -> Languages & Frameworks -> node.js）



### 打开内嵌的终端

 open the built-in WebStorm Terminal 

press `Alt+F12` （不管用）or choose `View | Tool Windows | Terminal` （可以打开）on the main menu。



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










## 一些技巧

可以直接拖动文件到编辑器中。比如引入jquery.js，我们先将该文件添加到项目中，再直接拖动该文件到html文档中就会直接生成类似下面的语句`<script src="../build/jquery.js"></script>`。






# React Native

标签（空格分隔）： Android

---

[React Native](https://facebook.github.io/react-native/)
[React Native 中文网](https://reactnative.cn/)

找到工作后再考虑是否需要学习 React Native。

[ReactNative基础与入门教程-慕课网](http://www.imooc.com/learn/808 "ReactNative基础与入门教程-慕课网")

慕课网的 [ReactNative开发跨平台GitHub App](http://coding.imooc.com/class/89.html) 是一套不错的付费视频教程。



## 开发环境搭建



需要安装：

- Node.js：nodejs分为了长期支持版和当前版本。安装方法： [官网](https://nodejs.org/en/download/) 下载压缩包解压到`/opt`目录，修改解压目录的所属用户和组，然后配置环境变量（推荐）；或者参考：[How to Install Latest Nodejs &amp; NPM on Ubuntu with PPA - TecAdmin](https://tecadmin.net/install-latest-nodejs-npm-on-ubuntu/# "How to Install Latest Nodejs &amp; NPM on Ubuntu with PPA - TecAdmin")
- React Native Cli：直接通过 `npm install -g react-native-cli` 安装
- 配置 npm 的国内镜像站点为：`https://registry.npm.taobao.org` 。步骤：在HOME目录新建`.npmrc`文件并添加 `registry = https://registry.npm.taobao.org` 


运行 `react-native -h`查看帮助，运行`react-native init 项目名称` 初始化一个项目。此时会下载一些组件到 `~/.npm` 目录。



项目初始化好之后会提示：

```shell
To run your app on iOS:
   cd /tmp/FirstApp
   react-native run-ios
   - or -
   Open ios/FirstApp.xcodeproj in Xcode
   Hit the Run button
To run your app on Android:
   cd /tmp/FirstApp
   Have an Android emulator running (quickest way to get started), or a device connected
   react-native run-android
```

我们选择：To run your app on Android。先确保打开了Android虚拟机或连接手机并打开了开发者模式

切换到项目根目录，运行命令：`react-native run-android`，来构建并安装该 app 到手机或模拟器。

运行此命令还将会开启一个JS server，会有如下提示：`Starting JS Server ...` 如果该server被关闭，可以通过在该目录下运行 `npm start `开启该 server。



弹出错误：

```
FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:mergeDebugResources'.
> Error: java.util.concurrent.ExecutionException: java.lang.RuntimeException: AAPT process not ready to receive commands

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output.

BUILD FAILED

```



也可通过Android Studio以项目的方式打开该项目下的 android 目录，进行编译安装。



错误：

终端错误提示：

```
[fan 23:42:01]/tmp/FirstApp$ npm start

> FirstApp@0.0.1 start /tmp/FirstApp
> node node_modules/react-native/local-cli/cli.js start

Scanning 557 folders for symlinks in /tmp/FirstApp/node_modules (16ms)
 ┌────────────────────────────────────────────────────────────────────────────┐ 
 │  Running packager on port 8081.                                            │ 
 │                                                                            │ 
 │  Keep this packager running while developing on any JS projects. Feel      │ 
 │  free to close this tab and run your own packager instance if you          │ 
 │  prefer.                                                                   │ 
 │                                                                            │ 
 │  https://github.com/facebook/react-native                                  │ 
 │                                                                            │ 
 └────────────────────────────────────────────────────────────────────────────┘ 
Looking for JS files in
   /tmp/FirstApp 


React packager ready.

Loading dependency graph, done.
Bundling `index.android.js`  [development, non-minified, hmr disabled]  0.0% (0/1), failed.
error: bundling failed: "TransformError: /tmp/FirstApp/index.android.js: Unexpected token ) (While processing preset: \"/tmp/FirstApp/node_modules/babel-preset-react-native/index.js\")"
error: bundling failed: "TransformError: /tmp/FirstApp/index.android.js: Unexpected token ) (While processing preset: \"/tmp/FirstApp/node_modules/babel-preset-react-native/index.js\")"

```



开启的APP中的错误提示：

```
The development server returned response error code: 500

URL: http://10.0.3.2:8081/index.android.bundle?platform=android&dev=true&hot=false&minify=false

Body:
{"message":"TransformError: /tmp/FirstApp/index.android.js: Unexpected token ) (While processing preset: \"/tmp/FirstApp/node_modules/babel-preset-react-native/index.js\")","type":"TransformError","lineNumber":0,"description":"","errors":[{"description":"","lineNumber":0}]}
processBundleResult
    BundleDownloader.java:170
access$100
    BundleDownloader.java:39
onResponse
    BundleDownloader.java:139
execute
    RealCall.java:135
run
    NamedRunnable.java:32
runWorker
    ThreadPoolExecutor.java:1133
run
    ThreadPoolExecutor.java:607
run
    Thread.java:761

```









> 参考：[将Ubuntu, RubyGems, NPM和PyPI的源更换为国内镜像 – 思诚之道](http://www.bjhee.com/source-mirror.html "将Ubuntu, RubyGems, NPM和PyPI的源更换为国内镜像 – 思诚之道")





## 开发工具



 WebStom：免去下载各种插件的烦恼。










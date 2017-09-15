

## npm介绍





包管理器(Package Manager)

npm 在不断的升级，最初它只是被称为 Node Package Manager，用来解决Node.js的包管理器。但是随着其它构建工具(webpack、browserify)的发展，npm已经变成了 "the package manager for JavaScript"，它用来安装、管理和分享JavaScript包，同时会自动处理多个包之间的依赖。

## 安装npm

新版的nodejs已经集成了npm

Node.js：nodejs分为了**长期支持版**和**当前版本**。

Linux中安装nodejs的方法：

*  [官网](https://nodejs.org/en/download/) 下载压缩包解压到`/opt`目录，修改解压目录的所属用户和组，然后配置环境变量（推荐）；
*  或者使用PPA安装：[How to Install Latest Nodejs &amp; NPM on Ubuntu with PPA - TecAdmin](https://tecadmin.net/install-latest-nodejs-npm-on-ubuntu/# "How to Install Latest Nodejs &amp; NPM on Ubuntu with PPA - TecAdmin")





## 升级现有npm版本

```javascript
npm install npm -g
```






## 更换 npm 镜像站点

对于国内的情形，在使用npm安装JS包之前建议先更改npm的镜像。

配置 npm 的国内镜像站点为：`https://registry.npm.taobao.org` 。

方法一：在系统的HOME目录新建`.npmrc`文件并添加 `registry = https://registry.npm.taobao.org` 

方法二：你可以使用淘宝定制的 cnpm 命令行工具代替默认的 npm:

```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
//之后即可使用cnpm来安装包
cnpm install <包>
```



> 详情请参考： [淘宝 NPM 镜像](https://npm.taobao.org/ "淘宝 NPM 镜像")



## 本地安装(默认)

npm 的包安装分为本地安装（local）、全局安装（global）两种。


```shell
npm install <包>      # 本地安装
# 或者
npm i <包>
```



- 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
- 可以通过 require() 来引入本地安装的包。





## 全局安装

```shell
npm install <包> -g   # 全局安装
```



- 将安装包放在 /usr/local 下或者你 node 的安装目录。
- 可以直接在命令行里使用。**这是使用全局安装的主要原因**。



使用下面的命令来查看全局的包安装的位置：

```javascript
npm prefix -g
```


## 创建全局链接


如果你希望具备两者功能（本地安装和全局安装的功能），则需要在两个地方安装它或使用 **npm link**。


npm link的功能是在本地包和全局包之间创建符号链接。我们说过使用全局模式安装的包不能直接通过 require 使用,但通过 npm link 命令可以打破这一限制。

比如我们将 express安装到了全局环境，使用下面的命令可以将其链接到本地环境：
```
npm link express
```

使用 npm link命令还可以将本地的包链接到全局。使用方法是在包目录( package.json 所在目录)中运行 `npm link` 命令。



> 像gem 或 pip 总是以全局模式安装，使包可以供所有的程序使用，而 npm 默认会把包安装到当前目录下。这反映了 npm 不同的设计哲学。如果把包安装到全局，可以提高程序的重复利用程度,避免同样的内容的多份副本，但坏处是难以处理不同的版本依赖。




## 常用命令

### 查看命令帮助

```shell
npm help <某命令>
```






### 查看安装信息

```shell
//全局安装信息
npm ls -g

//列出当前项目中的包
npm ls
```



### 卸载包

```shell
npm uninstall <包名>
```



### 更新包

```shell
//更新当前项目中安装的包
npm update <包名>

//更新全局安装的包
npm update <包名> -g
```



### 搜索包

```shell
npm search <关键字>
```





npm start

npm stop





## 使用 package.json



当你的项目需要依赖多个包时，推荐使用 package.json。其优点为：

* 它以文档的形式规定了项目所依赖的包
* 可以确定每个包所使用的版本
* 项目的构建可以重复，在多人协作时更加方便




### 创建package.json文件



- 手动创建
- 或者 通过 npm init 命令填入各种信息



文件中必须包含： name 和 version



### 指定依赖包

两种依赖包：

* dependencies: 在生产环境中需要依赖的包。通过`npm install <packge> --save`命令自动添加依赖到文件。
* devDependencies：仅在开发和测试环节中需要依赖的包。通过`npm install <packge> --save-dev`命令自动添加依赖到文件。

> 当然你也可以在文件中手动添加依赖



如果其他人也需要这个项目，只需要把这个 package.json 文件给他，然后进行简单的 `npm install` 即可。



## 发布包

在发布之前,首先需要让我们的包符合 npm 的规范,npm 有一套以 CommonJS 为基础包规范,但与 CommonJS并不完全一致,其主要差别在于必填字段的不同。通过使用 `npm init` 可以根据交互问答产生一个符合标准的 package.json。 

npm init 运行示例：

```
$ npm init
name: (node) test
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /tmp/node/package.json:

{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this ok? (yes) 

```

该文件就是一个符合 npm 规范的 package.json 文件。这里的 index.js 作为包的接口。



创建帐号： 

```shell
npm adduser
```

测试是否取得帐号：

```shell
npm whoami
```

发布

```shell
npm publish
```

更新包：修改 version字段，再重新发布

取消发布：

```shell
npm unpublish
```





## npm 脚本

[npm scripts 使用指南 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html "npm scripts 使用指南 - 阮一峰的网络日志")





## npm模块安装机制

[npm 模块安装机制简介 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/01/npm-install.html "npm 模块安装机制简介 - 阮一峰的网络日志")





## 学习资料

[NPM 使用介绍 - 菜鸟教程](http://www.runoob.com/nodejs/nodejs-npm.html "NPM 使用介绍 - 菜鸟教程")

[npm Documentation](https://docs.npmjs.com/ "npm Documentation")







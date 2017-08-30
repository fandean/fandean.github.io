

## Node.js



通过这里快速了解：

[NPM 使用介绍 - 菜鸟教程](http://www.runoob.com/nodejs/nodejs-npm.html "NPM 使用介绍 - 菜鸟教程")



### npm

[NPM 使用介绍 - 菜鸟教程](http://www.runoob.com/nodejs/nodejs-npm.html "NPM 使用介绍 - 菜鸟教程")

新版的nodejs已经集成了npm

npm 的包安装分为本地安装（local）、全局安装（global）两种

```javascript
npm install express      # 本地安装
npm install express -g   # 全局安装
```

 本地安装

- 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
- 可以通过 require() 来引入本地安装的包。

 全局安装

- 将安装包放在 /usr/local 下或者你 node 的安装目录。
- 可以直接在命令行里使用。

如果你希望具备两者功能，则需要在两个地方安装它或使用 **npm link**。



> require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。
>
> 通过 requier()引入本地安装包的示例：
>
> ```javascript
> var express = require('express');
> ```
>
> 通过requier()引入本地文件
>
> ```javascript
> # 当前路径存在一个 hello.js文件，这里我们将其引入
> var hello = require('./hello');
> ```
>
> 在开发 React 时也可能看到。





#### 查看安装信息

```shell
$ npm list -g

```




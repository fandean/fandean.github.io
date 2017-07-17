---
layout: post
title: "VS Code"
description: "VS Code"
date: 2017-07-17
tags: 
category: 
last_updated: 2017-07-17
comments: true
chare: true
---

* Kramdown table of contents
{:toc .toc}


# VS Code使用笔记

## 学习文档
[VScode中文文档](https://www.gitbook.com/book/jeasonstudio/vscode-cn-doc/details)  
[VS Code Tips and Tricks](https://github.com/Microsoft/vscode-tips-and-tricks)  
[Visual Studio Code 配置指南](https://github.com/kaiye/kaiye.github.com/issues/14 "强烈推荐")  
[Key Bindings for Visual Studio Code](https://github.com/kaiye/kaiye.github.com/issues/14)  

查看VS Code的自带帮助，来学习它。比如： `帮助 --> 欢迎使用`

[Visual Studio Code User and Workspace Settings](https://code.visualstudio.com/docs/getstarted/settings "Visual Studio Code User and Workspace Settings")

[Microsoft/vscode-tips-and-tricks: Collection of helpful tips and tricks for VS Code.](https://github.com/Microsoft/vscode-tips-and-tricks "Microsoft/vscode-tips-and-tricks: Collection of helpful tips and tricks for VS Code.")

## User Guide  
[Basic Editing in Visual Studio Code](https://code.visualstudio.com/docs/editor/codebasics "Basic Editing in Visual Studio Code")

### Multiple selections (multi-cursor)

使用 `Shift+Alt+Down`或`Shift+Alt+Up`达到下图效果：       

![](https://code.visualstudio.com/images/editingevolved_multicursor.gif)

> 使用下文的扩选操作，再使用此处的快捷键，会有意想不到的效果。



先选中某单词，再按`Ctrl+D`达到下图效果：    

![](https://code.visualstudio.com/images/editingevolved_multicursor-word.gif)


### Shrink/expand selection

扩大选中区域：

- 每次扩选一个单词：`Ctrl+Shift+L`
- 每次扩选一行：`Shift+Alt+Left`或`Shift+Alt+Right`  

![](https://code.visualstudio.com/images/editingevolved_expandselection.gif)

### Column (box) selection

通过 `Shift+Alt+鼠标拖动`，实现下面的效果：     

![](https://code.visualstudio.com/images/editingevolved_column-select.gif)



### 命令面板

通过`ctrl + p`或 `F1` 弹出的对话框叫“命令面板”

打开命令面板有多个快捷键，它们的区别是:

- `ctrl + shift + p` 和 `F1`：打开命令面板时会带有 `>`
- `ctrl + p`: 打开命令面板时没有 `>`

由于快捷键冲突而导致无法触发相应插件，解决方法之一是直接在命令面板中操作。

```
> 显示并执行命令
? 获取帮助
```

如果一个文件夹中包含的文件较多，使用命令面板寻找并打开文件是不错的选择。



## 设置

### 保存/自动保存

VS Code能很容易开启自动保存，在你配置延迟后或者焦点离开编辑器后自动保存你的更改文件

打开 User Setting 或者 Workspace 配置自动保存，找到如下相关设置：

files.autoSave ：设置值为off表示关闭自动保存，afterDelay 保存文件后延迟自动保存，onFocusChange 焦点移出编辑器后就会自动保存。
files.autoSaveDelay ： files.autoSave 的值是 afterDelay 时，就可以设置自动保存的延迟时间。




## VS Code插件
[Visual Studio Code的C/C++扩展功能](https://blogs.msdn.microsoft.com/c/2016/04/18/visual-studio-code%E7%9A%84cc%E6%89%A9%E5%B1%95%E5%8A%9F%E8%83%BD/)  



#### Evernote

Open and Save Evernote notes from VS Code using Markdown



#### Image preview
Shows image preview in the gutter and on hover.

支持鼠标悬停显示图片。



#### TranslationToolbox

翻译

使用快捷键 ctrl+alt+t or cmd+alt+t 启用TranslationToolbox扩展
选中想要翻译的文本，并将鼠标移至其上，即可显示翻译结果

#### Translator Plus
使用Google翻译，在状态栏显示翻译结果。很棒

但由于网络时好时坏，可能会显示"Waiting..."

#### Google Complete Me

Auto completion using Google Suggesting API.

国内还是使用不畅。


#### Dictionary Completion

word completion

Enabled for Markdown and LaTeX. 但是需要先配置以支持markdown等，见插件主页。





### 文件头
#### header source



#### File-Header-Comment Helper for Visual Studio Code

Insert File-Header-Comment

```json
    "fileHeaderCommentHelper.languageConfigs": {
        "language_markdown": { //指定语言比如 language_javascript
            "template": [
                "---",
                "layout: post",
                "title: \"$(currentFile)\"",
                "description: \"$(currentFile)\"",
                "date: 2017-",
                "tags: []",
                "category: ",
                "comments: true",
                "share: true",
                "---",
                "\n\n\n",
                "* Kramdown table of contents",
                "{:toc .toc}"
            ]
        }
    }
```



#### vscode fileheader

添加文件头，自动更新文件修改时间。


#### psioniq File Header
添加文件头，自动更新文件修改时间。

很棒的插件

[psioniq File Header - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=psioniq.psi-header "psioniq File Header - Visual Studio Marketplace")



#### EditorConfig for VS Code


#### Path Intellisense

自动补全路径


#### Project Manager

可以保存工程和在工程间切换

先将当前打开的文件夹以工程保存，之后就可以在命令面板中列出并打开。

#### vscode-icons

~~为文件和文件夹添加图标~~。vs code已经自带

> NOTE 微软官方已经集成了图表,使用”File Icon Theme”就可更改.

#### vscode-youcompleteme

与VIM中的类似。


#### Auto Rename Tag

![](https://github.com/formulahendry/vscode-auto-rename-tag/raw/master/images/usage.gif)


#### Auto Close Tag


### git相关插件

#### Git History(git log)
Open the file to view the history, and then Press F1 and select/type "Git: View History (git log)", "Git: View File History" or "Git: View Line History".







### Markdown相关插件

#### Markdown Preview Enhanced
预览效果不错，功能强。但就是有时会预览不成功，不知是何原因。

使用快捷键`ctrl + shift + m`预览。或输入`ctrl + shift + p`再输入 mpv 选择执行相关命令。


#### preview


#### markdown Shortcuts
功能很强的编辑markdown文件的辅助工具。


#### Markdown PasteUrl




#### Paste Image
> Linux系统需安装后xclip。该程序用于复制terminal内容到剪切板。

Paste image directly from clipboard to markdown(or other file)!

使用方法：   
先将图片保存到剪切板    
F1  然后输入  paste image   


[Paste Image](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image "Paste Image - Visual Studio Marketplace")

![](https://raw.githubusercontent.com/mushanshitiancai/vscode-paste-image/master/res/vscode-paste-image.gif)

自定义图片保存位置。

Config Example见插件的示例。

```json
//Paste Image Configration：涉及到图片本地保存路径和文件中图片url路径
//图片保存路径
"pasteImage.path": "${projectRoot}/assets/images/post-images",
"pasteImage.basePath": "${projectRoot}",
"pasteImage.forceUnixStyleSeparator": true,
"pasteImage.prefix": "/",
```


#### Jekyll Snippets


#### vscode-hexo
VSCode extension to manage hexo commands.

貌似也可以自己配置任务来管理jekyll。

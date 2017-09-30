## Bootstrap介绍

Bootstrap 来自 Twitter，是 2011 年八月在 GitHub 上发布的开源产品。

用于为小型站点开发响应式网站；对于像淘宝等复杂页面并不适合，为其重新创建专门用于移动端的页面可能更加简单。



> Bootstrap可视化布局工具



Bootstrap 的 JavaScript 插件需要引入 jQuery。所以需要与JQuery一起使用。

自 Bootstrap 3 起，框架包含了贯穿于整个库的**移动设备优先**的样式。



* Bootstrap 使用了一些 HTML5 元素和 CSS 属性。为了让这些正常工作，您需要使用 HTML5 文档类型（Doctype）。
* 为了让 Bootstrap 开发的网站对移动设备友好，确保适当的绘制和触屏缩放，需要在网页的 head 之中添加 **viewport meta** 标签





> *responsive*：响应



> Bootstrap 使用 [Normalize](http://necolas.github.io/normalize.css/) 来建立跨浏览器的一致性。
>
> Normalize.css 是一个很小的 CSS 文件，在 HTML 元素的默认样式中提供了更好的跨浏览器一致性。



**响应式图像：**

```html
<img src="..." class="img-responsive" alt="响应式图像">
```



**容器：**

```html
<div class="container">
  ...
</div>
```

Bootstrap 3 的 *container* class 用于包裹页面上的内容。

请注意，由于内边距（padding）是固定宽度，默认情况下容器container是不可嵌套的。



## Bootsrap网格系统

Grid System(网格系统，栅格系统)。Bootstrap 提供了一套响应式、移动设备优先的流式网格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。



### Grid System工作原理



网格系统通过一系列**包含内容的**行和列来创建页面布局。

* 行必须放置在 **.container** class 内，以便获得适当的对齐（alignment）和内边距（padding）。
* 使用行来创建列的水平组。
* **内容应该放置在列内**，且唯有列可以是行的直接子元素。
* 预定义的网格类，比如 **.row** 和 **.col-xs-4**，可用于快速创建网格布局。LESS 混合类可用于更多语义布局。
* 列通过内边距（padding）来创建列内容之间的间隙。该内边距是通过 **.rows** 上的外边距（margin）取负，表示第一列和最后一列的行偏移。
* 网格系统是通过指定您想要横跨的十二个可用的列来创建的。例如，要创建三个相等的列，则使用三个 **.col-xs-4**。






### 网格选项

下表总结了 Bootstrap 网格系统如何跨多个设备工作：

|          | 超小设备手机（<768px）      | 小型设备平板电脑（≥768px）    | 中型设备台式电脑（≥992px）    | 大型设备台式电脑（≥1200px）   |
| -------- | ------------------- | ------------------- | ------------------- | ------------------- |
| 网格行为     | 一直是水平的              | 以折叠开始，断点以上是水平的      | 以折叠开始，断点以上是水平的      | 以折叠开始，断点以上是水平的      |
| 最大容器宽度   | None (auto)         | 750px               | 970px               | 1170px              |
| Class 前缀 | **.col-xs-**        | **.col-sm-**        | **.col-md-**        | **.col-lg-**        |
| 列数量和    | 12                  | 12                  | 12                  | 12                  |
| 最大列宽     | Auto                | 60px                | 78px                | 95px                |
| 间隙宽度     | 30px（一个列的每边分别 15px） | 30px（一个列的每边分别 15px） | 30px（一个列的每边分别 15px） | 30px（一个列的每边分别 15px） |
| 可嵌套      | Yes                 | Yes                 | Yes                 | Yes                 |
| 偏移量      | Yes                 | Yes                 | Yes                 | Yes                 |
| 列排序      | Yes                 | Yes                 | Yes                 | Yes                 |







### 基本的网格结构

```html
<div class="container">
   <div class="row">
      <div class="col-*-*"></div>
      <div class="col-*-*"></div>      
   </div>
   <div class="row">...</div>
</div>
<div class="container">....
```









## 学习资料


[Bootstrap中文网](http://www.bootcss.com/ "Bootstrap中文网")

[印记中文 - 最权威的中文开发文档](https://docschina.org/ "印记中文 - 最权威的中文开发文档")



[Bootstrap响应式网站开发 移动端手机站制作视频教程_腾讯课堂](https://ke.qq.com/course/228137)

[Bootstrap前端框架_腾讯课堂](https://ke.qq.com/course/191050 "Bootstrap前端框架_腾讯课堂")

[Bootstrap 教程 - 菜鸟教程](http://www.runoob.com/bootstrap/bootstrap-tutorial.html "Bootstrap 教程 - 菜鸟教程")





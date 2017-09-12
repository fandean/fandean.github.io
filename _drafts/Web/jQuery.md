

《JQuery基础教程(第4版)》

[jQuery 教程 - 菜鸟教程](http://www.runoob.com/jquery/jquery-tutorial.html "jQuery 教程 - 菜鸟教程")





## jQuery介绍



jQuery核心特性：

* 取得文档中的元素：

  ```javascript
  $('div.content').find('p');
  ```

* 修改页面的外观：提供跨浏览器的解决方案

  ```javascript
  $('ul > li:first').addClass('active');
  ```

* 改变文档的内容：

  ```javascript
  $('#container').append('<a href="more.html">more</a>');
  ```

* 响应用户的交互操作：消除浏览器的不一致性

  ```javascript
  $('button.show-details').click(function(){
  	$('div.details').show();
  });
  ```

* 为页面添加动态效果：jQuery中内置了一批淡入、擦除之类的效果，以及制作新效果的工具包

  ```javascript
  $('div.details').slideDown();
  ```

* 无需刷新页面从服务器获取信息：消除浏览器的不一致性

  ```javascript
  $('div.details').load('more.html #content');
  ```

* 简化场景的JavaScript任务：

  ```javascript
  $.each(obj, function(key, value){
     total += value; 
  });
  ```

  ​



jQuery采用的策略：

* 利用CSS的已有优势。通过将查找页面元素的机制构建于CSS选择符之上。
* 支持扩展。为了避免特性蠕变(feature creep)1,jQuery将特殊情况下使用的工具归入插件当中。
* 抽象浏览器的不一致性。
* **总是面向集合**。.hide() 之类的方法被设计成自动操作对象集合,而不是单独的对象。利用这种称作隐式迭代(implicit iteration)的技术,就可以抛弃那些臃肿的循环结构,从而大幅地减少代码量。
* 将多重操作集于一行。



下载jQuery：

开发时使用未压缩版；正式发布时使用压缩版。或者利用CDN(内容分发网络)。

下载最新版本，然后将其重命名为 jquery.js 。

**注意**：引用jQuery库文件的<script>标签,必须放在引用自定义脚本文件的<script>标签之前。否则,在我们编写的代码中将引用不到jQuery框架。



通常，JavaScript代码在浏览器初次遇到它们时就会执行(当然，当有一个函数，只有我们在代码中调用时它才会执行)，而在浏览器处理头部时,HTML还不会呈现样式。因此,我们需要将代码延迟到DOM可用时再执行。

通过使用`$(document).ready()`方法, jQuery支持我们预定在DOM加载完毕后调用某个函数，而不必等待页面中的图像加载。



jQuery 语法是通过选取 HTML 元素，并对选取的元素执行某些操作。

基础语法： `$(selector).action()`



为了创建jQuery对象,就要使用`$()`函数。通常，该函数需要一个**字符串参数**，参数中可以包含**任何CSS选择符表达式**。 该函数会返回一个新的jQuery对象实例。jQuery对象中会封装零个或多个DOM元素,并允许我们以多种不同的方式与这些DOM元素进行交互。





## 选择元素

有三种基本的选择符：标签名，ID和类。

还有jQuery独有的完全不同的自定义选择符。



### 自定义选择符

但是其查找速度就会变慢。

自定义选择符通常跟在一个CSS选择符后面,基于已经选择的元素集的位置来查找元素。自定义选择符的语法与CSS中的伪类选择符语法相同,即选择符以冒号( :)开头。比如(`:eq()`)

> 注意：JavaScript数组采用从0开始的编号方式。而CSS时从1开始的。



示例：每隔一行为表格添加样式

通过两个非常有用的选择符：`:odd`(奇数)和`:even`(偶数)。注意这里奇偶是说数组(集合)的下标。

`:nth-child()`选择符：该选择符相对于元素的父元素而非当前选择的所有元素来计算位置。



基于上下文的内容选择元素：`:contains()`选择符

```javascript
$(document).ready(function() {
	$('tr:nth-child(odd)').addClass('alt');
	$('td:contains(Henry)').addClass('highlight');
});
```



基于表单的选择符：略



### DOM遍历方法

取得某个元素的父元素或者祖先元素都是基本的操作，而这正是jQuery的DOM遍历方法的用武之地。

`.filter()`筛选方法

`.next()`方法：只选择下一个最接近的同辈元素。

`.nextAll()`，`.prev()`，`.prevAll()`。

`.siblings()`能够选择处于相同DOM层次的所有其他元素，无论这些元素处于当前元素之前还是之后。

`.addBack()` 

`.parent()`，`.children()`



> 方法连缀的原理：几乎所有的jQuery方法都会返回一个jQuery对象。



### 访问DOM元素

使用场景：可能需要为另一个JavaScript库提供一组元素的结果集合。

为此jQuery提供了 `.get()`方法。比如 .get(0)，表示要访问jQuery对象所引用的第一个DOM元素，可以使用.get(0)。

jQuery为 .get() 方法提供了一种简写方式。比如 .get(0) 可以写成 [0]。



## 事件

让jQuery响应网页的加载事件,`$(document).ready()`事件处理程序可以用来触发函数中的代码。原生的window.onload事件也可以实现相同的效果。但是,它们在触发操作的时间上存在着微妙的差异,这种差异只有在加载的资源多到一定程度时才会体现出来。

当文档完全下载到浏览器中时,会触发window.onload事件。

通过 `$(document).ready()` 注册的事件处理程序,则会在DOM完全就绪并可以使用时调用。虽然这也意味着所有元素对脚本而言都是可以访问的,但是,**却不意味着**所有关联的文件都已经下载完毕。换句话说,当HTML下载完成并解析为DOM树之后,代码就可以运行。



> 为了保证JavaScript代码执行以前页面已经应用了样式,最好是在`<head>`
> 元素中把 `<link rel="stylesheet">` 标签和`<style>` 标签放在 `<script>`标
> 签前面。







## 样式与动画





## 操作DOM





## 通过Ajax发送数据








推荐书籍：《CSS揭秘》这里有许多技巧。



你有两年以上的前端开发经验吗？你会用 Sass 和 Autoprefixer 等高级的CSS辅助技能吗？你的 JavaScript 知识是否融汇贯通，你是否喜欢使用 Gulp ， npm 和 jQuery ？如果是这样，根据 [Ashley Nolan 的前端问卷调查](https://ashleynolan.co.uk/blog/frontend-tooling-survey-2016-results)，你是一个典型的前端开发工程师。



虽然 CSS 是一个看似简单的 属性 和 值 的键值对集合，但是 CSS 是众所周知地难以掌握。 CSS3引入了一系列新效果，并且越来越难以掌握所有的知道。



### 7.CSS

#### CSS规则

```css
h1选择器 { /*声明块*/
	color:red;	/*声明*/
   /*属性：值*/
}
```



#### 理解继承

将html文档理解为文档树。文档树有助于理解CSS。

有些属性不可以被继承。详见书中列表。

对大多数属性来说，还可以使用inherit值强制进行继承。`p {border: inherit;}`





#### 层叠：当规则发生冲突时
CSS用层叠的原则来考虑**特殊性、顺序、和重要性**，从而判断相互冲突的规则中哪个规则应该起作用。

**特殊性：**
特殊性规则指定选择器的具体程度。选 择器越特殊,规则就越强。遇到冲突时,优 先应用特殊性强的规则。

**顺序：**
有时候,特殊性还不足以判断在相互冲突的规则中应该优先应用哪一个。在这种情况下,规则的顺序就可以起到决定作用:晚
出现的优先级高

**重要性:**
如果这还不够,可以声明一条特殊的规 则覆盖整个系统中的规则,这条规则的重要 程度要比其他所有规则高。也可以在某条声 明 的 末 尾 加 上 !important, 比 如 `p{ color: orange !important; }`

>一般记住特殊性就行了



#### 属性的值

继承值inherit值:`p {border: inherit;}`
预设值：`p {border: none;}`
长度和百分数：使用em和百分数指定相对长度值
CSS颜色：RGB和RGBA
HSL和HSLA：色相hue、饱和度saturation、亮度lightness


>em: 
>一个 em 的 长度大约与对应元素的字号相等。
>例如,对 元素设置 margin-left: 2em 就代表将元素的 左外边距设为元素字号的两倍。(当 em 用于 设置元素的 font-size 属性本身时,它的值继 承自对应元素的父元素的字号)

>px像素；pt磅。





## 操作样式表



**外部样式表(首选方法)**

在HTML页面的 head 部分,输入 `<link rel="stylesheet href="url.css" />`

> 浏览器可以缓存该文件。



**嵌入样式表**

在 head 部分创建一个 style 元素，其中包含了我们的样式表。

```html
# 在head中插入
<style>
  img {
      border:4px solid red;
  }
</style>
```





**内联样式(不可取)**

在某个 元素中加上 `style="border: 4px solid red"`，来为该元素设置样式。

```html
<img src="img/palau.jpg" width="250" height="163" alt="El Palau de la" 
     style = "border: 4px solid red"/>
```










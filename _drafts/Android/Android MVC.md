---
layout: post
title: "Android MVC架构"
description: "Android MVC架构"
date: 2017-08-01
tags: [Android,MVC]
category: Android
last_updated: 2017-08-02
comments: true
chare: true
---

* Kramdown table of contents
{:toc .toc}


## 参考


Google提供的三篇文章：  

- [Android Architecture Patterns Part 1: Model-View-Controller — upday tech blog](https://upday.github.io/blog/model-view-controller/ )
- [Android Architecture Patterns Part 2: Model-View-Presenter — upday tech blog](https://upday.github.io/blog/model-view-presenter/ )
- [Android Architecture Patterns Part 3:Model-View-ViewModel — upday tech blog](https://upday.github.io/blog/model-view-viewmodel/ ) 
- [MVVM — It’s All In The (Implementation) Details – upday devs – Medium](https://medium.com/upday-devs/mvvm-its-all-in-the-implementation-details-40ed24871a02)

并结合的了Google的提供的示例项目 googlesamples/android-architecture 

作者提供的小示例：

[florina-muntenescu/MVPvsMVVM: Model-View-Presenter vs Model-View-ViewModel in a "Hello, World!" project](https://github.com/florina-muntenescu/MVPvsMVVM )

[florina-muntenescu/DroidconMVVM: "Hello, World!" example of the Model-View-ViewModel pattern](https://github.com/florina-muntenescu/DroidconMVVM )



纸飞机： [重构！将Google MVP应用于已有项目 - Tonny's Blog](https://tonnyl.github.io/2016/09/27/%E9%87%8D%E6%9E%84%EF%BC%81%E5%B0%86Google-MVP%E5%BA%94%E7%94%A8%E4%BA%8E%E5%B7%B2%E6%9C%89%E9%A1%B9%E7%9B%AE/ "重构！将Google MVP应用于已有项目 - Tonny's Blog") 这里应用的是 todo-mvp。





这里介绍了几个架构的关键点：

[Android Architecture – AndroidPub](https://android.jlelse.eu/android-architecture-2f12e1c7d4db "Android Architecture – AndroidPub")



​最终看到此篇文章时，我都快激动的落泪了 :cry: (当前处境不好) 。

- [Android中的Model View Presenter MVP，第1部分](http://www.tinmegali.com/en/model-view-presenter-android-part-1/ "Android中的Model View Presenter MVP，第1部分")
- [Android中的Model View Presenter，第2部分](http://www.tinmegali.com/en/model-view-presenter-mvp-in-android-part-2/ "Android中的Model View Presenter，第2部分")
- [Model View Presenter (MVP) in Android, part 3](http://www.tinmegali.com/en/model-view-presenter-mvp-in-android-part-3/ "Model View Presenter (MVP) in Android, part 3")



[ 译 -Android MVP 架构必要知识：第一部分 - 知乎专栏](https://zhuanlan.zhihu.com/p/25272412)






## MVC架构

**模型**  - 数据层，负责管理业务逻辑和处理网络或数据库API。该模型表示一组描述业务逻辑的类，即业务模型以及数据访问操作，即数据模型。它还定义数据的业务规则意味着数据如何被更改和操纵。

**视图**  - UI层 - 来自Model的数据的可视化。仅负责显示从控制器接收到的数据。

**控制器**  - 逻辑层，被通知用户的行为，并根据需要更新模型。控制器负责处理传入的请求。它通过View接收用户的输入，然后在Model的帮助下处理用户的数据，并将结果传回给View。通常，它作为View和Model之间的协调器。

这意味着Controller和View都依赖于Model：Controller来更新数据，View可以获取数据。

> 早期，询问“如何在Android中应用MVC”等问题，最受欢迎的答案就是说，在Android中，Activity是View和Controller。在这一点上，主要的重点是使模型可测试。通常View和Controller的实现选择依赖平台。


## MVC应该如何应用于Android

现在，把**Activities**, **Fragments** 和 **Views** 作为视图， 控制器应该是不扩展或使用任何Android类的单独类，对于模型也是一样。


[Android体系结构模式第1部分：模型 - 视图 - 控制器](https://medium.com/upday-devs/android-architecture-patterns-part-1-model-view-controller-3baecef5f2b6 "Android体系结构模式第1部分：模型 - 视图 - 控制器")


将Controller连接到View时会出现一个问题，因为Controller需要告诉View更新。在被动型MVC架构中，Controller需要持有对View的引用。最简单的方法是在集中测试的同时，拥有一个BaseView接口，即Activity / Fragment / View将会扩展。所以，Controller会引用BaseView。


### 优点

模型 - 视图 - 控制器模式高度支持关注点的分离。这个优点不仅增加了代码的可测试性，而且还使得扩展更加容易，从而允许相当容易地实现新功能。

Model类没有任何对Android类的引用，因此直接进行单元测试。控制器不扩展或实现任何Android类，并且应该引用View的接口类。这样，控制器的单元测试也是可能的。

如果View遵循单一责任原则，那么他们的角色只是为每个用户事件更新控制器，并只显示模型中的数据，而不会实现任何业务逻辑。在这种情况下，UI测试应该足以覆盖View的功能。

### 缺点

#### View 取决于控制器和模型

视图对模型的依赖随着视图的复杂开始成为了缺点。为了最小化View中的逻辑，模型应该能够为要显示的每个元素提供可测试的方法。在一个有效的模型实现中，由于需要每种数据类型的观察者，因此这会以指数方式增加类和方法的数量。

鉴于View取决于Controller和Model，UI逻辑的变化可能需要在几个类中进行更新，从而降低了模式的灵活性。


#### 谁处理UI逻辑

According to the MVC pattern, the Controller updates the Model and the View gets the data to be displayed from the Model. 

但谁决定如何显示数据？ Is it the Model or the View? 

值得一看。


如果模型的作用是提供“原始”数据，则意味着视图中的代码将是：

```
String firstName = userModel.getFirstName();
String lastName = userModel.getLastName();
nameTextView.setText(lastName + ", " + firstName)
```
所以这意味着**View将负责处理UI逻辑**。但是这使得UI逻辑不可能进行单元测试。


另一种方法是使模型仅显示需要显示的数据，从视图中隐藏任何业务逻辑。
但是，我们最终得到了**处理业务**和**UI逻辑**的**模型**。它将是单位可测试的，但是模型最终会隐含地依赖于View。
```
String name = userModel.getDisplayName();
nameTextView.setText(name);
```



另一位大侠介绍的MVC：

![](https://cdn-images-1.medium.com/max/800/1*U6JRenliQAVEsdD7YZuv1g.png)



视图：  视图表示UI组件。因此，**仅负责显示**从控制器接收到的数据。这也将模型转换为UI。

控制器：控制器负责**处理传入的请求**。它通过View接收用户的输入，然后在Model的帮助下处理用户的数据，并将结果传回给View。通常，它作为View和Model之间的协调器。

**注意：**观察上图 用户与控制器的关系。



## MVP

The Model-View-Presenter Pattern 

- 模型 - 数据层。负责处理与网络和数据库层的**业务逻辑**和**通信**。
- View - UI层。显示数据并通知Presenter用户操作。
- Presenter - 从模型中检索数据，应用UI逻辑并管理视图的状态，决定从视图中显示和对用户输入通知做出的响应。


![](https://upday.github.io/images/blog/model_view_presenter/mvp.png)



### 模型

该模型与远程和本地数据源一起使用以获取和保存数据。这是处理业务逻辑的地方。

例如，当请求Tasks 的列表时，模型将尝试从本地数据源检索它们。如果为空，它将查询网络，将响应保存在本地数据源中，然后返回列表。

RxJava用于移除主线程并能够处理异步操作。

### 视图

该视图与Presenter一起显示数据，并通知Presenter用户的操作。在MVP活动中，片段和自定义Android视图可以是Views。我们的选择是使用片段。

所有视图实现相同的BaseView界面，允许设置Presenter。

```
public interface BaseView<T> {
    void setPresenter(T presenter);

}
```

### Presenter 

The Presenter and its corresponding View are created by the Activity.



演示者及其相应视图由活动创建。



在[模型-视图-控制器模式](https://upday.github.io/blog/model-view-controller/)有两个主要的缺点：首先，查看具有对控制器和模型两者的引用; 其次，它不会将UI逻辑的处理限制在单个类中，这个责任在Controller和View或Model之间共享。Model-View-Presenter模式解决了这两个问题，即断开View与Model的连接，并只创建**一个类来处理**与**View的呈现**相关**的**一切- Presenter：一个易于单元化的类测试。



另一位大神说明：

![](https://cdn-images-1.medium.com/max/800/1*1P4n9JkHChEUVr5umQx4Zw.png)

视图表示UI组件。因此，仅负责显示从演示者接收的数据。这也将模型转换为UI。

**演示者负责代表视图处理所有UI事件。**这通过View接收用户的输入，然后在Model的帮助下处理用户的数据，并将结果传回给View。与视图和控制器不同，视图和演示者完全脱离对方，并通过界面相互通信。

#### MVP模式的要点

- 用户与视图进行交互。
- View和Presenter之间**存在一对一的关系**，意味着一个View仅映射到一个Presenter。
- View具有对Presenter的引用，但View没有引用Model。
- 提供View和Presenter之间的**双向**通信。



### 如何实施

时刻记住一点： View 与 Model之间不能直接通信。



## MVVM



一个基于事件的架构

MVVM代表Model-View-ViewModel。此模式支持视图和视图模式之间的双向数据绑定。这样可以在View视图模式下自动传播更改。通常，视图模型使用观察者模式来通知视图模型中的变化来建模。

![](https://cdn-images-1.medium.com/max/800/1*fpTUAtCz8iiWU90WM7Pj4w.png)



ViewModel负责公开方法，命令和其他属性，有助于维护视图的状态，操作模型作为视图上的操作的结果，并触发视图本身中的事件。



MVVM模式的要点:

- 用户与视图进行交互。
- View与ViewModel之间存在**多对一**关系，意味着许多View可以映射到一个ViewModel。
- View具有对ViewModel的引用，但ViewModel没有关于View的信息。
- 支持View和ViewModel之间的双向数据绑定。









## MVP





1. [Android官方MVP架构示例项目解析](http://www.infoq.com/cn/articles/android-official-mvp-architecture-sample-project-analysis)，官方的github项目仓库中用多个分支进行了演示。   
2. [Android开发中的MVP架构](http://www.jianshu.com/p/7567ed0d1853)  
3. [【译】Android MVP 架构必要知识：第一部分](https://zhuanlan.zhihu.com/p/25272412 "推荐")  
4. [Model-View-Presenter Architecture in Android Applications](http://macoscope.com/blog/model-view-presenter-architecture-in-android-applications/)  
5. [MODEL VIEW PRESENTER (MVP) IN ANDROID, PART 2](http://www.tinmegali.com/en/model-view-presenter-mvp-in-android-part-2/)  
6. [MVP for Android: how to organize the presentation layer](https://antonioleiva.com/mvp-android/)  
7. [Model-View-Presenter: Android guidelines](https://medium.com/@cervonefrancesco/model-view-presenter-android-guidelines-94970b430ddf)
8. [一步一步实现Android的MVP框架](https://dev.qq.com/topic/5799d7844bef22a823b3ad44)   
9. [Android MVP模式 简单易懂的介绍方式](https://segmentfault.com/a/1190000003927200)  
10. [Android框架模式（1）-MVP入门 - 远古大钟 - CSDN博客](http://blog.csdn.net/duo2005duo/article/details/50594757 "Android框架模式（1）-MVP入门 - 远古大钟 - CSDN博客")








[Mindorks 的最佳文章都在这里](https://mindorks.com/blogs)



转载吧，转载文章。



以下内容来自，

- [【译】Android MVP 架构必要知识：第一部分](https://zhuanlan.zhihu.com/p/25272412 "推荐")   
- [【译】Android MVP 架构必要知识：第二部分](https://github.com/xitu/gold-miner/blob/master/TODO/essential-guide-for-designing-your-android-app-architecture-mvp-part-2.md)



原文：

- [Essential Guide For Designing Your Android App Architecture: MVP: Part 1](https://blog.mindorks.com/essential-guide-for-designing-your-android-app-architecture-mvp-part-1-74efaf1cda40)
- [Essential Guide For Designing Your Android App Architecture: MVP: Part 2](https://blog.mindorks.com/essential-guide-for-designing-your-android-app-architecture-mvp-part-2-b2ac6f3f9637)
- [Essential Guide For Designing Your Android App Architecture: MVP: Part 3 (Dialog, ViewPager…](https://blog.mindorks.com/essential-guide-for-designing-your-android-app-architecture-mvp-part-3-dialog-viewpager-and-7bdfab86aabb)
- [Android MVP Architecture Extension with Interactors and Repositories](https://blog.mindorks.com/android-mvp-architecture-extension-with-interactors-and-repositories-bd4b51972339) 这看起来又像一篇好文。

项目主页：[**android-mvp-architecture**: This repository contains a detailed sample app that implements MVP architecture using Dagger2, GreenDao, RxJava2, FastAndroidNetworking and PlaceholderView](https://github.com/MindorksOpenSource/android-mvp-architecture)



MVP的基础规程：

1. View 的唯一职责就是根据 Presenter 的指示绘制 UI。它在这个程序里应该是“哑”的。

2. View 将所有的用户交互委派给它的 Presenter。

3. View 永远不与 Model 直接交互。

4. Presenter 负责接受 View 对 Model 的请求，并且在特定的情况下控制 View。

5. Model 负责从服务器、数据库和文件系统获取数据。




MVP实现原则：

1. Activity，Fragment 和 自定义视图是应用的 View 部分。
2. 每一个 View 都有一个单独的 Presenter。
3. View 通过一个接口与 Presenter 通信，反之亦然。
4. Model 被分为几类：ApiHelper, PreferenceHelper, DatabaseHelper 和 FileHelper。这些都是用来帮助实现用来连接各种 model 的 DataManager 的。
5. Presenter 通过接口和 DataManager 交互。
6. DataManager 只在被调用的时候提供服务。
7. Presenter 不访问任何 Android API。

MVP 在单 Activity 的例子中看起来很简单。但是当我们尝试将一个应用的所有组件联系起来时就有些困难了。

简单的架构蓝图：

![](https://pic1.zhimg.com/v2-da300ec7d04e1398558f3d1451d019c8_r.png)



让我们理解这个架构草图的每一部分：

- **View**：绘制 UI 并接受用户的操作。Activity，Fragment和自定义视图属于这一部分。
- **MvpView**：一种接口，被 View 实现。它包括暴露给 Presenter 的方法。


- **Presenter**：它是决定 View 行为的纯 Java 类（不访问任何 Android API）。它接受从 View 传来的用户操作，并根据业务逻辑进行响应，最终指挥 View 进行特定的行为。它也从 DataManager 获取必要的数据。
- **MvpPresenter**：被 Presenter 实现的接口。它包括提供给 View 的方法。


- **AppDbHelper**：数据库管理类，负责所有和数据库有关的操作。
- **DbHelper**：被 AppDbHelper 实现的接口，包括提供给应用的方法。这一层对 DbHelper 的任何特定实现进行了解耦，这使得 AppDbHelper 成为了一个即插即用的单元。


- **AppPreferenceHelper**：类似于 AppDbHelper，只不过提供的是对于 SharedPreferences 的读写操作。
- **PreferenceHelper**：类似于 DbHelper 的接口，被 AppPreferenceHelper 实现。


- **AppApiHelper**：管理网络 API 请求及其数据处理。
- **ApiHelper**：类似于 DbHelper 的接口，被 AppApiHelper 实现。


- **DataManager**：被 AppDataManager 实现的接口。包括所有数据处理操作。理想情况下，它负责委派所有 Helper 的服务。所以 DataManager 继承 DbHelper，PreferenceHelper 和 ApiHelper。
- **AppDataManager**：它是应用中所有数据操作的结合点。DbHelper，PreferenceHelper 和 ApiHelper 只为 DataManager 提供服务。它负责委派任务给指定的 Helper。




**现在我们对于各种组件和它们的职责都熟悉了，我们马上将制定组件间的交互规则：**

- Application 类实例化 AppDbHelper（通过 DbHelper 引用），AppPreferenceHelper（通过 PreferenceHelper 引用），AppApiHelper（通过 ApiHelper 引用）以及最终的 AppDataManager（通过 DataManager 引用）。
- View 组件实例化它的 Presenter 并通过 MvpPresenter 引用。
- Presenter 通过参数接受 View 组件，并用 MvpView 引用，Presenter 也接受 DataManager。
- DataManager 是单例。

**这些是在应用中实现 MVP 的基础引导。**

就像一个外科医生在实际动手之前是没法完全掌握手术流程的。我们也不能完全理解这些想法和方案直到我们真正去实现它。

在下一部分，我们将探索一个真实的应用例子，希望能够很好地理解和掌握这些概念。








## MVVM


[MVC，MVP 和 MVVM 的图示](http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html)

## Clean





## Android 架构组件



[Android架构组件简介](https://code.tutsplus.com/tutorials/introduction-to-android-architecture--cms-28749?_ga=2.12071028.1998131091.1501205919-2091102857.1500428525)

Android体系结构指南，[Guide to App Architecture - Android Developers](https://developer.android.com/topic/libraries/architecture/guide.html "Guide to App Architecture - Android Developers")





Android团队在2017年 I/O大会：

- Kotlin
- Android 架构组件
- 。。。？



Android团队在2017年 I/O会议上推出的架构组件的四个组成部分：

- Room
- ViewModel
- LiveData
- Lifecycle



简化图：

![](https://cms-assets.tutsplus.com/uploads/users/1308/posts/28749/image/diagram%2001%20-%20Architecture%20Pattern.jpg)










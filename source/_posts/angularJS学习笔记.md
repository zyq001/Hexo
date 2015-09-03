title: angularJS学习笔记
date: 2015-07-10 10:52:37
tags: [Js, angular]  
categories: [Js, angular]   
thumbnail: /images/AngularJSCover.jpg  
banner: /images/AngularJS.jpg  
---
AngularJS 通过 **ng-directives** 扩展了 HTML。


- **ng-app** 指令定义一个 AngularJS 应用程序。  


- **ng-model** 指令把元素值（比如输入域的值）绑定到应用程序。  


- **ng-bind** 指令把应用程序数据绑定到 HTML 视图。  


什么是 AngularJS？

"AngularJS 是专门为**应用程序**设计的 HTML。"   
AngularJS 使得开发现代的**单一页面应用程序**（SPAs：Single Page Applications）变得更加容易。  
AngularJS 把应用程序**数据绑定到 HTML 元素**。  
AngularJS 可以**克隆和重复** HTML 元素。  
AngularJS 可以**隐藏和显示** HTML 元素。  
AngularJS 可以在 HTML 元素"背后"**添加代码**。  
AngularJS 支持**输入验证**。
<!-- more -->


### ng-app 指令
--- 
ng-app 指令定义了 AngularJS 应用程序的 **根元素**。  
ng-app 指令在网页加载完毕时会自动引导（自动初始化）应用程序。    

### ng-init 指令
---
ng-init 指令为 AngularJS 应用程序定义了 **初始值**。  
通常情况下，不使用 ng-init。您将使用一个控制器或模块来代替它。  
稍后您将学习更多有关控制器和模块的知识。  
### ng-model 指令
---
ng-model 指令 绑定 HTML 元素 到应用**程序数据**。
ng-model 指令也可以：


- 为应用程序数据提供类型**验证**（number、email、required）。

- 为应用程序数据提供状态（invalid、dirty、touched、error）。

- 为 HTML 元素提供 CSS 类。

- 绑定 HTML 元素到 HTML 表单。  

### ng-repeat 指令
---
ng-repeat 指令对于集合中（数组中）的每个项会 **克隆一次** HTML 元素。  

	

## AngularJS 控制器
---
AngularJS 应用程序被控制器控制。  
**ng-controller** 指令定义了应用程序控制器。  
控制器是 JavaScript 对象，由标准的 JavaScript 对象的构造函数 创建。  
控制器的 `$scope` 是控制器所指向的应用程序 HTML 元素。  

	

实例讲解：  
AngularJS 应用程序由 ng-app 定义。应用程序在 <div> 内运行。  
ng-controller 指令把控制器命名为 object。  
函数 personController 是一个标准的 JavaScript 对象的构造函数。  
控制器对象有一个属性：`$scope.person`。  
person 对象有两个属性：firstName 和 lastName。  
ng-model 指令绑定输入域到控制器的属性（firstName 和 lastName）。  


上面的实例演示了一个带有 lastName 和 firstName 这两个属性的控制器对象。
控制器也可以把函数作为对象属性：  


### 控制器方法

控制器也可以带有方法：  



### AngularJS 过滤器

过滤器可以使用一个管道字符（|）添加到表达式和指令中。  
AngularJS 过滤器  

AngularJS 过滤器可用于**转换数据**：  
过滤器  &#8195;	&#8195;描述  
currency	格式化数字为货币格式。  
filter	&#8195;从数组项中选择一个子集。  
lowercase	格式化字符串为小写。  
orderBy	&#8194;根据某个表达式排列数组。  
uppercase	格式化字符串为大写。  

- 向表达式添加过滤器

过滤器可以通过一个管道字符（|）和一个过滤器添加到表达式中。
（下面的两个实例，我们将使用前面章节中提到的 person 控制器）
uppercase 过滤器格式化字符串为大写：
	

**过滤输入**

输入过滤器可以通过一个管道字符（|）和一个过滤器添加到指令中，该过滤器后跟一个冒号和一个模型名称。  
filter 过滤器从数组中选择一个子集：  


### AngularJS XMLHttpRequest

$http 是 AngularJS 中的一个核心服务，用于读取远程服务器的数据。  
AngularJS $http  

AngularJS` $http` 是一个用于读取web服务器上数据的服务。  
`$http.get(url) `是用于读取服务器数据的函数。  
	

## AngularJS SQL
---
在前面章节中的代码也可以用于读取数据库中的数据
使用 PHP 从 MySQL 中获取数据

	

PHP 读取 MySQL 数据代码  


### AngularJS HTML DOM

AngularJS 有自己的 HTML 属性指令。  
**ng-disabled 指令**

ng-disabled 指令直接绑定应用程序数据到 HTML 的 disabled 属性。
	
**ng-show 指令**

ng-show 指令**隐藏或显示**一个 HTML 元素。
	
## AngularJS HTML 事件
---
AngularJS 有自己的 HTML 事件指令。
**ng-click** 指令

ng-click 指令定义了一个 AngularJS **单击**事件。
	

- 隐藏 HTML 元素

**ng-hide**指令用于设置应用的一部分 不可见 。
`ng-hide="true" `让 HTML 元素 不可见。
`ng-hide="false"` 让元素可见。


- 显示 HTML 元素

**ng-show** 指令可用于设置应用中的一部分可见 。  
`ng-show="false"` 可以设置 HTML 元素 不可见。  
`ng-show="true"` 可以以设置 HTML 元素可见。  
以下实例使用了 ng-show 指令:

## AngularJS 模块
---
模块定义了您的应用程序。  
所有的控制器都应该属于一个模块。  
模块保持全局命名空间中的整洁。  
AngularJS 模块实例  

在本实例中，"myApp.js" 包含了一个应用程序模块定义，"myCtrl.js" 包含了一个控制器：  

	

使用一个由 模块 替代的控制器：  

	

您的应用程序至少应该有一个模块文件，一个控制器文件。  
首先，创建模块文件 "myApp.js"：  

	
然后，创建控制器文件。本实例中是 "myCtrl.js"：  

	
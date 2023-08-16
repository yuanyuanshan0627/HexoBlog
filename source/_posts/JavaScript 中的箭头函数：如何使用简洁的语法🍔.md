---
abbrlink: 784f1a7a
categories:
  - - 原生 js
cover: >-
  https://hexo-admin.oss-cn-beijing.aliyuncs.com/image/2023/8/e45ade4938a2819e8ea372f6a3f70334.webp
date: '2023-08-15T17:48:19.725362+08:00'
description: "JavaScript\_中的箭头函数：如何使用简洁的语法\U0001F354"
excerpt: "theme:\_channing-cyan\_了解有关\_JavaScript\_箭头函数的所有信息。我们将向您展示如何使用\_ES6\_箭头语法，以及在代码中利用箭头函数时需要注意的一些常见错误。您将看到许多示例来说明它们的工作原理。\_JavaScript\_箭头函数随着\_ECMAScript\_2015（也称为\_ES6）的发布而出现。由于其简洁的语法和对*this*关键字的处理，箭头函数很快成为开发人员最喜欢..."
mathjax: true
swiper_index: 2
tags:
  - 箭头函数
title: "JavaScript 中的箭头函数：如何使用简洁的语法\U0001F354"
updated: '2023-8-15T17:52:26.577+8:0'
---
---
theme: channing-cyan
---
**了解有关 JavaScript 箭头函数的所有信息。我们将向您展示如何使用 ES6 箭头语法，以及在代码中利用箭头函数时需要注意的一些常见错误。您将看到许多示例来说明它们的工作原理。**

JavaScript 箭头函数随着 ECMAScript 2015（也称为 ES6）的发布而出现。由于其简洁的语法和对*[this](https://www.sitepoint.com/inner-workings-javascripts-this-keyword/)*关键字的处理，箭头函数很快成为开发人员最喜欢的功能。

## 箭头函数语法：重写常规函数

函数就像菜谱，您可以在其中存储有用的指令来完成程序中需要完成的操作，例如执行操作或返回值。通过调用您的函数，您可以执行配方中包含的步骤。每次调用该函数时都可以这样做，而无需一次又一次地重写配方。

以下是声明函数然后在 JavaScript 中调用它的标准方法：

```
// function declaration
function sayHiStranger() {
  return 'Hi, stranger!'
}

// call the function
sayHiStranger()
```

[您还可以编写与函数表达式](https://www.sitepoint.com/function-expressions-vs-declarations/)相同的函数，如下所示：

```
const sayHiStranger = function () {
  return 'Hi, stranger!'
}
```

JavaScript 箭头函数始终是表达式。以下是如何使用粗箭头符号重写上面的函数：

```
const sayHiStranger = () => 'Hi, stranger'
```

这样做的好处包括：

- 只需一行代码
- 没有`function`关键字
- 没有`return`关键字
- 并且没有大括号 {}

在 JavaScript 中，[函数是“一等公民”。](https://www.sitepoint.com/higher-order-functions-javascript/)您可以将函数存储在变量中，将它们作为参数传递给其他函数，并将它们作为值从其他函数返回。您可以使用 JavaScript 箭头函数来完成所有这些操作。

## 无括号语法

在上面的示例中，该函数没有参数。`()`在这种情况下，您必须在粗箭头 ( ) 符号之前添加一组空括号`=>`。[当您有多个参数](http://jsbin.com/doporef/edit?html,js,console,output)时，同样适用：

```
const getNetflixSeries = (seriesName, releaseDate) => `The ${seriesName} series was released in ${releaseDate}`
// call the function
console.log(getNetflixSeries('Bridgerton', '2020') )
// output: The Bridgerton series was released in 2020
```

然而，只要[有一个参数](http://jsbin.com/fitubus/edit?html,js,console,output)，您就可以继续省略括号（您不必这样做，但可以）：

```
const favoriteSeries = seriesName => seriesName === "Bridgerton" ? "Let's watch it" : "Let's go out"
// call the function
console.log(favoriteSeries("Bridgerton"))
// output: "Let's watch it"
```

不过要小心。例如，如果您决定使用[默认参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)，则必须[将其括在括号内](http://jsbin.com/cesehiv/edit?html,js,console,output)：

```
// with parentheses: correct
const bestNetflixSeries = (seriesName = "Bridgerton") => `${seriesName} is the best`
// outputs: "Bridgerton is the best"
console.log(bestNetflixSeries())

// no parentheses: error
const bestNetflixSeries = seriesName = "Bridgerton" => `${seriesName} is the best`
// Uncaught SyntaxError: invalid arrow-function arguments (parentheses around the arrow-function may help)
```

## 隐式回报

当函数体内只有一个表达式时，可以使 ES6 箭头语法更加简洁。您可以将所有内容保留在一行中，删除花括号，并取消关键字`return`。

您刚刚在上面的示例中看到了这些俏皮话的工作原理。这里还有[一个例子](http://jsbin.com/bamudij/edit?html,js,console,output)，只是为了更好地衡量。该`orderByLikes()`函数执行其表面上所说的操作：即，它返回按最高点赞数排序的 Netflix 系列对象数组：

```
// using the JS sort() function to sort the titles in descending order 
// according to the number of likes (more likes at the top, fewer at the bottom
const orderByLikes = netflixSeries.sort( (a, b) => b.likes - a.likes )

// call the function 
// output:the titles and the n. of likes in descending order
console.log(orderByLikes)
```

这很酷，但请注意代码的可读性 - 特别是在使用单行代码和无括号的 ES6 箭头语法对一堆箭头函数进行排序时，如下例[所示](http://jsbin.com/bicapuf/edit?html,js,console,output)：

```
const greeter = greeting => name => `${greeting}, ${name}!`
```

那里发生了什么事？尝试使用常规函数语法：

```
function greeter(greeting) {
  return function(name) {
    return `${greeting}, ${name}!` 
  }
} 
```

现在，您可以快速了解外部函数如何`greeter`具有参数 ，`greeting`并返回匿名函数。该内部函数又具有一个名为 的参数，并使用和`name`的值返回一个字符串。以下是调用该函数的方法：`greeting``name`

```
const myGreet = greeter('Good morning')
console.log( myGreet('Mary') )   

// output: 
"Good morning, Mary!" 
```

### 注意这些隐式返回错误

当您的 JavaScript 箭头函数包含多个语句时，您需要将它们全部括在花括号中并使用关键字`return`。

在[下面的代码](http://jsbin.com/nulexar/edit?html,js,console,output)中，该函数构建了一个对象，其中包含一些 Netflix 系列的标题和摘要（Netflix 评论来自[烂番茄](https://editorial.rottentomatoes.com/guide/best-netflix-shows-and-movies-to-binge-watch-now/)网站）：

```
const seriesList = netflixSeries.map( series => {
  const container = {}
  container.title = series.name 
  container.summary = series.summary

  // explicit return
  return container
} )
```

函数内部的箭头函数`.map()`由一系列语句组成，在语句末尾返回一个对象。这使得在函数体周围使用花括号是不可避免的。

另外，当您使用花括号时，隐式返回不是一个选项。您必须使用`return`关键字。

如果您的函数使用隐式*返回返回对象文字*，则需要将该对象括在圆括号内。不这样做会导致错误，因为 JavaScript 引擎错误地将对象文本的大括号解析为函数的大括号。正如您在上面刚刚注意到的，当您在箭头函数中使用花括号时，不能省略 return 关键字。

先前代码的较短版本演示了此语法：

```
// Uncaught SyntaxError: unexpected token: ':'
const seriesList = netflixSeries.map(series => { title: series.name });

// Works fine
const seriesList = netflixSeries.map(series => ({ title: series.name }));
```

## 你不能命名箭头函数

关键字和参数列表之间没有名称标识符的函数`function`称为*匿名函数*。常规匿名函数表达式如下所示：

```
const anonymous = function() {
  return 'You can't identify me!' 
}
```

**箭头函数都是匿名函数**：

```
const anonymousArrowFunc = () => 'You can't identify me!' 
```

从 ES6 开始，变量和方法可以使用匿名函数的属性从其语法位置推断其名称`name`。这使得在检查其值或报告错误时识别该函数成为可能。

[](http://jsbin.com/menowoy/edit?html,js,console,output)使用[以下命令检查一下](http://jsbin.com/menowoy/edit?html,js,console,output)`anonymousArrowFunc`：

```
console.log(anonymousArrowFunc.name)
// output: "anonymousArrowFunc"
```

请注意，仅当将匿名函数分配给变量时，此推断`name`属性才存在，如上面的示例所示。如果您使用匿名函数作为[回调](https://www.sitepoint.com/demystifying-javascript-closures-callbacks-iifes/)，您将失去这个有用的功能。[下面的演示对此](http://jsbin.com/yofizis/edit?html,js,console,output)进行了举例说明，其中方法内的匿名函数`.setInterval()`无法利用该`name`属性：

```
let counter = 5
let countDown = setInterval(() => {
  console.log(counter)
  counter--
  if (counter === 0) {
    console.log("I have no name!!")
    clearInterval(countDown)
  }
}, 1000)
```

这还不是全部。这个推断的`name`属性仍然不能作为一个正确的标识符，您可以使用它来从内部引用该函数——例如递归、解除绑定事件等。

## 箭头函数如何处理`this`关键字

关于箭头函数，要记住的最重要的事情是它们处理关键字的方式`this`。特别是，`this`箭头函数内的关键字不会反弹。

为了说明这意味着什么，请查看下面的演示：

[codepen_embed height=”300″ default_tab=”html,result” slug_hash=”qBqgBmR” user=”SitePoint”]在[CodePen](https://codepen.io/)上通过 SitePoint ( [@SitePoint](https://codepen.io/SitePoint) )查看[
箭头函数中的](https://codepen.io/SitePoint/pen/qBqgBmR)Pen JS this 。[/codepen_embed][](https://codepen.io/SitePoint)
[](https://codepen.io/)

这是一个按钮。单击该按钮会触发从 5 到 1 的反向计数器，该计数器显示在按钮本身上。

```
<button class="start-btn">Start Counter</button>

...

const startBtn = document.querySelector(".start-btn");

startBtn.addEventListener('click', function() {
  this.classList.add('counting')
  let counter = 5;
  const timer = setInterval(() => {
    this.textContent = counter 
    counter -- 
    if(counter < 0) {
      this.textContent = 'THE END!'
      this.classList.remove('counting')
      clearInterval(timer)
    }
  }, 1000) 
})
```

请注意，方法内的事件处理程序`.addEventListener()`是常规匿名函数表达式，而不是箭头函数。为什么？如果您登录`this`该函数，您将看到它引用了侦听器所附加的按钮元素，这正是预期的内容，也是程序按计划工作所需的内容：

```
startBtn.addEventListener('click', function() {
  console.log(this)
  ...
})
```

Firefox 开发者工具控制台中的内容如下：

![处理按钮单击事件的常规匿名函数表达式内的 this 关键字的日志](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f3f3aa822bf54867b424c12435c8c0f9~tplv-k3u1fbpfcp-zoom-1.image)

但是，尝试用箭头函数替换常规函数，如下所示：

```
startBtn.addEventListener('click', () => {
  console.log(this)
  ...
})
```

现在，`this`不再引用该按钮。相反，它引用该`Window`对象：

![JavaScript 箭头函数内的 this 关键字引用的 window 对象传递给事件侦听器](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ec2bc81d61d640a8aabe1680b25e01c9~tplv-k3u1fbpfcp-zoom-1.image)

这意味着，例如，如果您想`this`在单击按钮后向按钮添加类，您的代码将不起作用：

```
// change button's border's appearance
this.classList.add('counting')
```

当您在 JavaScript 中使用箭头函数时，关键字的值`this`不会反弹。它是从父作用域继承的（这称为**[词法作用域](https://www.sitepoint.com/5-ways-declare-functions-jquery/)**）。在这种特殊情况下，所讨论的箭头函数作为参数传递给该`startBtn.addEventListener()`方法，该方法位于全局范围内。因此，`this`函数处理程序内部也绑定到全局范围，即绑定到`Window`对象。

所以，如果要`this`在程序中引用开始按钮，正确的做法是使用常规函数，而不是箭头函数。

### 匿名箭头函数

在上面的演示中接下来要注意的是方法内的代码`.setInterval()`。在这里，您也会发现一个匿名函数，但这次它是一个箭头函数。为什么？

`this`请注意，如果您使用常规函数，则的值会是什么：

```
const timer = setInterval(function() {
  console.log(this)
  ...
}, 1000)
```

会是`button`元素吗？一点也不。这将是一个`Window`对象！

![在 setInterval() 中使用常规函数将 this 关键字的引用从按钮更改为 Window 对象](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/41316f6a14ce46ff94c4fab097f6f0e0~tplv-k3u1fbpfcp-zoom-1.image)

事实上，上下文已经改变，因为`this`现在位于一个未绑定或全局函数内，该函数作为参数传递给`.setInterval()`. 因此，关键字的值`this`也发生了变化，因为它现在绑定到全局范围。

在这种情况下，一个常见的技巧是包含另一个变量来存储关键字的值，`this`以便它不断引用预期的元素 - 在本例中为元素`button`：

```
const that = this
const timer = setInterval(function() {
  console.log(that)
  ...
}, 1000)
```

您还可以使用以下方法`.bind()`来解决问题：

```
const timer = setInterval(function() {
  console.log(this)
  ...
}.bind(this), 1000)
```

使用箭头函数，问题就完全消失了。`this`以下是使用箭头函数时的值：

```
const timer = setInterval( () => { 
  console.log(this)
  ...
}, 1000)
```

![传递给 setInterval() 的箭头函数内的 this 值](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d18de01ac1104c088b096b39c4675b55~tplv-k3u1fbpfcp-zoom-1.image)

这次，控制台记录了按钮，这就是我们想要的。事实上，程序要更改按钮文本，因此需要`this`引用该`button`元素：

```
const timer = setInterval( () => { 
  console.log(this)
 // the button's text displays the timer value
  this.textContent = counter
}, 1000)
```

箭头函数*没有自己的`this`上下文*。他们继承了父母的价值`this`，正是因为这一特点，他们在上述情况下做出了很好的选择。

## JavaScript 箭头函数并不总是适合该工作的工具

箭头函数不仅仅是在 JavaScript 中编写函数的一种奇特的新方式。它们有其自身的局限性，这意味着在某些情况下您不想使用它们。上一个演示中的点击处理程序就是一个很好的例子，但它不是唯一的例子。让我们再检查一些。

### 箭头函数作为对象方法

箭头函数不能很好地用作对象上的方法。这是一个[例子](http://jsbin.com/bomeqiq/edit?html,js,console,output)。

考虑这个`netflixSeries`对象，它有一些属性和几个方法。调用`console.log(netflixSeries.getLikes())`应该打印一条包含当前点赞数的消息，并且调用`console.log(netflixSeries.addLike())`应该将点赞数增加一，然后在控制台上打印新值以及感谢消息：

```
const netflixSeries = {
  title: 'After Life', 
  firstRealease: 2019,
  likes: 5,
  getLikes: () => `${this.title} has ${this.likes} likes`,
  addLike: () => {  
    this.likes++
    return `Thank you for liking ${this.title}, which now has ${this.likes} likes`
  } 
}
```

相反，调用该`.getLikes()`方法会返回“undefined has NaN likes”，调用该`.addLike()`方法会返回“Thank you for Like undefine, it now has NaN likes”。因此，`this.title`和分别`this.likes`无法引用对象的属性`title`和`likes`。

问题再次出在箭头函数的[词法范围](https://www.sitepoint.com/joys-block-scoping-es6/)上。对象的内部`this`方法引用父级的作用域，在本例中是对象`Window`，而不是父级本身 - 也就是说，不是对象`netflixSeries`。

当然，解决方案是使用常规函数：

```
const netflixSeries = {
  title: 'After Life', 
  firstRealease: 2019,
  likes: 5,
  getLikes() {
    return `${this.title} has ${this.likes} likes`
  },
  addLike() { 
    this.likes++
    return `Thank you for liking ${this.title}, which now has ${this.likes} likes`
  } 
}

// call the methods 
console.log(netflixSeries.getLikes())
console.log(netflixSeries.addLike())

// output: 
After Life has 5 likes
Thank you for liking After Life, which now has 6 likes
```

### 带有第三方库的箭头函数

另一个需要注意的问题是第三方库通常会绑定方法调用，以便该`this`值指向有用的东西。

例如，在 jQuery 事件处理程序中，`this`您可以访问处理程序绑定到的 DOM 元素：

```
$('body').on('click', function() {
  console.log(this)
})
// <body>
```

但是如果我们使用箭头函数——正如我们所见，它没有自己的`this`上下文——我们会得到意想不到的结果：

```
$('body').on('click', () =>{
  console.log(this)
})
// Window
```

[这是使用Vue 的](https://www.sitepoint.com/vue-3-beginner-guide/)另一个示例：

```
new Vue({
  el: app,
  data: {
    message: 'Hello, World!'
  },
  created: function() {
    console.log(this.message);
  }
})
// Hello, World!
```

在钩子内部`created`，`this`绑定到 Vue 实例，因此“Hello, World!” 显示消息。

然而，如果我们使用箭头函数，`this`它将指向没有属性的父作用域`message`：

```
new Vue({
  el: app,
  data: {
    message: 'Hello, World!'
  },
  created: function() {
    console.log(this.message);
  }
})
// undefined
```

### 箭头函数没有`arguments`对象

有时，您可能需要创建一个具有无限数量参数的函数。例如，假设您想要创建一个函数，按照偏好顺序列出您最喜欢的 Netflix 系列。但是，您还不知道要包含多少个系列。JavaScript 使*[参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)*对象可用。这是一个类似数组的对象（不是完整的数组），它存储调用时传递给函数的值。

尝试使用箭头函数来[实现此功能：](https://jsbin.com/fitikoh/2/edit?html,js,console,output)

```
const listYourFavNetflixSeries = () => {
  // we need to turn the arguments into a real array 
  // so we can use .map()
  const favSeries = Array.from(arguments) 
  return favSeries.map( (series, i) => {
    return `${series} is my #${i +1} favorite Netflix series`  
  } )
  console.log(arguments)
}

console.log(listYourFavNetflixSeries('Bridgerton', 'Ozark', 'After Life')) 
```

当您调用该函数时，您将收到以下错误消息：`Uncaught ReferenceError: arguments is not defined`。这意味着该`arguments`对象在箭头函数内不可用。事实上，用常规函数替换箭头函数就可以达到目的：

```
const listYourFavNetflixSeries = function() {
   const favSeries = Array.from(arguments) 
   return favSeries.map( (series, i) => {
     return `${series} is my #${i +1} favorite Netflix series`  
   } )
   console.log(arguments)
 }
console.log(listYourFavNetflixSeries('Bridgerton', 'Ozark', 'After Life'))

// output: 
["Bridgerton is my #1 favorite Netflix series",  "Ozark is my #2 favorite Netflix series",  "After Life is my #3 favorite Netflix series"]
```

因此，如果您需要该`arguments`对象，则不能使用箭头函数。

但是，如果您*确实*想使用箭头函数来复制相同的功能怎么办？你可以做的一件事是使用[ES6 剩余参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)( `...`)。以下是重写函数的方法：

```
const listYourFavNetflixSeries = (...seriesList) => {
   return seriesList.map( (series, i) => {
     return `${series} is my #${i +1} favorite Netflix series`
   } )
 }
```

## 结论

通过使用箭头函数，您可以编写带有隐式返回的简洁单行代码，并最终忘记旧式技巧来解决`this`JavaScript 中关键字的绑定。箭头函数也可以很好地与`.map()`、`.sort()`、`.forEach()`、`.filter()`和 等数组方法配合使用`.reduce()`。但请记住：箭头函数不会取代常规 JavaScript 函数。请记住，仅当 JavaScript 箭头函数是适合该工作的工具时才使用它们。

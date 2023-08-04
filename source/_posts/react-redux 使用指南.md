---
abbrlink: react-redux
categories:
- - React
date: '2023-08-04T10:43:46.977768+08:00'
description: react-redux
mathjax: true
swiper_index: 1
tags:
- react-redux
title: 🍩react-redux 使用指南
updated: 2023-8-4T11:5:42.238+8:0
---
`React`是一款非常优秀的前端框架，但是我们不能说它是尽善尽美的。比如说`React`在做大型项目时，在处理状态管理的问题时就显得捉襟见肘。因此针对于状态管理的问题就衍生出了很多的技术，比如`flux`，`redux`等等。在这篇文章中我们只探讨`redux`，如果小伙伴们学会了`redux`，就不用再去学习`redux`，因为`redux`是`flux`的一个升级。当然有的小伙伴会问如果他用的是vue或者是`angular`可不可以用`redux`呢，这里明确的说明一下都是可以的，哪怕是原生的`js`也是可以的。

在这篇文章中我将会分为七个步骤来为小伙伴们介绍`React Redux`，相信看完这篇文章的你就可以很好的应用`React Redux`了。

> 准备工作
> 1.什么是state？
> 2.什么是redux为什么选择redux？
> 3.什么是reducer？
> 4.什么是store？
> 5.怎么关联store？
> 6.什么是action？
> 7.怎么处理异步代码？
> 总结
> 另附

---

**准备工作**

在准备工作进行之前默认你了解了`React`和`ES6`的相关知识。

首先我们在创建项目时用下面的命令行：

```js
npx create-react-app react-redux-example
```

如果是在创建好的项目中想要使用，应该在执行下面的命令：

```js
npm install redux react-redux
```

然后我们需要创建一些文件。

* 1、在`src`目录下创建一个`container`文件夹，在`container`下面创建一个Articles.js文件。

```js
import React, { useState } from "react"
import Article from "../components/Article/Article"
import AddArticle from "../components/AddArticle/AddArticle"

const Articles = () => {
  const [articles, setArticles] = useState([
    { id: 1, title: "post 1", body: "Quisque cursus, metus vitae pharetra" },
    { id: 2, title: "post 2", body: "Quisque cursus, metus vitae pharetra" },
  ])
  const saveArticle = e => {
    e.preventDefault()
    // 逻辑代码稍后更新
  }

  return (
    <div>
      <AddArticle saveArticle={saveArticle} />
      {articles.map(article => (
        <Article key={article.id} article={article} />
      ))}
    </div>
  )
}

export default Articles
```

* 2、在`src`目录下面创建一个`components`文件夹，然后创建AddArticle/AddArticle.js和Article/Article.js

`Article.js`

```js
import React from "react"
import "./Article.css"

const article = ({ article }) => (
  <div className="article">
    <h1>{article.title}</h1>
    <p>{article.body}</p>
  </div>
)

export default article
```

`AddArticle.js`

```js
import React, { useState } from "react"
import "./AddArticle.css"

const AddArticle = ({ saveArticle }) => {
  const [article, setArticle] = useState()

  const handleArticleData = e => {
    setArticle({
      ...article,
      [e.target.id]: e.target.value,
    })
  }
  const addNewArticle = e => {
    e.preventDefault()
    saveArticle(article)
  }

  return (
    <form onSubmit={addNewArticle} className="add-article">
      <input
        type="text"
        id="title"
        placeholder="Title"
        onChange={handleArticleData}
      />
      <input
        type="text"
        id="body"
        placeholder="Body"
        onChange={handleArticleData}
      />
      <button>Add article</button>
    </form>
  )
}
export default AddArticle
```

`App.js`

```js
import React from "react"
import Articles from "./containers/Articles"

function App() {
  return <Articles />
}
export default App
```

如果小伙伴们完成了上面的步骤，就可以接着往下进行啦！

---

**1.什么是`State`？**

每一个`react`组件（无状态组件除外）的核心都是`state`。它决定了组建的渲染方式和表现的形式。想要真正的理解`state`，必须通过实际的例子。比如说弹窗是否打开，组件是否渲染等等。

```js
// Class based component
state = {
  articles: [
    { id: 1, title: "post 1", body: "Quisque cursus, metus vitae pharetra" },
    { id: 2, title: "post 2", body: "Quisque cursus, metus vitae pharetra" },
  ],
}
// React hooks
const [articles, setArticles] = useState([
  { id: 1, title: "post 1", body: "Quisque cursus, metus vitae pharetra" },
  { id: 2, title: "post 2", body: "Quisque cursus, metus vitae pharetra" },
])
```

相信小伙伴们现在知道什么是`state`了，现在就为你们介绍`redux`。

---

**2.什么是`redux`为什么使用`redux`？**

如果没有`redux`或者是其他的工具管理`state`将变的无比艰难。想象一下我们必须检查每一个组件来看看弹窗是否开启了。为了解决这个问题，我们必须在组件间传递`props`，这会使组件的数据变得非常的混乱，开发成本也变得很高。但是有了`redux`一切就变得很简单了。

![](https://pic4.zhimg.com/80/v2-8cae5ee7e0d43cf94cf19b797f2eb2c7_1440w.webp)

---

**3.什么是`reducer`？**

`reducer`是一个纯函数，它接收之前的`state`和`action`作为参数，返回一个更新了的`state`。`reducer`只能处理同步的代码，意味着没有像`HTTP`请求那样的副作用。当然我们也可以用`redux`来处理异步代码，我们在后续会学习怎样处理。当然如果你对`action`还不了解那么没有关系，后面会为大家介绍的。下面让我们来创建我们的第一个`reducer`吧。

按照惯例，我们要创建一个`store`文件夹，然后创建一个`reducer.js`文件。

`reducer.js`文件

```js
const initialState = {
  articles: [
    { id: 1, title: "post 1", body: "Quisque cursus, metus vitae pharetra" },
    { id: 2, title: "post 2", body: "Quisque cursus, metus vitae pharetra" },
  ],
}

const reducer = (state = initialState, action) => {
  return state
}
export default reducer
```

reducer就是一个接收了以前的state和action作为参数的纯函数，返回了一个更新后的state。现在我们已经创建好了reducer了，接下来让我们来创建store吧。

---

**4.什么是`store`?**

`store`是`react`项目中存储`state`的地方，你可以把它看成是一个大的`JavaScript`对象。创建`store`时我们需要一个`reducer`来作为参数，我们已经创建好`reducer`了，让我们把它关联到`store`上面吧。

```js
import React from "react"
import ReactDOM from "react-dom"
import { createStore } from "redux"

import "./index.css"
import App from "./App"
import reducer from "./store/reducer"

const store = createStore(reducer)

ReactDOM.render(<App />, document.getElementById("root"))
```

---

**5.怎么把`store`关联到`React`？**

想把`store`关联到`React`，我们需要引入一个辅助函数叫做`Provider`。然后用`Provider`组件包裹着`App`组件，再把`store`作为`props`值传入`Provider`。

`index.js`文件

```js
import React from "react"
import ReactDOM from "react-dom"
import { createStore } from "redux"
import { Provider } from "react-redux"

import "./index.css"
import App from "./App"
import reducer from "./store/reducer"

const store = createStore(reducer)

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
)
```

`Articles.js`文件

```js
import React from "react"
import { connect } from "react-redux"

import Article from "../components/Article/Article"
import AddArticle from "../components/AddArticle/AddArticle"

const Articles = ({ articles }) => {
  const saveArticle = e => {
    e.preventDefault()
    // ...
  }
  return (
    <div>
      <AddArticle saveArticle={saveArticle} />
      {articles.map(article => (
        <Article key={article.id} article={article} />
      ))}
    </div>
  )
}

const mapStateToProps = state => {
  return {
    articles: state.articles,
  }
}

export default connect(mapStateToProps)(Articles)
```

在这里我们引入了`connect()`，它能帮助我们把组件和`store`连接起来，并且可以获取`state`。

我们声明了一个新的函数叫 `mapStateToProps()`，当然函数名也可以是别的，它从`store`中获取`state`值作为它的参数，返回了一个对象。

为了获取到`store`中的`state`，我们需要把 `mapStateToProps()`作为`connect`函数的参数。

---

**6.什么是`action`？**

`action`包含着各种类型，比如`REMOVE\_ARTICLE`*或者* `ADD*\_*ARTICLE`等。它从`react`组件中被分发（传递数据）到`redux`的`store` 中。当让`action`只是一个传递信息的，他不能改变`store`。`store`只能被`reducer`改变。

在项目中创建`action`，我们在`store`文件夹中先创建一个`actionTypes.js`

```js
export const ADD_ARTICLE = "ADD_ARTICLE"
```

然后我们去`Articles.js`文件

```js
import React from "react"
import { connect } from "react-redux"

import Article from "../components/Article/Article"
import AddArticle from "../components/AddArticle/AddArticle"
import * as actionTypes from "../store/actionTypes"

const Articles = ({ articles, saveArticle }) => (
  <div>
    <AddArticle saveArticle={saveArticle} />
    {articles.map(article => (
      <Article key={article.id} article={article} />
    ))}
  </div>
)

const mapStateToProps = state => {
  return {
    articles: state.articles,
  }
}

const mapDispatchToProps = dispatch => {
  return {
    saveArticle: article =>
      dispatch({ type: actionTypes.ADD_ARTICLE, articleData: { article } }),
  }
}

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(Articles)
```

在这里我们从`actionTypes.js`中引入了`everything` 。然后创建了一个新的函数`mapDispatchToProps` ，它接收`dispatch`作为参数。

`store/reducer.js`文件

```js
import * as actionTypes from "./actionTypes"

const initialState = {
  articles: [
    { id: 1, title: "post 1", body: "Quisque cursus, metus vitae pharetra" },
    { id: 2, title: "post 2", body: "Quisque cursus, metus vitae pharetra" },
  ],
}

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionTypes.ADD_ARTICLE:
      const newArticle = {
        id: Math.random(), // not really unique but it's just an example
        title: action.article.title,
        body: action.article.body,
      }
      return {
        ...state,
        articles: state.articles.concat(newArticle),
      }
  }
  return state
}
export default reducer
```

我们引入了`actionTypes`。然后我们检查`reducer`函数看看`action`的类型是否是 `ADD\_ARTICLE`。如果是的话我们创建了一个对象，返回了一个新的`state`。

---

**7.`redux`怎么处理异步代码？**

我们需要创建一个新的文件 `actionCreators.js`

`store/actionCreators.js`

```js
import * as actionTypes from "./actionTypes"

export const addArticle = article => {
  return {
    type: actionTypes.ADD_ARTICLE,
    article,
  }
}
```

`Articles.js`

```js
import React from "react"
import { connect } from "react-redux"

import Article from "../components/Article/Article"
import AddArticle from "../components/AddArticle/AddArticle"
import { addArticle } from "../store/actionCreators"

const Articles = ({ articles, saveArticle }) => (
  <div>
    <AddArticle saveArticle={saveArticle} />
    {articles.map(article => (
      <Article key={article.id} article={article} />
    ))}
  </div>
)

const mapStateToProps = state => {
  return {
    articles: state.articles,
  }
}

const mapDispatchToProps = dispatch => {
  return {
    saveArticle: article => dispatch(addArticle(article)),
  }
}

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(Articles)
```

现在还没有完成袄，我们还需引入一个新的依赖包`redux-thunk`，`redux-thunk`是一个中间件它可以使我们处理异步代码。

```js
npm install redux-thunk
```

`index.js`文件

```js
import React from "react"
import ReactDOM from "react-dom"
import { createStore, applyMiddleware } from "redux"
import { Provider } from "react-redux"
import thunk from "redux-thunk"

import "./index.css"
import App from "./App"
import reducer from "./store/reducer"

const store = createStore(reducer, applyMiddleware(thunk))

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
)
```

`store/actionCreators.js`

```js
import * as actionTypes from "./actionTypes"

export const addArticle = article => {
  return {
    type: actionTypes.ADD_ARTICLE,
    article,
  }
}

export const simulateHttpRequest = article => {
  return dispatch => {
    setTimeout(() => {
      dispatch(addArticle(article))
    }, 3000)
  }
}
```

`Articles.js`

```js
import React from "react"
import { connect } from "react-redux"

import Article from "../components/Article/Article"
import AddArticle from "../components/AddArticle/AddArticle"
import { simulateHttpRequest } from "../store/actionCreators"

const Articles = ({ articles, saveArticle }) => (
  <div>
    <AddArticle saveArticle={saveArticle} />
    {articles.map(article => (
      <Article key={article.id} article={article} />
    ))}
  </div>
)

const mapStateToProps = state => {
  return {
    articles: state.articles,
  }
}

const mapDispatchToProps = dispatch => {
  return {
    saveArticle: article => dispatch(simulateHttpRequest(article)),
  }
}

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(Articles)
```

在这里我们做的唯一的改变就是把`addArticle`变成了 `simulateHttpRequest`，现在我们就可以通过`redux`来执行异步代码了。

---

**总结**

当我们在处理中大型的`react`项目是，管理我们的`state`就变得非常的困难。有了`redux`就变得非常简单了，当然了还有很多其他的解决办法像 `context API（hook`）在处理`state`管理的问题时也是非常好用的。

最后，大家可以关注我的文章，定期为小伙伴们分享前端的知识，希望能够帮助到小伙伴们。

---

**另附**

本文参考了`Redux`官网，还有网上一些好文章，如有侵权，请联系我，谢谢。

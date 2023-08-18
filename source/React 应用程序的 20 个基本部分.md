---
date: '2023-08-18T11:51:09.378234+08:00'
title: title
updated: 2023-8-18T11:51:9.580+8:0
---
# 任何大型 React 应用程序的 20 个基本部分

多年来我有幸参与过一些大型 React 项目。今天，我收集了在构建新项目或增强任何大型应用程序的功能时需要记住的一些基本事项。

我们将从绝对基础开始，然后深入探讨。所以系好安全带！

## 一、项目结构

当我开始使用 React 时，我很直观地按文件类型保存文件。Bus 因为我有幸参与一些较大的项目，所以我了解随着任何项目变得越来越大，浏览文件会变得多么困难 > 花一些时间进行研究以找出最佳的文件夹结构。

对于大多数情况，我发现遵循域驱动的文件夹模式具有很强的可扩展性。例如，您应该将所有`user-related`文件保存在一个文件夹中，并将`authentication-related`文件保存在另一文件夹中。

这样您以后就可以很容易地找到特定的文件。

![我的文件夹结构](https://cdn-images-1.medium.com/max/2000/1*DCent5OwUirMGB-eZdC27Q.png)

这是我的。但您可以自行选择和定制。

## 2. 全球商店

拥有全球商店对于任何大型 ReactJS 应用程序都非常重要。

虽然有很多选择，但对于大型项目来说，Redux 仍然是一个非常好的、安全的选择。

* [还原](https://redux.js.org/)

Redux 生态系统也足够丰富，足以涵盖您的大多数用例。一些辅助库是......

[redux-persist](https://github.com/rt2zz/redux-persist)：用于在本地保存数据

[redux-thunk](https://github.com/reduxjs/redux-thunk)：用于异步操作

[reselect](https://github.com/reduxjs/reselect)：选择器库以优化您的商店访问

[react-redux](https://github.com/reduxjs/react-redux)：与 React 集成

此外，您应该使用[redux-devtools](https://github.com/reduxjs/redux-devtools)扩展来充分利用任何基于 react-redux 的项目。

[随着redux-toolkit](https://redux-toolkit.js.org/introduction/quick-start)的引入，它现在变得不再那么冗长和干净。

## 3. 路由

React 没有提供用于客户端路由的官方库。但`react-router-dom`迄今为止是大多数项目的首选。

* [反应路由器 DOM](https://reactrouter.com/web/guides/quick-start)

此外，还有一些与您的反应路由器生态系统非常匹配的帮助程序库。

[历史记录](https://www.npmjs.com/package/history)：跟踪导航页面的历史记录

[connected-react-router](https://github.com/supasate/connected-react-router)：帮助将你的路由与 redux 状态连接起来。

## 4. 多重环境

任何大型项目都会有多个环境，作为开发人员，您应该知道如何处理它。可以有多个环境，例如......

* 发展
* 分期
* 生产

您应该为此维护单独的环境文件。您可以为此目的添加`.env` `end.development`,等文件。`.env.staging`

您可以从此处了解有关 React 环境的更多信息

[https://javascript.plainenglish.io/handle-multiple-environments-in-react-d3d05b2c4248](https://javascript.plainenglish.io/handle-multiple-environments-in-react-d3d05b2c4248)

## 5. 表单处理

表单是几乎所有类型的 Web 应用程序的重要组成部分，以干净的方式手动处理它们可能会很棘手。

对于企业级应用程序，您可以使用一些非常流行的库，例如

* [福米克](https://formik.org/)
* [反应钩子形式](https://react-hook-form.com/)

他们将处理组件中的大部分样板逻辑，并提供验证和其他很酷的功能。但我`react-hook-form`更喜欢它，因为它的性能更高。

这是您的入门指南。

[https://javascript.plainenglish.io/how-to-use-react-hook-form-with-typescript-2cf597c0c45f](https://javascript.plainenglish.io/how-to-use-react-hook-form-with-typescript-2cf597c0c45f)

## 6. 造型

您可以使用普通的旧`css`组件，但在当今时代，您应该使用`sass`更好的样式设置。

* [节点 sass](https://www.npmjs.com/package/node-sass)

如果您想要更现代的东西，您应该使用`styled-components`. 事实上，它现在是我的首选图书馆。它帮助我将样式用作独立组件，并帮助我摆脱到处使用`className`属性的情况。

* [样式组件](https://styled-components.com/)

## 7.用户界面库

如果您手动设计所有组件，则不需要。但大多数时候情况并非如此。所以你应该明智地选择你的组件库。

* [材质用户界面](https://material-ui.com/)
* [语义用户界面](https://react.semantic-ui.com/)
* [蚂蚁设计](https://ant.design/)

这些是您应该注意的一些选项。

此外，对于某些特定的用例，您可以选择其他库，例如[react-loader-spinner](https://www.npmjs.com/package/react-loader-spinner?activeTab=readme)或[react-spinner](https://www.npmjs.com/package/react-spinners)来加载动画。

或者对于表来说，[react-table](https://www.npmjs.com/package/react-table)可能是一个值得考虑的强大选项。

## 8.HTTP查询

从远程服务器获取数据是动态反应应用程序最常见的任务之一。对于标准的CRUD操作，**Axios**是一个不错的选择

* [轴](https://github.com/axios/axios)

如果您想要更强大的功能，您可以使用开箱即用的`react-query`功能。`caching`

* [反应查询](https://github.com/tannerlinsley/react-query)

## 9. 文档

对于大型项目，文档非常重要。有很多库，但根据我的观点，最好和最简单的选择是使用`react-styleguidist`

* [反应风格指南](https://react-styleguidist.js.org/docs/documenting/)

您可以了解更多相关信息

[https://javascript.plainenglish.io/document-your-react-applications-the-right-way-f648053c3a70](https://javascript.plainenglish.io/document-your-react-applications-the-right-way-f648053c3a70)

## 10. 多语言支持

对于大型国际项目，您通常需要添加多语言支持。最好将其添加到项目的开头。

最好的选择是使用`react-i18next`和`i18next`库。

您可以在这里了解更多信息

[https://javascript.plainenglish.io/implement-multi-language-support-in-react-9854c52ddb55](https://javascript.plainenglish.io/implement-multi-language-support-in-react-9854c52ddb55)

## 11.动画库

动画有助于让您的应用程序看起来响应更快并且使用起来更有趣。适当数量的动画可以产生很大的不同。

但不要做得太过分！您可以创建自己的动画或使用强大的库，例如`react-awesome-reveal , react-spring or react-transition-group`.

感谢[Alex Chan](https://www.mohammadfaisal.dev/blog/undefined)，我从他的评论中发现了另一个很棒的库，名为[Framer Motion](https://www.framer.com/motion/)。这很棒！

## 12.EsLint 和 Prettier

对于大型项目，让所有开发人员遵循一致的代码风格可能很棘手。您可以借助两个很棒的库`eslint`和`prettier`.

* EsLint 充当项目的 linter 和静态类型检查器
* Prettier 有助于实现一致的样式和间距等。

您可以从这里了解有关它们的更多信息。

[https://javascript.plainenglish.io/how-to-add-linting-and-formatting-for-your-react-app-78227b328910](https://javascript.plainenglish.io/how-to-add-linting-and-formatting-for-your-react-app-78227b328910)

## 14.打字稿

拥有打字稿设置可以很大程度上提高您和您的团队的生产力。

可能需要一些时间来适应，但对于大型项目来说，这是一笔巨大的投资。将来可以节省大量的时间。

即使您现在正在开发 javascript 项目，您也可以将 typescript 增量添加到您的项目中，因为 typescript 是 javascript 的超集。

## 15. 分析

对于企业应用程序来说，分析是最重要的部分之一。您可以跟踪谁在使用您的应用程序以及他们如何使用您的应用程序

* [React-ga](https://github.com/react-ga/react-ga)：Google Analytics for React 的官方实现

[https://javascript.plainenglish.io/how-to-setup-and-add-google-analytics-to-your-react-app-fd361f47ac7b](https://javascript.plainenglish.io/how-to-setup-and-add-google-analytics-to-your-react-app-fd361f47ac7b)

## 16. 测试

为您的应用程序提供一定量的测试覆盖率非常重要。

您应该有一个适当的测试环境设置。您可以通过 . 自动获得该信息`create-react-app`。我最需要的库是

* [React-testing-library](https://testing-library.com/docs/react-testing-library/intro/)：用于测试 React 组件
* [jest](https://jestjs.io/)：用于 javascript 单元测试
* [cypress](https://www.cypress.io/)：端到端测试

这是为您准备的入门指南。

[https://betterprogramming.pub/everything-you-need-to-get-started-with-testing-in-react-e16819b0eba7](https://betterprogramming.pub/everything-you-need-to-get-started-with-testing-in-react-e16819b0eba7)

## 17. SEO 性能

如果您正在构建一个 SEO 很重要的应用程序（例如电子商务），那么您应该了解 SEO 的基础知识以及如何改进它。

[https://betterprogramming.pub/how-to-boost-the-seo-of-your-react-app-b1c36d272ddf](https://betterprogramming.pub/how-to-boost-the-seo-of-your-react-app-b1c36d272ddf)

否则，您可以构建一个在服务器端呈现的**同构应用程序。**为此，NextJS 或 GatsbyJS 可能是一个不错的选择。这是帮助您入门的资源。

[https://javascript.plainenglish.io/start-your-journey-with-next-js-958705cfc299](https://javascript.plainenglish.io/start-your-journey-with-next-js-958705cfc299)

## 18. 实用性

对于任何项目，我们都需要做一些常见的事情，为此我们需要外部库的帮助。他们之中有一些是

* [lodash](https://lodash.com/)：数据操作
* [date-fns](https://date-fns.org/)：日期处理

这些是最常见的需要记住的。

## 19. 码头工人

它不是一个重要的部分，但了解如何对你的 React 应用程序进行 docker 化是很有好处的。您可以从中获得一些真正的好处。

Docker 提供可移植性和效率。因此，请考虑在您的项目中设置 docker。您可以阅读以下文章来了解如何有效地 dockerize 您的 React 应用程序

[https://medium.com/javascript-in-plain-english/how-i-reduced-docker-image-size-from-1-43-gb-to-22-4-mb-84058d70574b](https://medium.com/javascript-in-plain-english/how-i-reduced-docker-image-size-from-1-43-gb-to-22-4-mb-84058d70574b)

## 20.持续交付

在这个自动化的世界中，您不必担心每次更改某些内容时都要部署应用程序。

因此，当您构建应用程序时，请记住进行持续交付设置。大多数时候，这是开发运营人员的工作，但了解该流程将帮助您了解全局。这是一个供您入门的工具

[https://javascript.plainenglish.io/continuous-deployment-pipeline-for-react-apps-886f887996f8](https://javascript.plainenglish.io/continuous-deployment-pipeline-for-react-apps-886f887996f8)

### 结论

所以就这样吧。如果我错过了什么，请告诉我。感谢您阅读这篇长文。

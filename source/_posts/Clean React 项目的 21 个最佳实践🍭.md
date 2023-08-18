---
abbrlink: ''
categories:
- - React
cover: https://hexo-admin.oss-cn-beijing.aliyuncs.com/image/2023/8/a2897f25c7cb438f70b0261903bc2df3.webp
date: '2023-08-18T11:14:54.575671+08:00'
description: Clean React 项目的 21 个最佳实践🍭
mathjax: true
swiper_index: 2
tags:
- react 最佳实践
title: Clean React 项目的 21 个最佳实践🍭
updated: 2023-8-18T13:27:58.460+8:0
---
# Clean React 项目的 21 个最佳实践

React 对于如何构建事物非常没有主见。这正是我们有责任保持项目整洁和可维护的原因。

今天，我们将讨论一些改善 React 应用程序健康状况的最佳实践。这些规则被广泛接受。因此，掌握这些知识是势在必行的。

一切都会用代码显示，所以系好安全带！

## 1.使用JSX速记

尝试使用 JSX 简写来传递布尔变量。假设你想要控制导航栏组件的标题可见性。

### 坏的

return (
<Navbar showTitle={true} />
);

### 好的

return(
<Navbar showTitle />
)

## 2.使用三元运算符

假设你想根据角色显示用户的详细信息。

### 坏的

const { role } = user;

if(role === ADMIN) {
return <AdminUser />
}else{
return <NormalUser />
}

### 好的

const { role } = user;

return role === ADMIN ? <AdminUser /> : <NormalUser />

## 3.利用对象文字

对象字面量可以帮助我们的代码更具可读性。假设您想根据角色显示三种类型的用户。您不能使用三元，因为选项数量超过两个。

### 坏的

const {role} = user

switch(role){
case ADMIN:
return <AdminUser />
case EMPLOYEE:
return <EmployeeUser />
case USER:
return <NormalUser />
}

### 好的

const {role} = user

const components = {
ADMIN: AdminUser,
EMPLOYEE: EmployeeUser,
USER: NormalUser
};

const Component = components[role];

return <Componenent />;
现在看起来好多了。

## 4. 使用片段

始终使用`Fragment`超过`Div`. 它可以保持代码整洁，并且也有利于性能，因为在虚拟 DOM 中创建的节点少了一个。

### 坏的

return (

<div>
     <Component1 />
     <Component2 />
     <Component3 />
  </div>  
)
### 好的

return (
<>
<Component1 />
<Component2 />
<Component3 />
</>
)

## 5. 不要在渲染中定义函数

不要在渲染中定义函数。尝试将渲染内部的逻辑保持在绝对最低限度。

### 坏的

return (
<button onClick={() => dispatch(ACTION_TO_SEND_DATA)}>    // NOTICE HERE
This is a bad example
</button>
)

### 好的

const submitData = () => dispatch(ACTION_TO_SEND_DATA)

return (
<button onClick={submitData}>
This is a good example
</button>
)

## 6. 使用备忘录

`React.PureComponent`并且`Memo`可以显着提高应用程序的性能。它们帮助我们避免不必要的渲染。

### 坏的

import React, { useState } from "react";

export const TestMemo = () => {
const [userName, setUserName] = useState("faisal");
const [count, setCount] = useState(0);

const increment = () => setCount((count) => count + 1);

return (
<>
<ChildrenComponent userName={userName} />
<button onClick={increment}> Increment </button>
</>
);
};

const ChildrenComponent =({ userName }) => {
console.log("rendered", userName);
return <div> {userName} </div>;
};
尽管子组件应该只渲染一次，因为 count 的值与`ChildComponent`. 但是，每次单击按钮时它都会呈现。

![转存失败，建议直接上传图片文件](转存失败，建议直接上传图片文件 )

### 好的

让我们将其编辑`ChildrenComponent`为：

import React ,{useState} from "react";

const ChildrenComponent = React.memo(({userName}) => {
console.log('rendered')
return <div> {userName}</div>
})
现在，无论您单击该按钮多少次，它只会在必要时呈现。

## 7.将CSS放入JavaScript中

编写 React 应用程序时避免使用原始 JavaScript，因为组织 CSS 比组织 JS 困难得多。

### 坏的

// CSS FILE

.body {
height: 10px;
}

//JSX

return <div className='body'>

</div>
### 好的


### 好的const bodyStyle = {
height: "10px"
}

return <div style={bodyStyle}>

</div>
## 8.使用对象解构


## 8.使用对象解构使用对象解构对你有利。假设您需要显示用户的详细信息。

### 坏的

return (
<>
<div> {user.name} </div>
<div> {user.age} </div>
<div> {user.profession} </div>
</>
)

### 好的

const { name, age, profession } = user;

return (
<>
<div> {name} </div>
<div> {age} </div>
<div> {profession} </div>
</>
)

## 9. 字符串道具不需要大括号

将字符串道具传递给子组件时。

### 坏的

return(
<Navbar title={"My Special App"} />
)

### 好的

return(
<Navbar title="My Special App" />
)

## 10. 从 JSX 中删除 JS 代码

如果任何 JS 代码不能用于渲染或 UI 功能，请将其移出 JSX。

### 坏的

return (

<ul>
    {posts.map((post) => (
      <li onClick={event => {
        console.log(event.target, 'clicked!'); // <- THIS IS BAD
        }} key={post.id}>{post.title}
      </li>
    ))}
  </ul>
);
### 好的

const onClickHandler = (event) => {
console.log(event.target, 'clicked!');
}

return (

<ul>
    {posts.map((post) => (
      <li onClick={onClickHandler} key={post.id}> {post.title} </li>
    ))}
  </ul>
);
## 11.使用模板文字

使用模板文字构建大字符串。避免使用字符串连接。它漂亮又干净。

### 坏的

const userDetails = user.name + "'s profession is" + user.proffession

return (

<div> {userDetails} </div>  
)
### **好的**

const userDetails = `${user.name}'s profession is ${user.proffession}`

return (

<div> {userDetails} </div>  
)
## 12. 按订单进口

始终尝试按特定顺序导入内容。它提高了代码的可读性。

### 坏的

import React from 'react';
import ErrorImg from '../../assets/images/error.png';
import styled from 'styled-components/native';
import colors from '../../styles/colors';
import { PropTypes } from 'prop-types';

### 好的

经验法则是保持导入顺序如下：

* 内置
* 外部的
* 内部的

所以上面的例子就变成了：

import React from 'react';

import { PropTypes } from 'prop-types';
import styled from 'styled-components/native';

import ErrorImg from '../../assets/images/error.png';
import colors from '../../styles/colors';

## 13.使用隐式返回

使用 JavaScript 隐含的功能`return`来编写漂亮的代码。假设您的函数执行简单的计算并返回结果。

### 坏的

const add = (a, b) => {
return a + b;
}

### 好的

const add = (a, b) => a + b;

## 14. 组件命名

始终对组件使用 PascalCase，对实例使用 CamelCase。

### 坏的

import reservationCard from './ReservationCard';

const ReservationItem = <ReservationCard />;

### 好的

import ReservationCard from './ReservationCard';

const reservationItem = <ReservationCard />;

## 15. 保留的道具命名

不要使用 DOM 组件 prop 名称在组件之间传递 prop，因为其他人可能不期望这些名称。

### 坏的

<MyComponent style="dark" />

<MyComponent className="dark" />
### 好的

<MyComponent variant="fancy" />
## 16. 行情

对 JSX 属性使用双引号，对所有其他 JS 使用单引号。

### 坏的

```

<Foo bar='bar' />

<Foo style={{ left: "20px" }} />
```

### 好的

<Foo bar="bar" />

<Foo style={{ left: '20px' }} />
## 17. 道具命名

如果 prop 值是 React 组件，则始终使用驼峰命名法作为 prop 名称或 PascalCase。

### 坏的

<Component
UserName="hello"
phone_number={12345678}
/>

### 好的

<MyComponent
userName="hello"
phoneNumber={12345678}
Component={SomeComponent}
/>

## 18. 括号中的 JSX

如果您的组件跨越一行以上，请始终将其括在括号中。

### 坏的

return <MyComponent variant="long">
<MyChild />
</MyComponent>;

### 好的

```

return (
    <MyComponent variant="long">
      <MyChild />
    </MyComponent>
);
```

## 19. 自闭合标签

如果您的组件没有任何子组件，请使用自闭合标签。它提高了可读性。

### 坏的

<SomeComponent variant="stuff"></SomeComponent>

### 好的

<SomeComponent variant="stuff" />
## 20.方法名称中的下划线

不要在任何内部 React 方法中使用下划线。

### 坏的

const _onClickHandler = () => {
// do stuff
}

### 好的

```

const onClickHandler = () => {
  // do stuff
}
```

## 21. 替代道具

始终在标签中包含 alt 属性`<img >`。并且不要在替代项中使用`picture`或 ，因为屏幕阅读器已经将元素宣布为图像。无需包括该内容。`image``property``img`

### 坏的

<img src="hello.jpg" />

<img src="hello.jpg" alt="Picture of me rowing a boat" />
### 好的

<img src="hello.jpg" alt="Me waving hello" />
## 结论

就这样吧。如果您已经做到了这一步，那么恭喜您！我希望您从本文中学到一两件事。

[个人博客网站](https://www.shanpersonage.com.cn/)🍷🍷

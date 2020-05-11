# **02-JSX简单介绍和使用**

> JSX是一个JavaScript的语法扩展。官方建议在React中使用JSX，当然也并非强迫。不使用的情况，后面介绍。

### **1.举个栗子**

- **创建一个元素并渲染**

```javascript
const name = 'Daniel Zhang'
const element = <h1>Hi,my name is { name }</h1> /*在JSX中嵌入表达式*/

/*渲染*/
ReactDOM.render(
  element,
  document.getElememtById('root')  /*root相当于Vue里面的app*/
)
```

> `{}`里面可以放置任何合法的`javascript`表达式,例如`1 + 1`，或者调用方法，如`getData(id)`

### **2.JSX 也是一个表达式**

> 也就是说，你可以在 `if` 语句和 `for` 循环的代码块中使用 JSX，将 JSX 赋值给变量，把 JSX 当作参数传入，以及从函数中返回 JSX


```javascript
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### **3.一些属性**

> 添加类的时候，应使用`camelCase`,例如`class`写成`className=""`

### **4.JSX 防止注入攻击**

> React DOM 在渲染所有输入内容之前，默认会进行`转义`。它可以确保在你的应用中，永远不会注入那些并非自己明确编写的内容。所有的内容在渲染之前都被转换成了字符串。这样可以有效地防止 `XSS`攻击。

### **4.不使用JSX**

> 其实，JSX代码进行编译的时候，`Bable`会调用一个`React.createElement()`函数

- **以下两种写法等效**

```javascript
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```javascript
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

> 意味着你可以直接写第二种方式
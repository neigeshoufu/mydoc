# **事件捕获与事件冒泡**

> 由于HTML是层级结构，这使得事件可以在多个地方得到处理。例如当一个button被点击，除了button本身可以处理这个事件，它的父亲、父亲的父亲也可以处理。

### **事件流阶段**

- 事件捕获
- 处于目标阶段
- 事件冒泡

### **事件冒泡**

> 从触发事件的元素开始，然后按照HTML层级结构往上走，这样所有的祖先都会处理事件。

- 例如

```html
<div id="parent">
    <h2>parent</h2>
    <div id="child_1">
      <h2>child_1</h2>
      <div id="child_2">
        <h2>child_2</h2>
      </div>
    </div>
  </div>
```

事件冒泡

```js
<script type="text/javascript">
    document.querySelector('#parent').addEventListener('click', e => {
      console.log('parent')
    })

    document.querySelector('#child_1').addEventListener('click', e => {
      console.log('child_1')
    })

    document.querySelector('#child_2').addEventListener('click', e => {
      console.log('child_2')
    })
  </script>
```

结果

![bubble](/img/bubble_1.png)

点击`child_2`的时候，会从最下面的节点冒泡到父亲节点

### **事件捕获**

> 捕获是从根节点开始，一直到具体的某个节点

```js
<script type="text/javascript">
    document.querySelector('#parent').addEventListener('click', e => {
      console.log('parent')
    }, true)

    document.querySelector('#child_1').addEventListener('click', e => {
      console.log('child_1')
    }, true)

    document.querySelector('#child_2').addEventListener('click', e => {
       //e.stopImmediatePropagation()
      console.log('child_2')
    }, true)
  </script>
```

结果

![catch](/img/catch.jpg)
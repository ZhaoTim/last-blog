---
title: "Build Your React"
dropCap: false
---

```jsx
const element = <h1 title='foo'>Hello World!</h1>
const container = document.getElementById('container');
ReactDom.render(element, container);
```

这是一个最简单的REACT应用，第一行使用了JSX语法声明了一个REACT元素，第二行获取到containerDOM，第三行将REACT元素渲染到containerDOM内。现在，我们使用纯JS语法来重写他，从而实现自己的REACT。

```js
const element = {
    type: 'h1',
    props: {
        title: 'foo',
        children: 'Hello World!',
    },
};
const container = document.getElementById('container');

const node = document.createElement(element.type);
node['title'] = 'foo';

const textNode = document.createTextNode('');
textNode['nodeValue'] = 'Hello World!';

node.appendChild(textNode);
container.appendChild(node);
```

以上就是REACT在做的事情！接下来，自己实现REACT.createElement和render。

```jsx
function createElement (type, props, ...children) {
  return {
    type,
    props: {
      ...props,
      children: children.map(child  => {
        return typeof child === 'object' ? child : createTextElement(child)
      })
    }
  }
}

function createTextElement(val) {
  return {
    type: 'TEXT_ELEMENT',
    props: {
      nodeValue, val,
      children: [],
    }
  }
}
```




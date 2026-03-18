# Airbnb React 代码规范

> GitHub: https://github.com/airbnb/javascript/tree/master/react

---

## 目录

- [基本规则](#基本规则)
- [Class vs React.createClass](#class-vs-reactcreateclass)
- [命名](#命名)
- [声明](#声明)
- [对齐](#对齐)
- [引号](#引号)
- [空格](#空格)
- [属性](#属性)
- [Refs](#refs)
- [括号](#括号)
- [标签](#标签)
- [方法](#方法)
- [排序](#排序)
- [isMounted](#ismounted)

---

## 基本规则

### 只有一个 React 组件

- 每个文件只包含一个 React 组件

```jsx
// bad
const Foo = () => <div />;
const Bar = () => <div />;

// good
const Foo = () => <div />;
```

### 使用 JSX 语法

- 始终使用 JSX 语法
- 不要使用 React.createElement

```jsx
// good
const Hello = () => <div>Hello</div>;
```

---

## Class vs React.createClass

### 使用 class extends React.Component

```jsx
// bad
const Listing = React.createClass({
  // ...
});

// good
class Listing extends React.Component {
  // ...
}
```

---

## 命名

### 文件扩展名

- 使用 `.jsx` 扩展名

### 文件名

- 使用 PascalCase

```jsx
// good
ReservationCard.jsx
ReservationCard.test.jsx
```

### 组件命名

- 使用 PascalCase

```jsx
// bad
const reservationCard = (props) => <div />;

// good
const ReservationCard = (props) => <div />;
```

### 高阶组件命名

```jsx
// good
const withFoo = (Component) => {
  const WithFoo = (props) => <Component {...props} foo />;
  WithFoo.displayName = `withFoo(${Component.displayName || Component.name})`;
  return WithFoo;
};
```

---

## 声明

### 不要使用 displayName

```jsx
// bad
export default React.createClass({
  displayName: 'ReservationCard',
  // ...
});

// good
export default class ReservationCard extends React.Component {
  // ...
}
```

---

## 对齐

### JSX 属性对齐

```jsx
// bad
<Foo superLongParam="bar"
     anotherSuperLongParam="baz" />

// good
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>
```

---

## 引号

### JSX 属性使用双引号

```jsx
// bad
<Foo bar='bar' />

// good
<Foo bar="bar" />
```

---

## 空格

### 自闭合标签前加空格

```jsx
// bad
<Foo/>

// good
<Foo />
```

---

## 属性

### 属性名使用 camelCase

```jsx
// bad
<Foo
  UserName="hello"
  phone_number={12345678}
/>

// good
<Foo
  userName="hello"
  phoneNumber={12345678}
/>
```

### 省略属性值为 true

```jsx
// bad
<Foo
  hidden={true}
/>

// good
<Foo
  hidden
/>
```

---

## Refs

### 使用回调函数

```jsx
// bad
<Foo
  ref="myRef"
/>

// good
<Foo
  ref={(ref) => { this.myRef = ref; }}
/>
```

---

## 括号

### 多行 JSX 使用括号

```jsx
// bad
render() {
  return <MyComponent variant="long body" foo="bar">
           <MyChild />
         </MyComponent>;
}

// good
render() {
  return (
    <MyComponent variant="long body" foo="bar">
      <MyChild />
    </MyComponent>
  );
}
```

---

## 标签

### 没有子元素时自闭合

```jsx
// bad
<Foo className="stuff"></Foo>

// good
<Foo className="stuff" />
```

---

## 方法

### 使用箭头函数绑定

```jsx
// bad
class extends React.Component {
  onClickDiv() {
    // ...
  }

  render() {
    return <div onClick={this.onClickDiv.bind(this)} />;
  }
}

// good
class extends React.Component {
  onClickDiv = () => {
    // ...
  }

  render() {
    return <div onClick={this.onClickDiv} />;
  }
}
```

---

## 排序

### 组件内部排序

1. `constructor`
2. `getChildContext`
3. `componentWillMount`
4. `componentDidMount`
5. `componentWillReceiveProps`
6. `shouldComponentUpdate`
7. `componentWillUpdate`
8. `componentDidUpdate`
9. `componentWillUnmount`
10. 点击/事件处理方法
11. `render` 的 getter 方法
12. `render`

---

## isMounted

### 不要使用 isMounted

```jsx
// bad
if (this.isMounted()) {
  // ...
}

// good
this._isMounted = true;

componentWillUnmount() {
  this._isMounted = false;
}

if (this._isMounted) {
  // ...
}
```

---

## 参考资料

- [Airbnb React/JSX Style Guide (GitHub)](https://github.com/airbnb/javascript/tree/master/react)

---

*本文档基于 Airbnb React/JSX Style Guide 整理*

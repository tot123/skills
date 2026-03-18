# Google HTML/CSS 代码规范

> 官方文档：https://google.github.io/styleguide/htmlcssguide.html

---

## 目录

- [通用规则](#通用规则)
- [HTML 规则](#html-规则)
- [CSS 规则](#css-规则)

---

## 通用规则

### 文件编码

- 使用 **UTF-8** 编码（无 BOM）

### 注释

- 尽可能解释代码
- 使用完整的句子

---

## HTML 规则

### 文档类型

- 使用 HTML5

```html
<!DOCTYPE html>
```

### 小写字母

- 所有元素和属性使用小写

```html
<!-- 正确 -->
<div class="container">
  <img src="image.png" alt="description">
</div>

<!-- 错误 -->
<DIV CLASS="container">
  <IMG SRC="image.png" ALT="description">
</DIV>
```

### 省略引号

- 属性值不含特殊字符时可省略引号

```html
<!-- 正确 -->
<input type="text" class="form-control">

<!-- 不推荐 -->
<input type="text" class="form-control">
```

### 布尔属性

- 省略属性值

```html
<!-- 正确 -->
<input type="checkbox" checked>
<option selected>Option</option>
```

### 缩进

- 使用 **2 个空格**

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

### 语义化

- 使用语义化标签

```html
<!-- 正确 -->
<article>
  <header>
    <h1>Title</h1>
  </header>
  <section>
    <p>Content</p>
  </section>
  <footer>
    <p>Footer</p>
  </footer>
</article>
```

### 多媒体后备

- 提供后备内容

```html
<video controls>
  <source src="video.mp4" type="video/mp4">
  <p>您的浏览器不支持视频标签</p>
</video>
```

---

## CSS 规则

### 选择器命名

- 使用小写字母和连字符

```css
/* 正确 */
.nav-list {}
.user-profile {}
.card-header {}

/* 错误 */
.navList {}
.userProfile {}
.card_header {}
```

### ID 和类名

- 使用有意义的名称

```css
/* 正确 */
.video-list {}
.author-bio {}

/* 错误 */
.list1 {}
.bio {}
```

### 简写属性

- 尽可能使用简写

```css
/* 正确 */
padding: 10px 20px;
margin: 0 auto;
border: 1px solid #ccc;

/* 不推荐 */
padding-top: 10px;
padding-right: 20px;
padding-bottom: 10px;
padding-left: 20px;
```

### 0值不带单位

```css
/* 正确 */
margin: 0;
padding: 0;

/* 错误 */
margin: 0px;
padding: 0em;
```

### 十六进制颜色

- 3 位十六进制表示法

```css
/* 正确 */
color: #fff;
background: #000;

/* 不推荐 */
color: #ffffff;
background: #000000;
```

### 声明顺序

按以下顺序组织：
1. Positioning
2. Box model
3. Typographic
4. Visual

```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box model */
  display: flex;
  width: 100px;
  height: 100px;
  margin: 10px;
  padding: 10px;

  /* Typographic */
  font-size: 14px;
  line-height: 1.5;
  text-align: center;

  /* Visual */
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 4px;
}
```

### 媒体查询

- 放在相关规则附近

```css
.element {
  font-size: 14px;
}

@media (min-width: 768px) {
  .element {
    font-size: 16px;
  }
}
```

---

## 参考资料

- [Google HTML/CSS Style Guide (官方)](https://google.github.io/styleguide/htmlcssguide.html)

---

*本文档基于 Google HTML/CSS Style Guide 整理*

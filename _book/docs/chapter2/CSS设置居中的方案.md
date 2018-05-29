# CSS设置居中的方案

块级元素居中 html代码部分
```html
<div class="parent">
   <div class="child">child</div>
</div>
```

行内元素居中 html代码部分
```html
<div class="parent">
   <span class="child">child</span>
</div>
```

## 水平居中

### 行内元素 text-align: center;

```css
.parent {
   text-align: center;
}
```

### 块级元素 margin: auto;
> （低版本浏览器还需要设置 text-align: center;）

```css
.parent {
    text-align: center; 
}
.child {
    margin: auto; 
}
```

## 垂直居中

### 行内元素（单行文字垂直居中）
```css
.parent {
   height: 200px;
   line-height: 200px;
}
```

### 块级元素：绝对定位（需要提前知道尺寸）
> 优点：兼容性不错
> 缺点：需要提前知道尺寸

```css
.parent {
    position: relative;
    height: 200px;
}
.child {
    width: 80px;
    height: 40px;
    background: blue;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-top: -20px;
    margin-left: -40px;
}
```
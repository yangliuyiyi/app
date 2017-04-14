# 前言
移动重构CSS相关部分，包括编码、字体、touch相关、硬件加速、兼容问题等。

### 编码
```
@charset "UTF-8";
```

### 字体设置

```
body { 
    font-family: "Helvetica Neue", Helvetica, STHeiTi, sans-serif; 
}
```

### 盒模型
```
*, *:before, *:after {
  -webkit-box-sizing: border-box;
  
  box-sizing: border-box;
}
```

### 上下拉动滚动条时卡顿、慢
```
E {
    -webkit-overflow-scrolling: touch;
    overflow-scrolling: touch;
}
```
Android3+和iOS5+支持CSS3的新属性为overflow-scrolling

### 禁止复制、选中文本
E {
    -webkit-user-select: none;
    -moz-user-select: none;
    -khtml-user-select: none;
     user-select: none;
}
解决移动设备可选中页面文本(视产品需要而定)

### 长时间按住页面出现闪退

E {
    -webkit-touch-callout: none;
}

### iphone及ipad下输入框默认内阴影
E {
    -webkit-appearance: none; 
}

### 更改输入框placeholder的颜色
```
input::-webkit-input-placeholder { color:#999; }
input:focus::-webkit-input-placeholder { color:#333; }
```
placeholder的文字在ios下可以换行，android不行

### ios和android下触摸元素时出现半透明灰色遮罩
```
E {
    -webkit-tap-highlight-color:rgba(255,255,255,0)
}
```
设置alpha值为0就可以去除半透明灰色遮罩，备注：transparent的属性值在android下无效。

### active兼容处理
```
<body ontouchstart="">
```
### 动画定义3D启用硬件加速
```
E {
    -webkit-transform:translate3d(0, 0, 0)
    transform: translate3d(0, 0, 0);
}
```
注意：3D变形会消耗更多的内存与功耗

### Retina屏的1px边框
```
E {
    border-width: thin;
}
```
### webkit mask 兼容处理  blur

某些低端手机不支持css3 mask，可以选择性的降级处理。

比如可以使用js判断来引用不同class：
```
if( 'WebkitMask' in document.documentElement.style){
    alert('支持mask');
} else {
    alert('不支持mask');
}
```

### 旋转屏幕时，字体大小调整的问题
```
html, body, form, fieldset, p, div, h1, h2, h3, h4, h5, h6 {
    -webkit-text-size-adjust:100%;
}
```

### transition闪屏
```
/*设置内嵌的元素在 3D 空间如何呈现：保留3D */ 
-webkit-transform-style: preserve-3d;

/* 设置进行转换的元素的背面在面对用户时是否可见：隐藏 */
-webkit-backface-visibility:hidden;
```
### 圆角bug
某些Android手机圆角失效
```
background-clip: padding-box;

```
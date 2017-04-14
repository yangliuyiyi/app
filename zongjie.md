平台选择
• MediaQuery
• 文字排版
• 流体布局
• 图片载入
• Dom操作性能优化
• 触屏事件


ViewPort Meta

<meta name="viewport" content=" width=device-width,
initial-scale=1">

ViewPort Meta 参数
  width=device-width
• user-scalable=1
• initial-scale=1
• maximum-scale=1
• minimum-scale=1

ViewPort 参数最佳组合
<meta name="viewport" content="width=device-width,
initial-scale=1,maximum-scale=1">

MediaQuery书写思路 先写⾼分辨率样式

字体样式定义 reset.css
body {
font-family:
tahoma,arial,\5b8b\4f53,sans-serif;
}
html {
-webkit-text-size-adjust: 100%;
}

iOS ：华⽂细黑 + Helvetica
Android ：⽂泉驿微⽶黑 + Droid Sans


设备适配只能在前端完成？
服务器端实现的“响应式”
RESS  Responsive Design + Server Side Components



如果抛开“兼容性”

<!doctype html>
<html manifest="http://www.../pad-sport-cache.php">
<head>
<!—ViewPortMeta设置，禁止手动缩放-->
<meta name="viewport" content="
width=device-width,
initial-scale=1,
maximum-scale=1">
<!--屏蔽拨号链接-->
<meta name="format-detection" content="telephone=no" />
<!--隐藏浏览器导航栏-->
<meta name="apple-mobile-web-app-capable" content="yes" />
<link rel="apple-touch-icon"
sizes="72x72"
href="http://cdn/img-72-72.png" />
</head>

多了⼏个新属性
<meta name="apple-mobile-web-app-capable"
content="yes">
<meta name="apple-mobile-web-app-status-bar-style"
content="black" />
<!--不自动将地址和email转为链接-->
<meta name="format-detection"
content="address=no;email=no" />
<!--添加到主屏时的图标-->
<link rel="apple-touch-icon-precomposed"
href="http://cdn/img-114-114.png">
<link rel="apple-touch-startup-image"
href="http://cdn/img-320-460.png">

将网页添加到主屏

添加到主屏的icon
apple-touch-icon-precomposed 添加到桌面时有圆角/高光修饰
apple-touch-icon 只处理圆角,没有高光修饰
icon原图

终端事件的渐进增强
淘宝使用最多的  Slide/Switchable 让他们支持touch事件
触屏事件不要用ʼclickʼ代替

YUI Slide http://jayli.github.com/gallery/yuislide/


触屏touch事件
if ('ontouchstart' in document.documentElement) {
node.delegate('touchstart‘, function(e){
var x = e.changedTouches[0].clientX;
//…
});
node.delegate('touchend‘, function(e){
var x = e.changedTouches[0].clientX;
//…
});
node.delegate("touchmove",function(e){
var current_x = e.touches[0].pageX;
});
//…
}


空间位移事件
if(window.DeviceMotionEvent) {
window.addEventListener('devicemotion',function(e){
var acceleration = e.accelerationIncludingGravity;
var x = acceleration.x,
y = acceleration.y,
z = acceleration.z;
//…
},false);
}

HTML5 和 Native App 如何对接?
1，Web App 服务可以适时更新
Native App软件更新需要重新安装 ？
2，Web App 开发周期相对较短
Native App和Web App之间的分别？

PhoneGap 提供了一些思路
将HTML5 App打成安装包，但包升级时无法自动更新
HTML5 App + NativeApp
HTML5快速开发原型+打包至NativeApp框架中


移动Web中的性能问题！
1，低端设备众多
2，系统分配给浏览器的资源有限
http://is.gd/hApzIp
3，简化的浏览器实现
4，不少老旧引擎
5，需要高性能支持的HTML5 OPOA

和PC平台相比
1，性能问题会被放大数倍
2，很容易造成体验瓶颈

Web App 的性能优化
1. 处理性能（CPU & RAM）
• Reflow & Repaint
• CSS3的性能问题
• 动画
• JS中的内存控制
• ⾼效的JS技巧
• 关于电量
• HTML5带来的优化
2. 网络性能 Network

需要优化的两个核心
1. 减少内存中存储的内容
2. 减少CPU的 实时运算消耗

减少Reflow & Repaint
1. off-document 避免直接操作DOM
2. 一次性修改样式
3. 让Dom脱离文档流
4. 减少Dom数量和深度
5. Dom复用

1.off-document:文档片段
var fragment = document.createDocumentFragment(),
list = [‘foo’,’bar’,’baz’],elem,contents;
for (var i = 0; i<list.length; i++){
elem = document.createElement(‘div’);
content = document.createTextNode(list[i]);
fragment.appendChild(content);
}
document.body.appendChild(fragment);

1.off-document:节点克隆
var tmpnode = document.getElementById(‘container’),
clone = tmpnode.cloneNode(true),
list = [‘foo’,’bar’,’baz’],elem,contents;
clone.setAttribute(‘width’,’50%’);
for(var i = 0; i<list.length; i++){
elem = document.createElement(‘div’);
content = document.createTextNode(list[i]);
clone.appendChild(elem);
}
original.parentNode.replaceChild(clone,original);


off-document:block-none-block
var subElem = document.create(‘div’),
elem = document.getElementById(‘animated’);
elem.style.display = ‘none’;
elem.appendChild(subElem);
elem.style.width = ‘320px’;
elem.style.height = ‘480px’;….
elem.style.display = ‘block’;

2.一次性修改样式
<style type=“text/css”>
div { background:white; color:black; }
div.active { background:blue; color:white; }
</style>
<script>
$(‘#styled’).addClass(‘active’);
</script>

3.让元素脱离文档流
.selector1 {
position:absolute;
}
.selector2 {
position:fixed;
}

4.减少Dom数量和深度
瓶颈1：节点reflow，子元素/后续元素都会reflow
瓶颈2：DOM尺寸会减慢所有操作


5.DOM复用
建立Dom复用池,避免频繁创建和销毁；使用前端模板

CSS3 性能问题！




微信小程序开发文档
https://mp.weixin.qq.com/debug/wxadoc/dev/index.html?t=201741
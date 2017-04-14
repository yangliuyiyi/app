# 页面布局结构
# 移动端JavaScript库  zepto.js  touch.js swiper.js
- 原生布局 样式重置
- mui布局

# html5+ 页面布局
index = index_header + index_content
list = list_header + list_content
show = show_header + show_content

# html5+ webview
## 获取所有Webview窗口
plus.webview.all();


## 获取当前窗口 currentWebview
获取当前窗口的WebviewObject对象
plus.webview.currentWebview();


## 查找指定标识的WebviewObject窗口
查找指定标识的WebviewObject窗口 getWebviewById
plus.webview.getWebviewById( id );


## 获取应用首页
获取应用首页WebviewObject窗口对象getLaunchWebview
plus.webview.getLaunchWebview();



## 显示Webview窗口show
显示已创建或隐藏的Webview窗口，需先获取窗口对象或窗口id，并可指定显示窗口的动画及动画持续时间。
plus.webview.show( id_wvobj, aniShow, duration, showedCB, extras );
				

## 创建并打开Webview窗口 open
plus.webview.open( url, id, styles, aniShow, duration, showedCB );
创建并显示Webview窗口，用于加载新的HTML页面，可通过styles设置Webview窗口的样式，创建完成后自动将Webview窗口显示出来。





## 关闭Webview窗口
plus.webview.close( id_wvobj, aniClose, duration, extras );
关闭已经打开的Webview窗口，需先获取窗口对象或窗口id，并可指定关闭窗口的动画及动画持续时间。



# html5+

html5+ 是一个js库，可以让我们以JavaScript方式去调用手机设备

## 使用html5+
等待html5+运行环境准备完成
document.addEventListener('plusready',function(){})

webView
# 获取当前webview
plus.webview.currentWebview();
# 新建webview
plus.webview.create(模板地址,窗口id,窗口样式)
plus.webview.create("_www/templates/index-header.html","templates/index-header.html",{width:"100%",height:"40px"})


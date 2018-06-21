# GetMiniProgram
微信小程序

## 基础语法

### 一. WXML特性
数据绑定, 列表渲染, 条件渲染, 模板引用
#### 1. 数据绑定
使用{{}}语法(mustache), 进行绑定
```
<view hidden="{{flag ? true : false}}" data-name="{{name}}  ">{{data}}</view>
```

微信小程序开发框架属性: id, class, style, hidden, data-\*(自定义属性), bind\*/cathch*(组件事件)

#### 2. 列表渲染
```
<view>
	<block wx:for="{{items}}" wx:for-item="item" wx:key="index">
		<view>{{idnex}}:{{item.name}}</view>
	</block>
</view>
```

#### 3. 条件渲染
```
<view wx:if="">
</view>
<view wx:elif="">
</view>
<view wx:else>
</view>
```
补充: 元素频繁切换, 建议使用hidden

#### 4. 模板引用
```
<!-- index.wxml -->
<template name="tempItem">
	<view>
		<view>收件人: {{name}}</view>
		<view>地址: {{address}}</view>
	</view>
</template>

<!-- 使用 -->
<template is="tempItem" data="{{..item}}"></template>

// index.js
Page({
	data: {
		item: {
			name: 'jack',
			address: '中国'
		}
	}
})
```

使用import 引入模板, import 是有作用域的(可以避免循环引入)
```<import src="index.wxml"></import>```
使用include 引入模板


### 二. WXSS特性
wxss是一套样式语言, 用于描述 WXML 的组件样式

#### 1. rpx单位
设备像素(device pixels), CSS像素(CSS pixels), PPI/DPI(pixel per inch), DPR(devicepixelRatio)

rpx 最终会转化为 rem 

#### 2. 外部样式导入
外联样式
@import './style,wxss'

内联样式
```
<view style="width:12rpx;background:{{color}}"></view>
```

#### 3. 选择器
优先级: !import(∞) > style(1000) > #element(100) > .element(10) > element(1)


### 三. JavaScript
微信小程序在不同平台运行环境:
iOS -> JavaScriptCore
Android -> X5内核
IDE -> nwjs


### 四. WXS
模板, 变量, 注释, 运算符, 语句, 数据类型, 基础类库

wxs 是对 JavsScript 上层封装


### 五. MINA 架构
View(视图层): page(WXML, WXSS)
App Service(逻辑层): Manager API
Native(系统层): JSBridge, 微信能力, 离线存储, 网络请求


## 小程序实操
### 一. 小程序运行机制
启动: 冷启动, 热启动

#### 1.生命周期
程序生命周期: onLaunch, onShow, onHide, onError  (进去小程序, 按home键等操作)

页面生命周期: onLoad, onShow, onReady, onHide, onUnload

两个线程:
AppService thread, View Thread


### 二. 小程序路由
#### 1.路由变化方式
初始化   ->    新页面入栈
打开新页面   ->   新页面入栈
页面重定向   ->   当前页面出栈, 新页面入栈
页面返回    ->    页面不出栈, 查到目标返回页, 新页面入栈
Tab切换   ->   页面全部出栈, 只留下新的 Tab 页面
重加载   ->    页面全部出栈, 只留下新的页面


#### 2.代码操作路由变化
打开新页面: 调用API wx.navigateTo 或者使用组件 ```<navigator open-type="navigateTo"></navigator>```

页面重定向: 调用API wx.redirectTo 或者使用组件 ```<navigator open-type="redirectTo"></navigator>```

页面返回: 调用API wx.navigateBack 或者使用组件 ```<navigator open-type="navigateBack"></navigator>```

Tab切换:  调用API wx.switchTab 或者使用组件 ```<navigator open-type="switchTab"></navigator>```

重启动: 调用API wx.reLaunch 或者使用组件 ```<navigator open-type="reLaunch"></navigator>```


### 三. 小程序事件流
```
<!-- index.wxml -->
<view class="btn" bindtap="clickMe">
	点击我
</view>
<!-- index.js -->
Page({
	clickMe (e) {
		console.log(e)
	}
})
```
#### 1. 事件类型
事件捕获阶段, 事件处理阶段, 事件冒泡阶段 

#### 2. 事件操作
可捕获事件: touchstart, touchmove, touchcancel, touchend, tap, longpress, longtap

可冒泡事件: touchstart, touchmove, touchcancel, touchend, tap, longpres, longtap, transitionend, animationstart, animationiteration, animationend, touchforcechange


### 四. 组件
媒体组件, 地图, 开放能力, 画布, 视图容器, 基础内容, 表单组件, 导航

#### 1.视图容器
view, scroll-view, swiper, movable-view, cover-view

### 五. 微信小程序API



---
title: 小程序webview调研与Map组件
tags: 
  - miniProgram
  - webview
date: 2018-05-04 14:41:36
---
### webview
- [官方文档](https://developers.weixin.qq.com/miniprogram/dev/component/web-view.html)
- 使用
```html
<!-- wxml -->
<!-- 指向微信公众平台首页的web-view -->
<web-view src="https://mp.weixin.qq.com/" bindmessage="handleMsg"></web-view>
```
- 通信
小程序 => webview: 配置webview的src给url加参数即可
webview => 小程序: wx.miniProgram.postMessage
<!-- more -->
```
网页向小程序 postMessage 时，会在特定时机（小程序后退、组件销毁、分享）触发并收到消息。e.detail = { data }
小程序后退: navigateBack
组件销毁: redirectTo reLaunch
分享: 
```
- 优劣讨论 
  - 自由度高
  - 无法实时通信 

### 原生Map组件
- [官方文档](https://developers.weixin.qq.com/miniprogram/dev/component/map.html#map)
- 优劣分析
  - 地图事件不够细化，视野变化事件无法区分事件来源（修改地图中心点、手指双击缩放、拖拽地图）
  - 自由度不高，对于marker control等地图组件只能修改官方提供的属性
  - 地图原生组件层级最高，覆盖在地图上的需求必须包含在地图本身内
  - 地图元素层级无法控制
  - 动画限制：css 动画对 map 组件无效，体验生硬

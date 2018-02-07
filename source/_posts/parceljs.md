---
title: parceljs
tags: tags
date: 2018-02-02 15:23:16
---

### [parcel](https://github.com/parcel-bundler/parcel)
传闻中**极速零配置的打包神器**parceljs，官网中对于其的使用介绍极其简单
```javascript
	npm i parcel-bundler
	parcel index.html
```
官方给出的例子中，对于各个工具打包时间和结果文件夹大小进行了对比

Bundler	| Time
:--- | :---
browserify | 22.98s
webpack | 20.71s
parcel | 9.98s
parcel - with cache | 2.64s

### Why
- parcel内置很多资源文件的parser
![parser](/assets/blogImg/parcel-parser.png) 
<!-- more -->
- 多核（通过 worker 平行构建）

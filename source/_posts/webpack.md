---
title: 关于webpack
tags: 
  - js
date: 2018-01-02
---
### 常用的插件
- [HtmlWebpackPlugin](https://github.com/jantimon/html-webpack-plugin)
  - 自动生成入口文件，并引入外部资源
  - 实现原理： 将 webpack中`entry`配置的相关入口thunk  和  `extract-text-webpack-plugin`抽取的css样式   插入到该插件提供的`template`或者`templateContent`配置项指定的内容基础上生成一个html文件，具体插入方式是将样式`link`插入到`head`元素中，`script`插入到`head`或者`body`中。
- [ManifestPlugin](https://github.com/danethurber/webpack-manifest-plugin)
  - This will generate a manifest.json file in your root output directory with a mapping of all source file names to their corresponding output file, for example:
  ```json
  {
	   "app.js": "app.bundle.js",
	   "index.js": "index.bundle.js"
	}
  ```

### 利用code split实现分批打包，按需下载
之前使用webpack，是将所有的资源All in one地打包进一个文件中，但实际场景中，
```javascript
```
---
title: hexo-generator-search
tags: [hexo,性能测试]
categories: 工具
toc: true
---


生成搜索 data   Hexo  3。x   4. x。这个插件    用于生成  搜索索引 文件,  包含所有的必要  data    文章 你 可以使用 写 本地搜索引擎   博客。JSON支持  XML 和   输出格式。

## 安装
```shell
$ npm install hexo-generator-search --save
```

## 配置

```yml
search:
  path: search.xml
  field: post
  content: true
```


如果需要排除搜索，只要在indexing:false 即可
```
---
title: "Code Highlight"
date: "2014-03-15 20:17:16"
tags: highlight
categories: Demo
description: "A collection of Hello World applications from helloworld.org."
toc: true
indexing: false
---
```
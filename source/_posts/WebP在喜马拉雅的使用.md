---
title: WebP在喜马拉雅的使用
date: 2020-09-04 10:45:13
tags:
---

## 背景

不管是 PC 还是移动端，图片一直是流量大头，以苹果公司 Retina 产品为代表的高 PPI 屏对图片的质量提出了更高的要求，如何保证在图片的精细度不降低的前提下缩小图片体积，成为了一个有价值且值得探索的事情。

但如今对于 JPEG、PNG 和 GIF 这些图片格式的优化几乎已经达到了极致， 若想改变现状开辟新局面，便要有釜底抽薪的胆量和气魄，而 Google 给了我们一个新选择：WebP。


## 了解WebP

### 什么是WebP

WebP，是一种支持有损压缩和无损压缩的图片文件格式，派生自图像编码格式 VP8。根据 Google 的测试，无损压缩后的 WebP 比 PNG 文件少了 45％ 的文件大小，即使这些 PNG 文件经过其他压缩工具压缩之后，WebP 还是可以减少 28％ 的文件大小。

### WebP的优点

WebP 的优势体现在它具有更优的图像数据压缩算法，能带来更小的图片体积，而且拥有肉眼识别无差异的图像质量；同时具备了无损和有损的压缩模式、Alpha 透明以及动画的特性，在 JPEG 和 PNG 上的转化效果都相当优秀、稳定和统一。

![WebP](http://image.uisdc.com/wp-content/uploads/2014/12/20141212164211465-590x201.png)

### WebP的缺点

![测试数据](http://image.uisdc.com/wp-content/uploads/2014/12/20141215144323396.jpg)

* <font color=red>解码耗时：WebP 的解码时间是 PNG 格式的 4.4 倍（24.8ms）</font>
* 流畅程度：两种格式下，AIO 滑动流畅度无明显差异
* CPU使用：两种格式下，连续发送 15 个图片，CPU 使用均在 10%—26% 之间波动，两者无明显差异
* 内存占用：两者格式下，连续发送 15 个图片，内存占用跨度均为 11M，无明显差异

### WebP的浏览器兼容性

![浏览器兼容性](https://fdfs.xmcdn.com/group83/M05/DA/96/wKg5HV9RsCfC5zBDAAR68WSLiPY683.png)

### WebP的IOS客户端兼容情况
![喜马拉雅IOS客户端支持情况](https://fdfs.xmcdn.com/group86/M03/DB/30/wKg5Jl9RsJLBGTlXAAwm8yCMfQ0620.png)
IOS大部分还是不支持的

### WebP的Android客户端兼容情况
![喜马拉雅Android客户端支持情况](https://fdfs.xmcdn.com/group83/M01/DB/A3/wKg5I19Rv7aC0EjcAAZNDJm-DAQ644.png)
Android4.3以上全部支持

### 谁在使用WebP

2010 年发布的 WebP 已经不算是新鲜事物了，在 Google 的明星产品如 Youtube、Gmail、Google Play 中都可以看到 WebP 的身影，而 Chrome 网上商店甚至已完全使用了 WebP。国外公司如 Facebook、ebay 和国内公司如腾讯、淘宝、美团等也早已尝鲜。

![谁在使用WebP](https://fdfs.xmcdn.com/group87/M00/D9/B3/wKg5J19RwCCBqMFvAA_vZ6WNp_E130.png)

YouTube 的视频略缩图采用 WebP 格式后，网页加载速度提升了 10%；谷歌的 Chrome 网上应用商店采用 WebP 格式图片后，每天可以节省几 TB 的带宽，页面平均加载时间大约减少 1/3；Google+ 移动应用采用 WebP 图片格式后，每天节省了 50TB 数据存储空间。

### 喜马拉雅哪些项目在使用WebP

![喜马拉雅哪些项目在使用WebP](https://fdfs.xmcdn.com/group87/M0B/D9/C6/wKg5J19RwV2yZKGIABHJ9dQ0kns286.png)

### 实际效果

喜马拉雅PC站，某Banner图

![实际效果](https://fdfs.xmcdn.com/group83/M04/DB/D0/wKg5I19RwxKg-YgoAC2jJryPl7Q667.png)

### 实际效果2

云吸猫活动，背景大图

![实际效果2](https://fdfs.xmcdn.com/group82/M04/D8/69/wKg5HF9Rw6vg5CI8AAj0eUp--fc655.png)

## 如何在项目中使用WebP

### 图片组件

![@xmly/fast-image](https://fdfs.xmcdn.com/group83/M03/DB/A1/wKg5HV9RxOyj1InzAAJHONgJsJ4604.png)

## 总结

* WebP的优点
  - 同等质量下图片更小，而且支持有损和无损两种压缩模式
  - 压缩之后质量无明显变化，图片质量得到保证
* WebP的缺点
  - 兼容性问题
  - WebP在解码时间上比png的图片要长一些，由于减少图片大小，来提高加载速度，总体来说，还是利大于弊，所以不妨碍我们使用
* @xmly/fast-image
  - 屏蔽兼容性问题，动态判断是否选用WebP
  - 提供剪裁功能，进一步减少图片大小

## 相关文章

[@xmly/fast-image](http://gitlab.ximalaya.com/FEA/fast-image/fast-image)
[实时图片处理接口](http://thoughts.ximalaya.com/workspaces/5ce3850abe825bee8c09d4c7/docs/5ce3853bbe825bee8c09d5ea)
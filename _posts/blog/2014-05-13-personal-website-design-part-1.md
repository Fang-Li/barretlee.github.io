---
layout: post
title: 个人网站架构设计(一)
description: 从大二开始，坚持每月3到8篇的技术分享，到现在差不多两年了。一直在分享之中跟着大家一起进步，从最开始的点点网，到github，再到现在的博客园。分享是一件有趣的事情，能够收到很多的反馈，渐渐地，已经把写博当成一种习惯。
category: life
tags: website
---

从大二开始，坚持每月3到8篇的技术分享，到现在差不多两年了。一直在分享之中跟着大家一起进步，从最开始的点点网，到github，再到现在的博客园。分享是一件有趣的事情，能够收到很多的反馈，渐渐地，已经把写博当成一种习惯。

在不同的平台上写博客会有不同的感受，但是几乎没有哪个平台可以满足自己的所有需求，比如，期望没有广告、希望速度可以更快、自己可以更多的操作后端、找个地方放DEMO、有个NodeJS测试的环境、自定义样式和主题等等，对我这个喜欢折腾的人来说，这些需求真是太普通了，可惜，没有哪个平台可以提供这么多的服务。再如，我希望把更多的生活中元素或者情感的东西带到博客中来，这些平台貌似不太适合做这些事情。

无奈之下只好自己花点钱买个主机安置个人网站。搭建一个网站是一个系统学习前后端的最佳机会，之前考虑过使用别人的框架，快捷搞定一个博客平台，但是我希望这次的网站架设能够承受几十万甚至上百万的PV（哈哈，这个可能性几乎为零，主要为了提高标准），同时也支持一些诸如陌生人交流，网站爬虫归类等等附加的功能。用商业性网站的建站标准来规范化网站，也给自己一个实践的机会~

花了四五个小时整理了思路，考虑的东西有点多，所以通过文字将建站的整个过程记录下来。

### 1、网站定位

记录生活，分享交流。凸显交流。

### 2、设计理念

- 重视体验
- 数据在前端
- 实时更新
- 快、稳定、安全
- 自动化
- 低消耗、低流量

### 3、基本架构

	+------------------+     +------------------+
	| Frond-End        |     | Browser          |
	|     前端处理      |     +--------------+   |
	|                  |←---→| LocalStorage |   |
	+--↑-----↑-----↑---+     +--------------+---+
	   |     |     |                             
	+--↓-----↓-----↓---+     
	| NodeJS           |     +-------------+  
	|     处理I/O      |     | Database    |  
	|                  |←-+-→|             |  
	+-----|-----↑------+  |  |             |  
	      |     |         |  |             |
	+-----↓-----|------+  |  +----------+  |
	| PHP              |  |  |          |  |
	|     处理数据      |←-+-→|   cache  |  |
	|                  |     |          |  |
	+------------------+     +----------+--+  


三个重点：

- 前端数据缓存。数据放在本地LocalStorage中，用户每次访问网站，都会从数据库拉去数据，同步到本地。低版本IE基本快死绝了，这个降级处理。
- NodeJS 处理I/O，如果某个页面的单日访问量太大，不至于服务器扛不住。由于全站使用socket连接，利用NodeJS也便于后端编程。
- 数据库对针对访问频率进行cache。


### 4、基本模块

1. 留言，多个位置使用，组件化处理
2. 自动化分享，发布文章自动分享到 SNS 上
3. 防盗链/盗链
4. 数据自动备份
5. 后台发文系统
6. 提问交流平台
7. 陌生人交流模块
8. 最新资讯的爬虫
9. RSS聚合
10. QQ回复/邮件自动回复功能


后续会针对每个功能模块，进行详细的记录。
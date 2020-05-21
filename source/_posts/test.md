---
title: React笔记一
date: 2020-05-20 18:11:36
tags: [React]
categories: [React]
meta:
  header: [title, author, category,date,wordcount]
---
## js工具

<!-- more -->

- JSON
	String转json对象：`JSON.parse()`
	json对象转json String：`JSON.stringify()`
- 时间格式转换
```
	let sdate = new Date(r.create_time).toJSON();
 let sdate2 = new Date(+new Date(sdate) + 8 * 3600 * 1000).toISOString().replace(/T/g, ' ').replace(/\.[\d]{3}Z/, '');
 ```
- 百分比计算
	`Math.round(value/total*10000)/100.00`

---
title: React笔记一：工具与三方库
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

## 实用三方库

- json组件
```
	import ReactJson from 'react-json-view';
	<ReactJson src={this.state.jsonSrc} name={null}
        iconStyle="square" collapseStringsAfterLength={30} displayDataTypes={false} collapsed={false}
        style={{fontFamily:'微软雅黑'}}/>
```
- echarts组件
```
	import ReactEcharts from "echarts-for-react";
	import echartsTheme from '../../theme/tabletheme1';
	componentWillMount(){
        echarts.registerTheme('theme', echartsTheme);
    }
	<ReactEcharts option={this.getOption()}
        style={{height: 400}}
        theme="theme"></ReactEcharts>
```
- cookie操作
```
	import cookie from 'react-cookies';
```
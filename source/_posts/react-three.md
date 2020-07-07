---
title: 图表-echarts
date: 2020-07-07 18:22:24
tags: [React]
categories: [React]
meta:
  header: [title, author, category,date,wordcount]
---
## 图表echarts

<!-- more -->

### 主题
从官网导出主题js文件，将主题配置用`export default{}`封装，在页面代码中引入
```
import echarts from 'echarts/lib/echarts';
import ReactEcharts from "echarts-for-react";
import echartsTheme from '../../theme/tabletheme1';

class EchartsTest extends Component{

	componentWillMount(){
			//注册意图
			echarts.registerTheme('theme', echartsTheme);
	}
	
	getOption = () => {
        let option = {
            toolbox:{
                feature:{
                    saveAsImage:{
                        name:"test" + Date.parse(new Date()),
                    }
                }
            },
            title: {
                text: 'test',
                subtext: 'test',
                left: 'center'
            },
            legend: {
                orient: 'vertical',
                left: 'left',
                data: ['data1', 'data2']
            },
            series: [{
                name: 'test',
                type: 'pie',
                radius: '55%',
                center: ['50%', '50%'],
                label: {
                    normal: {
                        show: true,
                        formatter: '{b}: {c}({d}%)'
                    }
                },
                data: this.state.callNum,
                emphasis: {
                    itemStyle: {
                        shadowBlur: 10,
                        shadowOffsetX: 0,
                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                    }
                }
            }],

            tooltip:{
                show: true,
                trigger: 'item',
                formatter: '{a} <br/>{b} : {c} ({d}%)'
                //formatter: "{a0} <br/> {b} : {c0} <br/> {a1} <br/> {c1}%"
            }
        }
        return option;
    }
	
	render(){
		return(
		<ReactEcharts option={this.getOption()}
                                          style={{height: 400}}
                                          theme="theme"></ReactEcharts>
		);
	}
}

export default EchartsTest;	

```
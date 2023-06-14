# Knowledge
## flask- 安装与使用

1. 安装 Python
2. pip install flask flask_cors
3. python main.py

```py
import flask
from flask_cors import CORS
from flask import Flask
 
app=Flask(__name__)
app.config['TEMPLATES_QUTO_RELOAD'] = True
CORS(app)

@app.route('/')
def index():
	return flask.send_from_directory('static','index.html')
	
if __name__ == '__main__':
   app.run(debug = True)
```

### Scale是函数

```js
d3.scaleLinear 和 d3.scaleBand得到的返回值本质上是函数
给出数据中的值 domain
返回映射的值 range
domain()和range()可以理解为配置这个函数的过程
const xScale=d3.scaleLinear().domain([0,10]).range([0,innerWidth]);//scaleLinear()线性比例尺
const yScale=d3.scaleBand().domain([0,d3.max(data,d=>d.value)]).range([0,innerHeight])
.padding(0.1)//y轴中的留白，0.1===》1%     不是attr
const y=d3.scaleBand().domain([0,d3.max(data,d=>d.value)]).range([0,innerHeight])//scaleBand()序数比例尺 离散数，不连续
```
domain()数据范围，range()画布范围
d3.max(data,function)	 取最大值		data:数据本身	function:对每条数据的操作
data.map()数据列表，map(回调函数),返回一个数组，所以不需要[data.map()]

### 坐标轴
```js
const yAxis = d3.axisLeft(d3.scaleBand())	y轴
const xAxis = de.axisBottom(比例尺)			x轴//渲染
const g=svg.append('g')
g.append('g').call(yAxis);//显示出x,y轴

g.append("g").call(xAxis)//默认再上方
.attr('transform',`translate(0,${innerHeight})`);//将坐标移至下方
call() 把
```

### 画布
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/34e38c3e-a993-4a19-b679-98386c6b0413)

### 修改坐标的文字
.tick表示每一个刻度，用select可以选择,类名
tickSize()坐标轴的刻度线
```js
d3.selectAll("text").attr("fontSize","16px")//无效果
d3.selectAll(".tick text").attr("fontSize","2em")//无效果
d3.selectAll(".tick text").attr("font-size","2em")//有效果
```

### 文字居中：文字锚
```js
g.append("text").text("Member of 2PM").attr("font-size","3em")
.attr("transform",`translate(${innerWidth/2},0)`)
.attr("text-anchor","center")//容易犯错
.attr("text-anchor",'middle')
```
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/9bb85736-ca3d-419c-9f0a-56384b178946)

### forEach()函数
```js
data.forEach(d=>{		Array.forEach(d为每一个元素）
  g.append("rect")
  .attr("width",xScale(d.value))   
  .attr("height",yScale.bandwidth())  //y轴间隔
  .attr("fill","green")
  .attr("y",yScale(d.name));//y的位置
  console.log("xScale(d.value)"+xScale(d.value))
})
```
### 结果

![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/390fd9ca-cacf-4306-b28d-7f680272d789)


### 遇到的问题1
- +"String"----->number
- +("String")----->number
### 遇到的问题2
attr("width","100px")
attr("width")---->100px        +"100px"==NAN
#### 改进内容
1. 各个比例尺的关系，了解其他比例尺
2. 对坐标轴的配置，需更到的了解、学习

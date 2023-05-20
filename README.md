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
const xScale=d3.scaleLinear().domain([0,10]).range([0,innerWidth]);
```
domain()数据范围，range()画布范围
d3.max(data,function)	 取最大值		data:数据本身	function:对每条数据的操作
data.map()数据列表，map(回调函数)

### 坐标轴
```js
const yAxis = d3.axisLeft(d3.scaleBand())	y轴
const xAxis = de.axisBottom(比例尺)			x轴
const g=svg.append('g')
g.append('g').call(yAxis);
g.append('g').call(xAxis);
call() 把
```

### 画布
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/34e38c3e-a993-4a19-b679-98386c6b0413)

### 修改坐标的文字
.tick表示每一个刻度，用select可以选择
```js
d3.selectAll('.tick text').attr("font-size","2em")
```

### 文字居中：文字锚
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/9bb85736-ca3d-419c-9f0a-56384b178946)


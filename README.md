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


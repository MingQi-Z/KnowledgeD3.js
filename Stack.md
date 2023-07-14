
# 堆叠
- d3.stack()
- 本质上是D3.js提供的用于数据预处理的接口（或功能、模块）

```js
  let stack=d3.stack()
            .keys(数据属性)
            .order(谁在上)
//d3.stackOrderAsceding 升序
.order(d3.stackOrderAsceding)(数据）
//d3.stackOrderDescending 降序
```

![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/2c0e21ce-145b-4c57-b4b3-8ab5a4bc368e)

### monentjs库
日期的输出



### tips
坐标轴配置
.nice()//让坐标轴的宽度一致

naiveAxes()   //生成坐标
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/c3b7ca9a-1f9b-4030-9e86-80f73feca15c)

随机配色
```js
const color=d3.scaleOrdinal()
            .domain(['apple','banana','bear'])
            .domain(['black','red','yello'])
自带配色方案
d3.schemeSet3
```

data() 可以嵌套
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/8627d99e-a100-46cd-a59b-4ebcdba98f8c)
naiveStack作为一个二维数组，第一个data遍历外层
第二个data遍历内层
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/178811bf-b05c-46cb-bfce-8c5b72383c7a)
 ![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/c52dd2db-afa9-4a91-be05-542be9d1773d)


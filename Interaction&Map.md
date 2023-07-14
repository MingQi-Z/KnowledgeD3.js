## Json数据的读取
TopoJson是一个js库&&&GeoJson

```js
d3.json('/xx.json').then(data=>{
data==>是一个对象
topoJson===>GeoJson（转换）
let worldmeta=  topojson.feature(data,data.objects.countries);
})

```
## GeoPath与投影
- 如何将地形的数据映射到画布上
  - const projection = d3.geoNaturalEarth1()
  - const pathGenerator = d3.geoPath().projection(projection)
 
- 类似 "比例尺" ，地图要画在多大的画布上？
  - projection.fitSize([innerwidth,Height\],worldmeta);
 
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/440fbe64-218c-45a7-976a-1171f33835e8)

```js
            const projection = d3.geoNaturalEarth1();
            const geo = d3.geoPath().projection(projection);
            d3.json('').then(data=>{
                g.selectAll("path").data(worldmeta.features)
                .join("path")
                .attr('d',geo)
                .attr('stroke','black')
```



## 事件
- 事件的设置
  - d3.select("#example').on('eventName',callBack)
  - 图元.on(事件类型,触发动作)
 
- DOM Events
  - click
  - mouseover
  - mouseout
  - keydown
  - contextmenu
    - 右键单击事件：preventEven(坑）
  - https://developer.mozilla.org/en-US/docs/Web/Events
 
```js
     g.selectAll("path").data(worldmeta.features)//！！！是个坑==》features
                .join("path")
                .attr('d',geo)
                .attr('stroke','black')
                .on("click",function(d){
                    d3.select(this)
                    .attr(xx)
                    
                })

```

## D3 之外的 库   D3-Tip
!!!!需要导入
- D3-Tip
- 自动在‘合适’的位置显示对话框
- 不作为D3.js的本体，由community的爱好者们开发的用于辅助D3的库
- 初始化D3.Tip

```js
const tip=d3.tip()
.attr('class','d3-tip').html(function(d){ return d.properties.name} );
svg.call(tip);


xx.on('click',function(d){
tip.show(d);
})
```


### CSS
- 外部
- 内部
- 内联
内联样式 > 内部样式 > 外部样式

## litter tips
- 箭头函数，this没有定义
- 


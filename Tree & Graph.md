# 树 和 图
- 层级结构的可视化
  - 树、Tree、Hierarchy
    - d3.hierarchy
   
  - 直接的可视化方案
    - d3.tree
   
  - 更直观的可视化方案
    -  d3.partition & d3.arc for 'd' of <path>
- 网络结构的可视化
  - 网络结构：图、Graph、Network
  - D3.js : Force Simulation
 
## 层级数据
- 数据格式仍为Json
- 节点可以包含"属性"
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/51abb588-15ce-4eb0-b9cf-85b11b902ce0)
### D3.js的层级数据预处理
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/d5f3307b-fc21-4040-b7c4-68154d7f4b70)


```js

let root;
        let color;
        const fillFunction =function(d){
          //子节点都与第二层节点的颜色一致
          if(d.depth===0)
          return color(d.data.name)
          while(d.depth>1){
            d=d.parent;
          }
          return color(d.data.name)
        }
        const render =function(data){
          color=d.scaleOrdinal()//定义颜色
          domain(root.descendants().filter(d=>d.depth<=1)).map(d=>d.data.name)
          .range()

          //或者
          // color=d.scaleOrdinal(d3.schemeCategory10)//定义颜色
         

         // d3.linkHorizontal()//树之间的线
            g.selectAll("path")
            .data(root.links())//root.links()
            .join("path")
            .attr("fill","none")
            .attr("stroke-width",1.5)
            .attr("d",d3.linkHorizontal().x(d=>d.y).y(d=>d.x));
        
            //树间的圆圈      root.descendants()将root的所有子节点（广度优先）返回一个List
            g.selectAll('circle').data(root.descendants()).join('circle')
            .attr("cx",d=>d.y)
            .attr('cy',d=>d.x)
            .attr('fill',fillFunction)
            .attr('r',)

            g.selectAll('text').data(root.descendants()).join('text')
            .attr('font-size','1em')
            .attr('x',d=>d.y)
            .attr('y',d=>d.x)
            .text(d=>d.data.name)
            //dy 属性

        
        
        }
        d3.json('/xxx.json').then(data=>{
          root = d3.hierarchy(data);//数据处理
          root = d3.tree().size([innerHeight,innerWidth])(root)//多 x ,y 值
          render()
        })


tip:
            .attr("d",d3.linkHorizontal().x(d=>d.x).y(d=>d.y));
        }
        d3.json('/xxx.json').then(data=>{
          root = d3.hierarchy(data);//数据处理 height depth
          root = d3.tree().size([innerWidth,innerHeight])
效果就是竖着的，树
```

##### 冰锥图
```js
const render=function(data){
  const color = d3.scaleOrdinal(d3.schemeCategory10)
  const fill= d=>{
    while(d.depth>1)
    d=d.parent;
    return color(d.data.name)
  }

//添加矩形
  g.selectAll('.datarect').data(data.descendenats()).join('rect')
  .attr('class','datarect')
  .attr('fill',fill)
  .attr('x',d=>d.y0)
  .attr('y',d=>d.x0)
  .attr('height',d=>d.x1-d.x0)
  .attr("width",d=>d.y1-d.y0)

 g.selectAll('.datatext').data(data.descendenats()).join('text')
  .attr('class','datarect')
  .attr('text-anchor',"middle")
  .attr('x',d=>(d.y0+d.y1)/2)
  .attr('y',d=>(d.x0+d.x1)/2)

  .attr('height',d=>d.x1-d.x0)
  .attr("width",d=>d.y1-d.y0)
  .text(d=>d.data.name)
}

d3.json('/xx.json').then(data=>{
  root=d3.partition().size([height,width])(
    d3.hierarchy(data).sum(d=>d.popularity)
    .sort((a,b)=>b.popularity-a.popularity)
  )

  //dataDraw
  render(root)
})
```


![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/32e2e3f5-78b2-489d-aab3-2c90566044b4)

##### sunburst图
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/034d759c-4c95-4639-abd7-ba32ec4206ed)


```js
//sunburst
let root;
const arc = d3.arc()
.startAngle(d=>d.x0)
.endAngle(d=>d.x1)
.innerRadius(d=>d.y0)
.outerRadius(d=>d.y1)
// .padAngle(...)

const render=function(data){
  const color = d3.scaleOrdinal(d3.schemeCategory10)
  const fill= d=>{
    while(d.depth>1)
    d=d.parent;
    return color(d.data.name)
  }
//不要根节点
  g.selectAll('.datapath').data(data.descendenats().filter(d=>d.depth!==0)).join('path')
  .attr('class','datapath')
  .attr('d',arc)
  .attr('fill',fill)


 g.selectAll('.datatext').data(data.descendenats().filter(d=>d.depth!==0)).join('text')
  .attr('class','datarect')
  .attr('text-anchor',"middle")
  .attr('tranform',d=>{
    let x =(d.x0+d.x1)/2*180/Math.PI
    let y=(d.y0+d.y1)/2
    return `rotate(${x-90}) translate(${y},${0}) rotate(${x<180?0:180})`
  })
  .text(d=>d.data.name)
  //dy

}

d3.json('/xx.json').then(data=>{
  //size(周长，半径)
  root=d3.partition().size([2*Math.PI,height/1.6])(
    d3.hierarchy(data).sum(d=>d.popularity)
    .sort((a,b)=>b.popularity-a.popularity)
  )

  //dataDraw
  render(root)
})
```

## 一般图的可视化
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/0dc6aa5c-5a67-479e-9eb8-cc5a42698cd6)

- 力导图
- D3.js:Force
- let nodes=[{},{},{},{},{},{}\]
- let simulation = d3.foreSimulation(nodes)定义后会发生
- - 补全nodes中每个节点的数据结构
  - - 包括 index、x、y、vx、vy，后两者为速度
   
  - 开始模拟例子运动
  - - 粒子质量为1
    - 不断地通过内部timer触发‘tick'事件
   
  - 根据一些列的’力‘来计算每个例子的加速度、速度
  - 位置
 
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/6ce6ebf1-47da-4bb6-bfea-82ff8970c51e)
### Foece
- d3.forceManyBody
- - 粒子之间两两的作用力
  - strength为正互相吸引，为负则相互排斥
 
- d3.forceCenter
- - 指向某一个中心的力，会尽可能让粒子向中心靠近或重合
 
- d3.forceLink
- - 粒子之间两两的作用力
  - 让相互之间有链接的节点保持在某一个特定的距离
  - 是否有链接需要通过图的边集合给出
 
```js
simulation = d3.forcesimulation(nodes)
.force("manyBody",d3.forceManyBody().strength(-30))
.force("center",d3.forceCenter(width/2,height/2))
.force("link",d3.forceLink(links).strength(0.1).distance(100))
```
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/ae1404e2-0e18-4456-9f8c-b51a92600a74)


##### 力导图
```js
simulation = d3.forcesimulation(nodes)
.force("manyBody",d3.forceManyBody().strength(-30))
.force("center",d3.forceCenter(width/2,height/2))
.force("link",d3.forceLink(links).strength(0.1).distance(100))

let nodes,simulation,circles,lines,links;

const render_init=function(){
  //连线和园
  lines= svg.selectAll('line').data(links).join('line')
  .attr("stroke",'black')
  .attr("opacity",0.8)
  .attr("stroke-width",0.5)

  circles=svg.selectAll('circle').data(nodes).join('circle')
  .attr("r",5)
  .attr("fill",'blue')

}

const ticked =function(){
      lines.attr("x1",d=>d.source.x)
      .attr("y1",d=>d.source.y)
      .attr("x2",d=>d.target.x)
      .attr("y2",d=>d.target.x)

      circles
      .attr("cx",d=>d.y)
      .attr("cy",d=>d.y)

}

//读数据
d3.json('/xx.json').then(data=>{
  nodes=[]
  //数据初始化
  for(let i=0;i<data["#nodes"];i++){
    nodes.push({'index':i})
  }
  console.log(nodes);
  //图元初始化
  render_init();

  //力模拟
  simulation =d3.forcesimulation(nodes)
  .force("liname",d3.forceManyBody().strength(-30))//万有引力/斥力
  .force("center",d3.forceCenter(width/2,height/2))//画布的中间
  .force("link",d3.forceLink(links).strength(0.1).distance(100))
  .on('tick',ticked)//映射出来
})
```



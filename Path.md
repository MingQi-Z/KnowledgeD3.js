## Path
可以用来绘制多样的图形

path元素的形状是通过属性 d 来定义的，属性d的值是一个“命令+参数”的序列

### Paht的属性
- d
- fill :填充颜色
- stroke:描边颜色
- stroke-width：描边宽度
- transform：变换

#### d 属性
- M 0 0 画笔移动到指定的坐标位置（0，0）
- L x y 画直线到指定的坐标位置
- V y   画垂直线到指定的 Y 坐标位置
- H x   画水平线到指定的 X 坐标位置
- C x1 y1 x2 y2 ENDX ENDY 三次贝塞曲线
- S x2 y2 ENDX ENDY 平滑曲线
- Q X Y ENDX ENDY 二次贝塞曲线
- T ENDX ENDY　映射
- A RX RY XROTATION FLAG1 FLAG2 X Y 弧线
- Z 关闭路径
- 以上所有命令均允许小写字母。大写表示绝对定位，小写表示相对定位。


## Path 生成器
- d3.line(...).x(...).y(...)
  .curve(d3.curveCardinal.tension(0.5))//差值
-  - 用于折线图
- d3.geoPath(...).projection()
- - 用于地图
- d3.area()
- - 用于主题河流
 
- d3.arc(...).innerRadius(...).outerRadius(..)
- - 用于饼图
 
- d3.lineRadial().angle(...).radius(...)
- - 极坐标系的d3.line(...)
 
- D3.shapes:https://github.com/d3/d3-shape/tree/v1.3.7
### 折线图
![image](https://github.com/MingQi-Z/KnowledgeD3.js/assets/77725176/2129d3c2-6a0e-456a-b845-4e4c934a2936)


##### 函数
new Set()，集合   ===>   去重
sort(（a,b)=>{
return a.x-b.x
})
datum()  将data数组当作一个
transition().duration(20000)

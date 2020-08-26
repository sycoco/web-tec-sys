## 响应式布局常用方案对比（媒体查询，百分比，rem和vh/vm）
### 视口
1. 设置视口

   ```javascript
      <meta id="viewport" name="viewport" content="width=device-width; initial-scale=1.0; maximum-scale=1; user-scalable=no;">
   ```

其中width属性，在移动端布局时，在meta标签中我们会将width设置称为device-width，device-width一般是表示分辨率的宽，通过width=device-width的设置我们就将布局视口设置成了理想的视口


### 媒体查询
1. 简单来说就是给每一个不同尺寸的设备，各一套不同的样式来实现自适应效果，缺点就是样式太多，太繁杂，不建议使用
```javascript
  
@media screen and (max-width: 960px){
    body{
      background-color:#FF6699
    }
}

@media screen and (max-width: 768px){
    body{
      background-color:#00FF66;
    }
}

@media screen and (max-width: 550px){
    body{
      background-color:#6633FF;
    }
}

@media screen and (max-width: 320px){
    body{
      background-color:#FFFF00;
    }
}
```
### 百分比布局
1.就是根据浏览器的宽度或者高度发生变化时，内部组件按比例缩放，从而实现响应式效果。缺点是计算复杂，以及各个元素
使用百分比，相对父元素不是唯一的（margin、padding不管垂直还是水平方向都相对比父元素的宽度、border-radius则是相对于元素）
导致布局变得复杂。

### rem布局
1.rem单位，rem 是灵活可扩展的单位，只想对与根元素html的font-size,默认情况下，html元素的font-size为16px
```
1rem = 16px
```
2.通过rem来实现响应式布局
rem单位都是相对于根元素html的font-size来决定大小的,根元素的font-size相当于提供了一个基准，当页面的size发生变化时，只需要改变font-size的值，那么以rem为固定单位的元素的大小也会发生响应的变化。
因此，如果通过rem来实现响应式的布局，只需要根据视图容器的大小，动态的改变font-size即可。
```
function refreshRem() {
    var docEl = doc.documentElement;
    var width = docEl.getBoundingClientRect().width;
    var rem = width / 10;
    docEl.style.fontSize = rem + 'px';
    flexible.rem = win.rem = rem;
}
win.addEventListener('resize', refreshRem);
```
缺点：也就是说css样式和js代码有一定的耦合性。且必须将改变font-size的代码放在css样式之前。

### css3新的单位vw/vh











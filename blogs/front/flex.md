---
title: 响应式常用的几种方法
date: 2020-12-20
tags:
 - flex
categories: 
 - front
---
# 响应式常用的几种方法
## 课堂地址
[imooc地址](https://www.imooc.com/video/22669)

### 为什么要做这门课
- 页面设计在不同设备的显示情况
- 布局只用float+定位，不使用flex
- 不能很好的使用rem作为设计单位
- 掌握响应式布局，弹性等常见布局

#### 学习方法
- 充分利用开发工具
- 多做各种测试并观察浏览器渲染效果
- 先分析计算，在运行观察效果

#### 什么是媒体查询
- 概念:为不同尺寸的屏幕设定不同的css样式
- <span style="color:red">screen</span>指定屏幕尺寸
    - min-width,max-width与min-device-width,max-device-width是有差别的,前者指的是浏览器的可是宽度,后者指的是设备的屏幕宽度
- style标签:写在style标签中，有条件的执行某个内部样式表

#### flex弹性布局
- 概念:FlexiableBox即是弹性盒子，用来进行弹性布局，可以配合rem处理尺寸的适配问题

#### 为什么使用flex
- 使盒子模型更加灵活
- 更加符合响应式的设计理念

###### flex-direction
- 作用:子元素在父元素盒子中的排列方式
- 属性
    - row:默认值。按从左到右的顺序排列
    - row-reverse:与row相同，但是以相反的排列
    - column:灵活的项目将垂直显示，按从上到下的顺序排列
    - column:与column相同，但是以相反的顺序

###### flex-wrap
- 作用:子元素在父元素盒子中的是否换行
- 属性
    - nowrap:默认值，不换行，不换列。
    - wrap:换行或换列。
    - wrap-reverse:换行或换列，但是以相反的顺序

##### flex-flow
- 作用:flex-direction和flex-wrap属性的简写形式
- 语法:flex-flow: flex-direction || flex-wrap

##### justify-content
- 作用:用来在存在剩余空间时，设置为间距的方式
- 属性
    - flex-start:默认值，从左到右，挨着行的开头
    - flex-end:从右到左，挨着行的结尾
    - center:居中显示。
    - space-between:平均分布在改行上，两边不留间隔空间
    - space-around:平均分布在改行上，两边留有一半的间隔空间

##### align-items
- 作用:设置每个flex元素在交叉轴上的默认对齐方式(单行:以一行为整体)
- 属性:
    - flex-start:位于容器的开头
    - flex-end:位于容器的结尾
    - center:居中显示

##### align-content
- 作用:设置每个flex元素在交叉轴上的默认对齐方式
- 属性:
    - flex-start:位于容器的开头
    - flex-end:位于容器的结尾
    - center:位于容器的中心
    - space-between:之间留有空白
    - space-around:两端都留有空白

##### 其他属性(针对子元素的设置)
- flex-basis:设置弹性盒伸缩基准值。
- flex-grow:设置弹性盒子的扩展比率。
- flex-shrink:设置弹性盒子的缩小比率。
- flex:flex-grow、flex-shrink、flex-basis的缩写

### 常用布局
- rem的使用方法
    - 指相对于根元素的字体大小的单位
    - 与em的区别
        1. rem与根字体的关联，em是与父对象的关联

### 自适应布局
- 不用设备对应不同的html
- 局部自适应
- 不同的设备用不同的页面或者局部伸缩
- 判断设备的类型或控制局部的变化

### 响应式布局
- 布局特点
    - 确保一个页面在所有终端上，都能显示出令人满意的效果
- 一套方案，处处运行
- 使用%或rem作为单位，此处采用%为单位

### rem弹性布局
- 布局特点
    - 为了保证在各种屏幕上的不失真，就要根据实际屏幕宽度做等比例换算
- 一句话
    - 一套方案，使用不同尺寸、分辨率的视口，都能呈现出较好的东西
- 设计思路
    - 使用%或rem作为单位，此处采用ren单位
```javascript
//使用当前函数来计算页面大小
//使用rem为单位来代替px进行布局
    <script>
        var c = () => {
            let w = document.documentElement.clientWidth;       //获取设备的宽度
            let n = (20*(w/320)>40?40+"px":(20*(w/320)) + "px");    //20表示随意的字体比列，40表示任意设备最大的字体不超过40
            document.documentElement.style.fontSize = n;
        }

        window.addEventListener("load",c);
        window.addEventListener("resize",c);
    </script>
```
[代码地址](https://github.com/hackerabbit/Responsive.git)
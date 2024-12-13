
## **前情**


Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为 Flex 布局，如果说目前我开发中离不开的布局方式那就非Flex莫属了，而且小程序就是推荐使用Flex布局的，对 Grid布局的支持不太理想。


在一次次使用flex布局的时候遇到了一些小困扰，而解决这些小困扰的过程中发现了一些小技巧，特记录并分享出来。


## 技巧内容


### 技巧 1：flex\-direction为column的子元素自适应内容宽



```
html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <style>
	    .test {
			  width: 100%;
			  display: flex;
			  flex-direction: column;
			}
			.test-item {
			  height: 100px;
			  display: flex;
			  flex-direction: row;
			  justify-content: center;
			  align-items: center;
			  background-color: red;
			  color: white;
			}
			.test-item:nth-of-type(3){
			  align-self: flex-start;
			}
    style>
  head>
  <body>
      <div class="test">
        <div class="test-item">010101div>
        <div class="test-item">020202div>
        <div class="test-item">030303div>
      div>
  body>
html>

```

当设置为flex\-direction: column后，项目元素align\-self样式值默认为stretch，导致项目元素会充满整行，如果你想做到项目元素自适应内容宽你设置为align\-self:baseline或者flex\-start即可


上述示例可以实现如下图布局效果：


![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212731316-1501414196.png)


体验链接：[CSS Playground](https://github.com)


### 技巧 2：利用margin:auto实现一些特殊布局


对于如下需求你第一想到的flex布局方式是怎么实现：


![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212834205-1909721451.png)


按正常的实现思路是左边一个div包住左边内容，右边再一个div，再使用justify\-content:between可以实现或者让左边的div为 flex:1，那有什么方式可以让结构打平一层，左边的包裹div免去了，那就是margin:auto，利用好margin:auto可以实现一些特殊布局，演示代码如下：



```
html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
	  <style>
	  .test,.test0,.test1 {
			  width: 100%;
			  display: flex;
			  flex-direction: row;
			  background-color: black;
			}
			.test-item,.test-item0,.test-item1 {
			  width: 100px;
			  height: 100px;
			  display: flex;
			  justify-content: center;
			  align-items: center;
			  color: white;
			  background-color: green;
			}
			.test-item:nth-last-of-type(1){
			  margin-left: auto;
			}
			.test-item0:nth-last-of-type(2){
			  margin-left: auto;
			}
			.test-item1:nth-of-type(2){
			  margin-left: auto;
			}
			.test-item1:nth-of-type(3){
			  margin-right: auto;
			}
	  style>
  head>
  <body>
    <div class="test">
      <div class="test-item">1div>
      <div class="test-item">2div>
      <div class="test-item">3div>
      <div class="test-item">4div>
    div>
    <div class="test0">
      <div class="test-item0">1div>
      <div class="test-item0">2div>
      <div class="test-item0">3div>
      <div class="test-item0">4div>
    div>
    <div class="test1">
      <div class="test-item1">1div>
      <div class="test-item1">2div>
      <div class="test-item1">3div>
      <div class="test-item1">4div>
    div>
  body>
html>

```

上述示例可以实现如下图布局效果：


![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212819767-643916944.png)


体验链接：[CSS Playground](https://github.com)


### 技巧 3：利用align\-self实现**交叉轴(Cross Axis)上单个元素位置控制**



```
html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
	    .test {
			  display: flex;
			  flex-direction: column;
			  align-items: center;
			}
			.test-item {
			  width: 100px;
			  height: 100px;
			  display: flex;
			  flex-direction: row;
			  justify-content: center;
			  align-items: center;
			  color: white;
			  background-color: red;
			}
			.test-item:nth-of-type(1){
			  align-self: flex-start;
			}
			.test-item:nth-of-type(3){
			  align-self: flex-end;
			}
    style>
  head>
  <body>
    
    <div class="test">
      <div class="test-item">1div>
      <div class="test-item">2div>
      <div class="test-item">3div>
    div>

  body>
html>


```

通过align\-items可以整体控制交项目元素在叉轴上的对齐方式，但如果想单个控制它的对齐方式，那就用好align\-self吧，上述示例可以实现如下图布局效果：


![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212848935-1166779175.png)


体验链接：[CSS Playground](https://github.com):[楚门加速器](https://chuanggeye.com)


### 技巧 4：使用gap设置容器内项目之间的间距



```
html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
	  <style>
		  .wrap {
			  display: flex;
			  flex-direction: row;
			}
			.test {
			  width: 320px;
			  display: flex;
			  flex-direction: row;
			  align-items: center;
			  justify-content: space-between;
			  flex-wrap: wrap;
			  margin-right: 20px;
			}
			.test-item {
			  width: 100px;
			  height: 100px;
			  margin-bottom: 10px;
			  flex: none;
			  display: flex;
			  flex-direction: row;
			  justify-content: center;
			  align-items: center;
			  color: white;
			  background-color: red;
			}
			.test0 {
			  width: 320px;
			  display: flex;
			  flex-direction: row;
			  align-items: center;
			  flex-wrap: wrap;
			  margin-right: 20px;
			  gap: 10px 10px;
			}
			.test-item0 {
			  width: 100px;
			  height: 100px;
			  flex: none;
			  display: flex;
			  flex-direction: row;
			  justify-content: center;
			  align-items: center;
			  color: white;
			  background-color: red;
			}
	  style>
  head>
  <body>
    <div class="wrap">
      <div class="test">
        <div class="test-item">01div>
        <div class="test-item">02div>
        <div class="test-item">03div>
        <div class="test-item">04div>
        <div class="test-item">05div>
        <div class="test-item">06div>
        <div class="test-item">07div>
        <div class="test-item">08div>
      div>

      <div class="test0">
        <div class="test-item0">11div>
        <div class="test-item0">12div>
        <div class="test-item0">13div>
        <div class="test-item0">14div>
        <div class="test-item0">15div>
        <div class="test-item0">16div>
        <div class="test-item0">17div>
        <div class="test-item0">18div>
      div>
    div>
  body>
html>


```

Flex布局如果不依赖gap想实现如下右图的布局是比较麻烦的，通过justify\-content: space\-between可以做到平分余下空间让元素间有间距，但是如果遇到未行元素不够的时候就会出现如下左图的问题，解决办法是手动生成一个空的元素让它补齐一行内容也是可以做到的；另一种实现方式是通过margin来实现元素间距，再通过:nth\-child()方式来去除每行最边缘元素的margin。上述二种方式都相对比较麻烦，如果你使用gap就可以轻松实现右图效果


![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212900649-343747600.png)


体验地址：[CSS Playground](https://github.com)


### 技巧 5：比较常用的几个缩写


flex: 1/flex: 0%; 等效于flex:1 1 0%; 子元素平分父元素空间，各子元素尺寸一样


![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212912596-195528678.png)


flex: none; 等效于flex:0 0 auto; 元素保持自身原始大小不变
![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212922654-1545577358.png)


flex：auto; 等效于flex:1 1 auto; 元素尺寸可以弹性增大，也可以弹性变小，具有十足的弹性，项目会根据自身大小和剩余空间进行伸缩
![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212932569-58188974.png)


注:flex:1和flex:auto区别:


* flex\-basis属性定义了项目在分配多余空间之前，占据的主轴空间（main size）
* flex:1相当于flex: 1 1 0%，表示项目的基准大小为0%，不考虑项目本身的大小，只根据剩余空间进行伸缩
* flex:auto相当于flex: 1 1 auto，表示项目的基准大小为auto，即项目本身的大小，同时也会根据剩余空间进行伸缩
* 如果容器有足够的空间，flex:1和flex:auto都会平分剩余空间，但是flex:auto会保持项目本身的最小宽度，而flex:1不会
* 如果容器没有足够的空间，flex:1会优先压缩内容，使得所有项目都能等分空间，而flex:auto会优先保持内容的完整性，挤压其他项目的空间


在线测试地址：[JS Bin \- Collaborative JavaScript Debugging](https://github.com)


### 技巧 6：浏览器开发者工具辅助使用


对于新手刚刚学习使用flex布局，经常容易忘记一些属性，其实可以通过浏览器开发者工具辅助来学习flex布局，vs code也有对应的插件可以辅助
![](https://img2024.cnblogs.com/blog/685637/202412/685637-20241212212945391-544420628.gif)


### 期望


上述只是个人在开发中发现的一些Flex布局小技巧，如果你有好的技巧欢迎也分享出来，共同学习进步。期待你的留言👀。



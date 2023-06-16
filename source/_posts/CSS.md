---
title: CSS
date: 2023-06-08 13:43:46
tags:
---

# CSS
1. CSS表示层叠样式表（Cascading Style Sheet，简称：CSS，又称为又称串样式列表、级联样式表、串接样式表、阶层式样式表）是为网页添加样式的代码。
2. 并非编程语言，是样式表语言或计算机语言
3. CSS的出现是为了美化HTML的，并且让**结构（HTML）与样式（CSS）分离**；
	美化方式一：为HTML添加各种各样的样式，比如颜色、字体、大小、下划线等等；
	美化方式二：对HTML进行布局，按照某种结构显示（CSS进行布局 – 浮动、flex、grid）；
4. 	![css属性](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230608134759699.png)CSS应用到元素上

1. 内联样式
	存在于HTML元素中的style属性中，**样式之间采用分号分割**
2. 内部样式表、文档样式表、内嵌样式表
	放在<head>元素中的<style>元素中
	在Vue的开发过程中，每个组件也会有一个style元素，和内部样式表非常的相似（原理并不相同）
3. 外部样式表
	独立文件，通过<link>元素引入进来
4. **@import**
	@import url(css文件地址);
	在<style>元素中导入其他CSS文件

## 文本
1. **text-decoration**
    设置文字的装饰线
    none
    underline
    overline
    line-through

2. **text-transform**
    设置文字大小写转换
    capitalize：(使…首字母大写, 资本化的意思)将每个单词的首字符变为大写
    uppercase：(大写字母)将每个单词的所有字符变为大写
    lowercase：(小写字母)将每个单词的所有字符变为小写
   none：没有任何影响

3. **text-indent**
	用于设置第一行缩进
	2em
	
4. **text-align**
	设置文本对其颜色
	MDN：定义行内内容（例如文字）如何相对它的块父元素对齐;
	常用值：left：左对齐；right：右对齐；center：正中间显示；justify：两端对齐

5. letter-spacing、word-spacing
	letter-spacing、word-spacing分别用于设置字母、单词之间的间距
	默认是0，可以设置为负数
	
## 字体
1. **font-size**
    设置文字的大小
    100px 、 50%

2. **font-family**
    设置文字字体名称，可设置多个
    可通过**@font-face** 指定的可以直接下载的字体

3. **font-weight**
    设置文字的粗细(重量)
    normal：400；bold：700

4. font-style
    normal、italic、oblique

5. **line-height**
    设置文本行高
    行高：两行文字基线之间的间距
    基线（baseline）：与小写字母x最底部对齐的线

  ![文本行高](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230608171128970.png)
	 应用实例：假设div中只有一行文字，如何让这行文字在div内部垂直居中
		让line-height等同于height

## 选择器
1. 通用选择器
	所有元素都会被选中
	用来给所有素性设置通用属性

2. 元素选择器
	元素的名称

3. 类选择器
	**.类名**

4. id选择器
	**#id**
	**唯一的，不能重复的**
	
5. 属性选择器
	拥有某一个属性[att]
	属性等于某个值[att=val]
	
6. 后代选择器

7. 伪元素选择器 **::before  ::after**
	用来给一个元素的内容前或后插入其他内容的东西	

## 盒子模型

## CSS继承-层叠-元素类型

## 定位 | position
### 静态定位 | static
1. 元素俺找 **normal flow** 布局
2. left 、 right、 top、 bottom没有任何作用


### 相对定位 | relative
1. 还在标准流布局
2. left 、 right、 top、 bottom被激活，相对自己的位置
3. 在不影响其他元素位置的前提下，对当前元素位置进行微调

### 固定定位 | fixed
1. 脱标，定位参照对象是视口(可视区域)
2. 主要设置一些不随画布移动的图标

### 绝对定位 | absolute
1. 脱标；参照对象是**最邻近的<u>定位祖先元素</u>，如果无则为视口**
2. **子绝父相**是因为相对定位没有脱离标准流，但是也能是最邻近的定位祖先元素

### fixed | absolute
1. **可以随意设置宽高**，不论是否是行内非替换元素
2. 宽高默认由内容决定

### 粘性定位 | sticky
1. 考虑兼容性问题，较新，不兼容IE
2. 相当于relativ和fixed的结合，当滚动到一定位置时，停留在视口位置
3. 相对于最近的滚动祖先包含视口的	

### z-index 
1. 仅对定位元素有效
2. 同一层级的比较
2. z-index越大，层叠越在上面；相等，写在后面的元素在上面

### 总结
![position定位总结](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230609110822255.png)

## 其他
### auto
1. 交给浏览器来处理，具体交给浏览器处理
2. 绝对定位中，top……设置为auto大概率是不会平分居中显示的

## 浮动 | float 
1. **float**: none  |  left  | right 
2. 脱离标准流，让元素靠左靠右(包含块)
3. **层叠关系：普通元素 < float < 定位元素**
4. 浮动元素之间不能层叠
5. 浮动元素不能和行内级内容层叠，否则内容将会被推出
6. **正在退出历史舞台，兼容性好，图文混排**

### 清除浮动
1. 还没看，后面再看一次


## 其他
1. 在书写代码中的换行符被浏览器解析会产生间隙
2. **将多个行内级元素中间的空格去除的方法**
	* 删除换行符
	* 将父元素的font-size设置为0 ，但是子元素需要设置回来
	* 浮动可以去除空袭
	* flex布局

## flex layout | 一维
### 理解
1. flexbox：弹性盒子
2. display：flex
3. 开启flex布局的元素叫**flex container**；flex container里面的直接子元素叫做**flex item**
4. 主轴、交叉轴(可变)

   ![flex布局模型](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230609215913006.png)
   
### container
1. **flex-direction**: 决定主轴方向
	* row-reverse | row | column | column-reverse
	
2. **flex-wrap**： flex-container单行还是多行显示
	* 元素最终展示的宽度和width有关系，但没有绝对的关系
	* flex-wrap: nowrap 单行显示
	* flex-wrap: wrap 多行显示
	* flex-wrap: wrap-reserve 多行显示，与wrap相比cross-start、cross-end相反
	
3. **flex-flow: flex-direction flex-wrap**

4. **justify-content**
	* 主轴对齐方式
	![对齐方式](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230610094741669.png)
	
5. **align-item**
	* 交叉轴对齐方式
	* 在flex布局中，normal和scratch的样式一样拉伸(height：auto)
	* 在设置具体高度后，不会进行拉伸
	![flex交叉轴对齐方式](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230610100943832.png)

6. **align-content** 少
	* 在交叉轴中多行中，类似主轴中的justify-content
	![align-content](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230610102839625.png)

### flex-item
1. order： 设置顺序，值越小越往后
2. flex-shlef:
3. **flex-grow**: 决定flex items如何扩展、拉伸，默认值:0
4. flex-shrink：决定flex items如何缩小，默认值：1
5. flex-basis
6. flex：缩写属性

### 其他

![布局问题](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230610105917292.png)

增加（列数-2）个span，虽然是无用元素，但是占据位置，没有给高度默认不显示高度可以达到相应效果

## 形变
### transform
1. 对行内级非替换元素无效
### transition
### animation
### vertical-align




## grid layout | 二维
### 理解
1. 兼容性不好

## 形变



## 元素居中方案

### absolute | fixed

1. 子绝父相，left、right、bottom、top都设置为0，margin设置为aotu，元素由宽高_143
2. **不存在兼容性问题**
   ![绝对定位元素居中](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230609113500652.png)
3. ![水平居中方案](C:\Users\86159\AppData\Roaming\Typora\typora-user-images\image-20230612113931709.png)

# 适配

1. 为什么需要适配

   各个移动端设备、屏幕尺寸、分辨率大小不一致

   让拥有不同屏幕大小的终端设备拥有一致的UI界面

2. 1px问题

3. 高清屏图片显式模糊问题

## 基础概念

1. **屏幕尺寸**

   屏幕对角线的长度，单位英寸

   1英寸 = 2.54厘米

2. **物理像素(设备像素)**

   设备屏幕上真实存在的像素点

   是屏幕设备像的最小单位

   每个物理像素由3个颜色像素构成

   每个物理像素可以表示2^24中颜色

3. **屏幕密度(PPI)**

   屏幕密度是指一个设备表面上存在的像素数量，他通常以每英寸多少像素来计算

   ![PPI计算](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230615134031238.png)

   ![Iphone6PPi](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230615134106819.png)

4. 物理分辨率

   物理分辨率是指纵横向上的物理像素点

   iphone6 屏幕分辨率为 **750 * 1334**

   分辨率小颗粒感明显

5. css像素

   ![](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230615134528402.png)

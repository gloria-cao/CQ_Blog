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
4. 	<img src="https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230608134759699.png" alt="CSS样式编写规则" style="zoom: 33%;" />

## CSS应用到元素上
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
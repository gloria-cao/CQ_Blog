---
title: Algorithm
date: 2023-06-15 21:26:49
tags:
---

# diff算法
1. 目的是找出差异，使最小化更新视图；本质上是比较两个JS对象的差异



# 定制化输出数组
``` javascript
// 随机生成一个长度为10的整数类型数组，
// 例如 [2， 10， 3， 35， 5， 11， 10， 11， 20]，
// 将其排列成一个新数组，要求新数组形式如下
// [[2, 3, 5], [10, 11], [20], [35]]

// 解题过程
/**
* 1. 随机生成0-99的数据
* 2. 数组去重
* 3. 排序
* 4. 规律存储 0-9 10-19
*/

// 随机生成一个0-1的数，这个数 * max - min + 1 可以获取min的值，再加上min的值就能够获取最大的值
    function getRandomNumber(min1, max1) {
      // 可能存在小数的情况，小的向上取整，大的向下取整
      let min = Math.ceil(min1)
      let max = Math.floor(max1)
      return Math.floor(Math.random() * (max - min + 1) + min)
    };

    // 利用Set数据只能存储一次的特性，进行数组去重
    let initArr = Array.from({ length: 10 }, () => { return getRandomNumber(0, 99) });
    initArr = [... new Set(initArr)];
    initArr.sort((a, b) => a - b);

    const map = {}
    initArr.forEach(item => {
      let key = Math.floor(item / 10)
      if (!map[key]) {
        map[key] = []
      }
      map[key].push(item)
    });

    const result = []
    for (const key in map) {
      result.push(map[key])
    }
    console.log(result)

```



# 树状结构转换为平铺属性结构，你会几种写法？
``` javascript
//	方法一：递归
//	每次处理一层结构，通过判断属性的值是否是对象来确定递归是否结束
//	- 如果是对象，则表示递归没有结束，递归调用
//	- 如果不是对象，表示递归的最后一层，确定属性值



//	方法二：while循环-队列
//	使用Object.entries()方法，处理原始对象
//	使用队列存储每一层的值，知道队列中的值处理完毕

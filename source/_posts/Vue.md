---
title: Vue
date: 2023-06-16 09:05:53
tags:

---

# watch

1. 



# 跨域

1. 协议、域名、端口号相同才算在同一个域
2. 只发生在浏览器的请求，不会发生在浏览器请求服务器

## 解决

1. 在响应头添加允许跨域字段

   Access-Control-Allow-Origin 

2. JSONP只支持get请求，不支持post请求

3. 反向代理

   在浏览器与服务器通信之间增加一个反向代理（与浏览器在同一个域中），这样一来就能解决跨域问题



# SSR | 服务端渲染	



# JWT 

1. **JSON Web Token**，通过数字签名的方式，以JSON对象为载体，在不同的服务中断之间安全的传输信息。

2. JWT最常见的应用场景时 **授权认证**，一旦用户登录，后续每个请求都会包含JWT，系统在每次处理用户请求之前，都要先进行JWT安全校验，通过之后在处理。

3. **三部分组成，用.拼接** 

   header （算法 + 加密方式）

   payload （载荷，存放有效信息的地方），加密

   Signature （签名），对上诉两部分使用.拼接再次进行加密操作



# keep-alive

1. 不设置keep-alive的话组件在进行切换的过程中会不断的进行创建和销毁。
2. keep-alive可以实现保存组件的状态(譬如组件在切换之前是黄色，当用户进行页面切换时，再次回到页面可以保留黄色状态)
3. 内置组件，包裹路由跳转，保留组件状态，防止重复渲染DOM


# nextTick
1. this.$nextTick() 会在dom渲染完毕后执行该函数，就可以获取到dom渲染完毕之后的数值
2. Vue进行异步渲染是批量的

# SPA
1. 单页面应用，切换快，用户体验好
2. 首屏加载慢，毕竟首次加载会将资源统一加载
3. 不利于搜索引擎优化


# 双向绑定原理
1. 利用Object.defineProperty(,,{})进行数据劫持，get、set数据监听
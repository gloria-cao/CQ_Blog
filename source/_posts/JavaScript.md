---
title: JavaScript
date: 2023-06-13 13:23:47
tags:

---

# this
1. 在非严格模式下指向一个对象
2. 只跟谁调用她有关，只有在运行时才知道绑定，**只看是谁调用的他，还有优先级**
3. **严格模式下的，独立函数的调用指向的是undefined**  use strict
4. (person.sayName)()  === person.sayName() => 隐式绑定
5. (b = person.sayName)()  === sayName() => 间接函数引用
## 默认绑定
1. 独立函数的调用，this指向window
2. 不论形式怎么改变，只要是在调用时是独立函数就是指向window
3. 像null、undefined这些数据没有对应包装类型是默认绑定到window上
## 隐式绑定
1. 通过某个对象发起的调用

   ![隐士绑定](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613135831171.png)
## 显式绑定
1. foo().call写法是错误的，会限制性foo函数，应该是foo.call()先拿到foo这个函数再执行call方法

2. foo.call(123)会创建原始包装类型，然后绑定到他的包装类对象里

3. **call()**
	* 第一个参数绑定this，后面以参数列表的形式传递额外参数
	
4. **apply()**
	* 第一个参数绑定this，后面以数组形式传递额外参数
	
5. **bind()**
	* 只能在bind的时候绑定参数和this，返回一个新的函数
	
	  ![image-20230613141523079](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613141523079.png)
## new绑定
1. 函数可以作为一个构造函数来使用，也就是一个类可以通过new来进行条用
2. new操作
	创建新的空对象，将this指向这个空对象；执行函数体代码；没有显示返回非空对象时，默认返回这个对象
3. new绑定绑定的式空对象
	
## 内置函数的调用绑定
1. 定时器，按钮的点击等this绑定由浏览器完成

## 优先级
1. ** new绑定 > bind > call > 隐式绑定 > 默认绑定**
2. new不能和call、apply一起使用
3. **new优先级高于bind**
4. bind的优先级高于apply

## 间接函数使用

## 箭头函数
1. 默认不绑定this，也不绑定arguments，往上层作用域里面寻找

2. 简写中一行代码不能带rerurn关键字，默认值返回是一个对象必须加()，不然js引擎不知道如何解析

3. 有自己的作用域，代码块（函数、全局）才有作用域，对象没有作用域，放键值对
4. 箭头函数找不到this往上层作用域找，正常的考虑独立函数调用

4. **this应用场景**

   ![业务逻辑，不绑定this的好处](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613200346754.png)
## 问题
1. 这几种绑定之间的区别？
   1. ![箭头函数求所有偶数的和](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613194753797.png)

# 浏览器的运行原理
## 网页的解析过程
1. 浏览器输入域名解析过程
	* 输入域名，域名经过DNS解析找到对应IP地址，通过IP找到对应的服务器，请求页面，再将html渲染到网页上
2. ![浏览器解析网页过程](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613205218444.png)

## 浏览器内核
1. 浏览器的排版引擎、排版引擎、浏览器引擎、页面渲染引擎、样板引擎

2. ![浏览器内核](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613224948273.png)

3. 页面引擎如何渲染页面

   ![渲染引擎解析界面](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613205551855.png)

   ![更详细](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613205725947.png)

   link元素不会阻塞DOM Tress的构建过程，但会阻塞Render Tree的构建构成（因为他构建时需要CSSOM Tree）；Render Tree和DOM Tree不是一一对应的关系（设置display: none）

   **布局和绘制**
   布局是确定渲染树中所有节点的宽度、高度和位置信息

## 回流和重绘
### 回流 | reflow | 重排
1. 修改元素需要重新计算DOM节点大小、位置修改重新计算，布局页面，就叫回流(在页面删除某个dom节点)
	* 字体大小、窗口尺寸、DOM结构发生改变、boer-width
2. 非常消耗性能

### 重绘 | repaint
1. 第一次内容渲染叫做绘制，**之后重新渲染叫重绘**
2. 页面颜色的修改，不改变DOM结构会引起重绘
3. 回流一定会引起重绘，但是重绘不一定会回流

### 避免
1. 样式尽量一次性修改
2. 避免频繁操作DOM
3. 对某些元素使用position的absolute和fixed(会引起，但是开销小，因为脱标元素重新布局不会影响别的dom节点)
4. 减少使用getComputedStyle()

## 特殊解析 | composite合成
1. 在标准流下是同一个图层
2. fixed会生成新的图层
3. absolute不会生成新的图层
4. transform在执行动画时，是在新的图层上进行的所以性能更高
4. 不同图层再进行回流时减少性能损耗，在GPU上进行渲染
5. 分层确实能够提高性能，但本身是以内存管理为代价的，因此**不应该作为web性能优化策略的一部分过度使用**
6. **做动画尽量使用transform 和opacity进行动画性能会更高，因为不在同一个图层里面**

## script元素和页面解析的关系
1. 遇到css下载代码浏览器不会停止，遇到JavaScript代码会停止构建DOM Tree，下载JavaScript代码，并执行JavaScript脚本，等到脚本结束后才会继续解析HTML文件构建DOM Tree
2. 原因： 因为JavaScript的作用之一时操作DOM，并且可以修改DOM，如果等到DOM树构建完成并且渲染再执行JavaScript，**会造成严重的回流和重绘，影响页面性能**；所以在遇到script元素时，优先下载和执行JavaScript代码，在继续构建DOM树。
3. 在目前开发模式下(Vue)，脚本往往比HTML页面更重，处理时间需要更长；所以会造成页面的解析阻塞，在脚本下载和执行完成前，用户界面什么都看不到。
4. 为解决 **3**的问题，script元素给我们提供了defer和async两个属性(attribute)
5. defer不会阻塞DOM Tree的构建过程，继续解析HTML，构建DOM Tree ； **如果脚本提前下载好了，他会等到DOM Tree构建完成，在DOMContentLoaded(构建DOM完成后会回调，在这之前操作DOM，不会引起严重的回流)事件之前先执行defer中的代码，多个脚本执行时defer可以保证正确的执行顺序，从某种程度来说defer可以提高页面的性能，并推荐放到head元素当中**
6. **defer仅仅适用于外部脚本，对内部脚本无意义**
7. **async**也能够让脚本不阻塞页面，不保证顺序因为他独立下载，独立运行，不受DOM影响，下载完就执行，不能随意执行DOM(执行时机不确定)

# JavaScript运行原理
## V8引擎
1. TypeScript能提高V8引擎性能，因为限制参数类型，进行优化机器码操作，不需要重新弄机器码 541
	
	![V8引擎执行原理](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230613225859648.png)
	
2. 版本说明

## 执行上下文栈
1. GO全局对象，在浏览器中即window指向自己
2. 在GO中，遇到函数对象，会声明函数对象，所以函数能被提前调用，函数是被提前声明的，可以在函数声明前调用这个函数(JS引擎优化)
3. 在创建执行上下文之前会先创建VO也就是GO(全局执行上下文情况下)，一些变量函数会提前声明GO里面，但不会赋值，只有等到代码执行该行时才会有值
4. 每个执行上下文都需要关联一个VO对象，
5. **GO**所以一开始VO等于GO
6. **AO**
	* 当进入函数执行上下文(即**函数执行时**)，会创建一个AO对象
	* 这个AO对象会使用arguments作为初始化，并且初始值是传如的参数
	* 这个AO对象会作为执行上下文的VO来存放变量的初始化
	*  **每次调用函数都会执行新的执行上下文，原来的是否存在内存是由垃圾回收器是否回收决定的 **
7. 赋值操作是在栈中完成，堆里面只是加了属性，本身不矛盾

## 作用域和作用域链 | scope scope chain
1. 作用域链是一个对象列表，用于变量标识符的求值；
2. 当进入一个执行上下文时，这个作用域链被创建，并且根据代码类型，添加一系列的对象
3. **只跟定义位置有关，跟调用位置无关与this相反**
4. **return**后面的代码会显式，因为他解析的时候是定义的，并没有进行代码的执行**先解析，再执行**
5. 忘记了写var是错误的，但是不管什么位置写 **message = “hello”**，这个message都是加在全局里面的 **var a = b = 100**，此时a是局部的，而b会放到全局下面

## 内存管理
1. 手动管理内存，自己进行释放，指向null
### 自动管理内存
1. JS引擎会帮我们管理内存

2. 垃圾回收(GC Garbage Collection)，最早提出Lisp
	* 引用计数： 当引用计数为0的时候，内存就会被释放
	
	* 标记清楚：根对象（window、GO）可达性
	
	* 标记整理，搬运连续内存空间，减少碎片化内存
	
	* 分代收集
	
	  ![分代收集内存表现](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230614102807453.png)
	  
	* 增量收集
	* 闲时收集

## 闭包
1. 函数及其关联环境组成的就是闭包（为什么能访问到呢？本质上是通过作用域链来实现的），如果没有闭包，函数再不传递参数时，是不能访问到外层作用域的数据的，所以在JavaScript中只要创建函数就会形成闭包，因为它本身会通过作用域链连接顶层作用域
2. 内存泄漏：就垃圾回收装置可达性，一直用不上，占用内存
3. ![闭包基础概念](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230616091008638.png)

## arguments
1. 对应于传递给函数的参数的类数组对象 **本身不是数组类型，而是一个对象类型，拥有一些数组的特性如length、index等，没有数组的一些方法如filter、map等**
2. 箭头函数不绑定this，会往上层作用域里面寻找
3. 函数的剩余参数rest(rest只包含没有对应形参的实参，arguments包含了传递给函数的所有实参)，**rest是一个数组**，ES6提出希望代替arguments，必须放在最后一位，在函数传递过程中写**...**

## 纯函数
1. 确定的输入产生确定的输出，在函数执行过程中，不能产生副作用
2. **副作用：** bug的温床，除了函数返回值外，还对调用函数产生了附加的影响，比如**修改了全局变量、修改参数或者改变外部的存储**
3. **slice：(纯函数)**slice截取数组时不会对原数组进行任何操作，而是生成一个新的数组；
4. **splice：**splice截取数组，会返回一个新的数组，也会对原数组进行修改。
5. **纯函数优势：**
	* 安心编写安心使用，只需要单纯实现业务逻辑，不需要关心传入的内容是如何让获得的或者依赖其他**外部变量**是否发生了修改；
	* 使用时，确定你的输入内容不会被任意篡改。并且自己确定的输入一定会有确定的输出。

## 柯里化函数
1. 把接收多个参数，变成接收一个单一的参数即将**f(a,b,c)  =>  f(a)(b)(c)**，为什么可以这样，我理解是在作用域链的作用下，前一个传递的值已经绑定到了作用域中，通过闭包概念可以进行获取并操作
2. **优势：**
  * 函数参数的服用
  * ```javascript
    function makerAddr(count) {
        return function(num) {
            return num + count
        }
    }
    
    var add5 = makeAddr(5)
    add5(10)
    add5(100)
    
    var add10 = makeAddr(10)
    add10(10)
    add10(100)
	* 职责单一，让函数代码尽量职责单一

3. **劣势：**
	* 容易造成内存泄漏，保留原有的AO对象，原理还是利用了闭包
4. **自动化柯里化函数**

## 组合函数 | Compose Function
1. 将两个函数组合起来，自动依次调用。
2. 边界判断

## 严格模式 | Strict Mode
1. 严格模式通过抛出错误来消除原有的**静默错误（不报错也没有任何效果）（message = “hello” // 本身是错误语法，但是JavaScript语法松散，浏览器并不会报错，使用严格模式就可以）**

   ![静默错误](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230614141745710.png)

2. JS引擎在执行代码时可以进行更多的优化

3. 严格模式下禁用了在ECMAScript未来版本中可能会定义的一些语法

4. **支持粒度化迁移**，即可以在某和js文件或者函数中执行，在开头写**use strict**

5. class、module默认情况下时开启严格模式的

6. 严格模式下，八进制不能以0开头要以0o开头，不允许with，eval函数为上层创建变量；this不会转成对象类型

## 对象增强

### Object.defineProperty()

1. 默认情况下属性都没有特殊的配置，对属性进行特殊控制需要用到属性描述符(属性是否能进行删除之类的操作)
2. 该方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回该对象	
3. 数据属性描述符、存储属性描述符（可否删除或修改特性默认值true，通过属性描述符来创建默认时false；可否枚举（for in ；Object.keys()）；告诉JS引擎返回这个value而不是其他的value；可否写入）
	* ![属性描述符类型](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230614143753128.png)
	
	set方法监听函数的调用，get方法监听设置的过程，尽量不在里面使用，可能会形成回调地狱
### Object.defineProperties 
1. ![给多个属性添加属性描述符](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230614144900821.png)

# 原型
## 对象原型
1. 任何对象都是有原型的**obj.__proto__  | Object.getPrototypeOf(obj)**
2. 优先查找自己作用域中，没有再在原型上查找

## 函数原型
1. 对象原型的作用是在查找某个属性查找不到时在原型上查找
2. 将函数看成是一个普通的对象时，它具备__proto__（隐式原型）
2. 将函数看成是一个函数时它具备prototype属性(显示原型)，因为是函数才具备这个一个属性
3. 所有的函数都有prototype属性，不是__proto__，**对象没有prototype属性**
4. **new：创建空的对象，将Foo的prototype(显式原型)赋值给空对象的__proto__隐式原型 **
5. 属性不要放在原型上，方法可以放在原型上，这样不会创建很多分
6. prototype对象上存在constructor函数，constructor指向的是Person函数对象，形成一个闭环

## 重写原型对象
1. 可以让该Person原型对象重新赋值为一个对象，但是对象里面没有constructor属性(指向该Person对象，这样即可：constructor: Person，功能一致，但效果不一致),但是在原来的原型对象constructor是不可枚举的，可以通过前面学习过的Object.defineProprety属性描述符来进行修改`Object.definedProperty(Person.prototype, "constructor", {
value: Person
})`，在里面写默认属性都是false，在对象中写，默认属性为true以此达到重写原型的想法

# 面向对象-继承
1. var obj = {}  本质上等于 var obj = new Object()
2. obj对象是有__proto__

## 原型链实现方法的继承
1. 通过父类new一个对象，让子类的显式原型指向该对象，可以实现方法的继承
## 借用构造函数实现属性继承 | constructor stealing
1. 在子类中写`Person.call(this, name, age,height)`
	* 因为new操作创建空对象，**将空对象赋值给this**，通过call调用父类方法将this(指向student)传递给父类，那么在父类进行this.age = age就会使用的是子类的属性，就可以把属性都放在stu对象里面

## 组合借用继承的问题 | 组合继承
1. **弊端**
	* 调用两次构造函数
	* 所有的子类实例事实上都会拥有两份父类的属性

## 原型式继承函数 | 寄生组合式继承
1. 满足条件
	* 必须创建一个对象
	* 这个对象的隐式原型必须指向父类的显式原型
	* 将这个对象赋值给子类的显式原型

2. ```javascript
   // 方案一
   var obj = {}
   Object.setPrototypeOf(obj, Person.prototype)
   Student.prototype = obj
   
   // 方案二
   var  obj = Object.create(Person.prototype) //会创建一个对象，然后将该显式原型赋值给obj的隐式原型
   console.log(obj.__proto__)
   Student.prototype = obj
   // 方案三封装成函数,可能存在兼容性问题
   function inherit(SubType, SuperType) {
       subType.prototype = SuperType.prototype
       // 构造函数指向本身
       Object.defineProtoType(SubType.prototype, "constructor", {
           enumrable: false,
           configurable: true,
           writable: true,
           value: Subtype
       })
   }

# 防抖debounce 
1. 操作时不执行，确定不操作了才执行
1. 譬如：玩手机一直玩不会息屏，但一分钟后不玩就会息屏
1. 每次操作前都会先清除掉定时器，并开始定时器



# 节流 | throttle

1. 持续触发事件，到时间必须执行一次

2. 譬如：坐公交时，公交十分钟一趟

3. 接收一个函数，记录开启时间，记录当前时间，只有两者时间差值大于传入时间才触发，并用现在的时间赋值给开始时间

4. ```javascript
   function throttle(fn, time){
       let startTime = 0
       return function() {
           let nowTime = new Date()
           if(nowTime - startTime > time) {
               // 不理解这里
               fn.apply(this, arguments)
               startTime = nowTime
           }
       }
   }
   ```

5. 



# Promise

1. 优雅的异步请求，下一个函数的执行会依赖上一个函数执行的结果，传统上就是在函数中不断调用函数形成回调低于，而Promise就很好解决了这个问题
2. 三种状态 ： **pending、 fulfilled、rejected三种状态**
3. Promise本身是构造函数，可以通过new来创建，接收一个函数，函数又接受两个回调函数，then的执行本身依赖上一步的结果，then本身接收两个回调函数reject和resolve，每步写reject太麻烦了，就可以通过catch来进行异常捕获，在.catch的方法会监听上诉then的过程是否出错，finally无论怎么样都会执行。



# 递归

1. 反复剥洋葱皮，知道剥到尽头
2. 调用自身，设置终止条件

# 手写Promise

# ES6

1. **let、const**，避免使用var定义变量，避免变量提升
2. **模块化**，通过需要导出的模块前面加上export，需要引入的加上import from
3. **解构**：只需要取两个值，直接将数组赋值给另一个数组即可，中间元素使用空格代替
4. **扩展运算符**：拷贝数组(…arr赋值给)，合并数组，将多个数组扩展后放到新数组即可； 将数组扩展为函数的参数；克隆对象、合并对象
5. **给参数赋值默认值**
6. **对象属性的简写，增强语法**
7. **async、await**
8. **includes**：判断数组是否包含某一项
9. **指数操作符** 
10. **Object.keys()  | Object.values() | Object.entries()键值对**
11. null传导运算符 ？ ||  ？？
12. **模板字符串**

# async | await

1. 能暂停执行yeild()、也能恢复执行next()



# git

1. ![git提交流程](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230615231855558.png)



# 路由

1. 前端路由实现方式
2. **  # **hash
3. history
   1. back
   2. go
   3. 刷新页面可能404



![npm run serve执行了什么](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230616090402513.png)

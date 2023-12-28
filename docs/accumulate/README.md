# 前端积累

## html

### 请实现一个简单的页面布局，要求如下

---

1. 页面中包含一个头部，头部中包含一个标题
2. 页面中包含一个主体，主体中包含一个段落
3. 页面中包含一个底部，底部中包含一个按钮

---

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <header>
        <h1>标题</h1>
    </header>
    <main>
        <p>段落</p>
    </main>
    <footer>
        <button>按钮</button>
    </footer>
</body>
</html>
```

## css

### 三种css隐藏元素的方式有哪些？

> + `display: none`;这样的样式会让元素在页面上彻底消失，不占据任何空间。但是会被其他元素覆盖。所以会导致重排和重绘。
> + `visibility: hidden`;这样的样式会在页面消失之后，他原本占有的空间还会被保留。会导致浏览器的重绘，而不会导致重排。
> + `opacity: 0`;透明度为0。在视觉上也是隐藏的，会让元素在页面上彻底消失，但是会被其他元素覆盖。所以会导致重排和重绘。

### CSS 盒模型？

> + 1、每个html元素都可以看作一个盒子，这个盒子由里到外，由这个元素的内容content、边框border、内边距padding、外边距margin组成。
>
> + 2、盒子模型一般分为标准盒模型 和 怪异盒模型，怪异盒模型又叫做IE盒模型。这两种盒模型又有什么区别呢？
>
> + 3、在标准盒模型下，浏览器的width属性，就是内容content的宽度，也就是说，如果我们给一个元素设置width属性，那么width属性就是内容的宽度，此时这个元素盒子的总宽度就是：width + 内边距 + 边框 + 外边距，高度也是这样。而怪异盒模型，指的是浏览器的width属性不是内容的宽度，是元素的内容 + 内边距 + 边框的宽度之和。
换句话说，如果我们给一个元素设置width属性，那么这个盒子的总宽度就是：width + 外边距 之和。因为width已经包含了内容、内边距、边框。
> + 正常情况下默认是标准盒模型，但是我们可以通过box-sizing属性来指定盒模型，当它的值是border-box时，就是怪异盒模型。当值content-box时，就是标准盒模型，因为标准盒模型的width就是content。

### 3. 页面布局有哪几种方式？

> + 页面布局常用的方法有浮动、定位、flex、grid网格布局、栅格系统布局
> + 浮动：优点: 兼容性好。缺点:浮动会脱离标准文档流，因此要清除浮动。我们解决好这个问题即可。
> + 绝对定位。优点: 快捷。缺点: 导致子元素也脱离了标准文档流，可实用性差。
> + flex 布局 (CSS3中出现的)。优点: 解决上面两个方法的不足，fex布局比较完美。移动端基本用 flex布局。
> + 网格布局 (grid)。CSS3中引入的布局，很好用。代码量简化了很多。

### 利用网格布局实现的个左右300px中间自适应的布局

``` html

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Document</title>
<style>
html * {
padding: 0;
margin: 0;
}
/* 重要：设置容器为网格布局，宽度为100% */
.layout.grid .left-center-right {
display: grid;
width: 100%;
grid-template-rows: 100px;
grid-template-columns: 300px auto 300px; /* 重要：设置网格为三列，并设置每列的宽度。即可。*/
}
.layout.grid .left {
background: red;
}
.layout.grid .center {
background: green;
}
.layout.grid .right {
background: blue;
}
</style>
</head>
<body>
<section class="layout grid">
<article class="left-center-right">
<div class="left">我是 left</div>
<div class="center">
我是 center
<h1>网格布局解决方案</h1>
</div>
<div class="right">我是 right</div>
</article>
</section>
</body>
</html>

```

---

1. 页面中包含一个头部，头部中包含一个标题
2. 页面中包含一个主体，主体中包含一个段落
3. 页面中包含一个底部，底部中包含一个按钮

## js

### 请实现一个简单的事件机制，能够实现对事件的触发和监听

---

如：EventEmitter.on(); EventEmitter.trigger();
>

``` js
    <script>

        const EventEmitter = {

            on: function(type, handle) {

                //创建一个缓存

                this.cache = {};

                console.log(this);

                //判断是否有这个类型的事件

                if (!this.cache[type]) {

                    //没有则创建一个

                    this.cache[type] = [handle];

                } else {

                    //已经存在就推入

                    this.cache[type].push(handle);

                }

            },

            trigger: function(type) {

                //判断是否传入了参数，如果传入了就把它填进一个数组中

                var params = arguments.length > 1 ? Array.prototype.slice.call(arguments, 1) : [];

                if (this.cache[type]) {

                    this.cache[type].forEach(item => {

                        //执行函数，并将参数传入

                        item(params);

                    })

                }

            }

        }

    </script>
```

---

---

### 创建一个new

---

``` js
 <script>

        function mynews(Func, ...args) {

            const obj = {};

            obj.__proto__ = Func.prototype;

            let result = Func.apply(obj, args);

            return result instanceof Object ? result : obj;

        }

    </script>

```

---

### 创建ajax的步骤

---

``` js
 <script>

        //创建XMLHttprequest()对象

        var ajax = new XMLHttpRequest();

        //设置请求的方式，url，是否异步

        ajax.open("GET", url, true);

        //发送信息至服务器时内容编码类型

        ajax.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

        //发送请求

        ajax.send();

        //接受服务器响应数据

        ajax.onreadystatechange = () => {



        };

    </script>
```

---

### 请基于以下代码实现功能：点击 1000 个 span 元素中的任意一个，将元素内的值 alert 弹出即可

---

``` js
//  <div id=“box”>

//         <span> 1 </span><span> 2

//     </span><span> 3 </span>…<span> 1000 </span>

//     </div>

    <script>

        var box = document.querySelector('#box');

        box.addEventListener('click',

            function(e) {

                var target = e.target;

                if (target.nodeName.toLowerCase() === 'span') {

                    alert(target.innerText);

                }

            }, false);

    </script>
```

---

### 发布订阅

---

``` js
 <script>

        let fs = require("fs");

        let evenobj = {

            arr: [],

            on(event, fn) {

                // if(this.arr[event]){

                //     this.arr[event].push(fn);

                // }else{

                //     this.arr[event]=[];

                //     this.arr[event].push(fn);

                // }

                (this.arr[event] || (this.arr[event] = []).push(fn))

            },

            emit() {

                let event = [].shift.call(arguments);

                if (this.arr[event]) {

                    this.arr[event].forEach(fn => fn.apply(this.arguments));

                }

            }

        }

        evenobj.on("data1", function(x) {

            console.log("订阅1" + x);

        });

        fs.readFile("1.txt", (err, res) => {

            evenobj.emit("data1", res);

        });

    </script>

```

---

### 防抖与节流原理代码实现

---

``` js

 <script>

        //     1）防抖



        // 原理：在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则重新计时。

        // 适用场景：

        // 按钮提交场景：防止多次提交按钮，只执行最后提交的一次

        // 搜索框联想场景：防止联想发送请求，只发送最后一次输入

        // 简易版实现

        function debounce(func, wait) {

            let timeout;

            return function() {

                const context = this;

                const args = arguments;

                clearTimeout(timeout)

                timeout = setTimeout(function() {

                    func.apply(context, args)

                }, wait);

            }

        }

        // 立即执行版实现

        // 有时希望立刻执行函数，然后等到停止触发 n 秒后，才可以重新触发执行。

        // 有时希望立刻执行函数，然后等到停止触发 n 秒后，才可以重新触发执行。

        function debounce(func, wait, immediate) {

            let timeout;

            return function() {

                const context = this;

                const args = arguments;

                if (timeout) clearTimeout(timeout);

                if (immediate) {

                    const callNow = !timeout;

                    timeout = setTimeout(function() {

                        timeout = null;

                    }, wait)

                    if (callNow) func.apply(context, args)

                } else {

                    timeout = setTimeout(function() {

                        func.apply(context, args)

                    }, wait);

                }

            }

        }

        // 返回值版实现

        // func函数可能会有返回值，所以需要返回函数结果，但是当 immediate 为 false 的时候，

        //因为使用了 setTimeout ，我们将 func.apply(context, args) 的返回值赋给变量，最后再 return 的时候，

        //值将会一直是 undefined，所以只在 immediate 为 true 的时候返回函数的执行结果。

        function debounce(func, wait, immediate) {

            let timeout, result;

            return function() {

                const context = this;

                const args = arguments;

                if (timeout) clearTimeout(timeout);

                if (immediate) {

                    const callNow = !timeout;

                    timeout = setTimeout(function() {

                        timeout = null;

                    }, wait)

                    if (callNow) result = func.apply(context, args)

                } else {

                    timeout = setTimeout(function() {

                        func.apply(context, args)

                    }, wait);

                }

                return result;

            }

        }

        // 2）节流



        // 原理：规定在一个单位时间内，只能触发一次函数。如果这个单位时间内触发多次函数，只有一次生效。

        // 适用场景

        // 拖拽场景：固定时间内只执行一次，防止超高频次触发位置变动

        // 缩放场景：监控浏览器resize

        // 使用时间戳实现

        // 使用时间戳，当触发事件的时候，我们取出当前的时间戳，然后减去之前的时间戳(最一开始值设为 0 )，

        //如果大于设置的时间周期，就执行函数，然后更新时间戳为当前的时间戳，如果小于，就不执行。

        function throttle(func, wait) {

            let context, args;

            let previous = 0;



            return function() {

                let now = +new Date();

                context = this;

                args = arguments;

                if (now - previous > wait) {

                    func.apply(context, args);

                    previous = now;

                }

            }

        }

        // 使用定时器实现

        // 当触发事件的时候，我们设置一个定时器，再触发事件的时候，如果定时器存在，就不执行，直到定时器执行，

        //然后执行函数，清空定时器，这样就可以设置下个定时器。

        function throttle(func, wait) {

            let timeout;

            return function() {

                const context = this;

                const args = arguments;

                if (!timeout) {

                    timeout = setTimeout(function() {

                        timeout = null;

                        func.apply(context, args)

                    }, wait)

                }



            }

        }

    </script>

```

---

### 斐波那契数列

---

``` js
<script>

        function fib(n) {

            if (n < 0) throw new Error('输入的数字不能小于0');

            if (n < 2) {

                return n;

            }

            let list = [];

            list[0] = 0;

            list[1] = 1;

            for (let i = 1; i < n; i++) {

                list[i + 1] = list[i] + list[i - 1];

            }

            return list[n];

        }

    </script>

```

---

### 有一堆整数，请把他们分成三份，确保每一份和尽量相等（11，42，23，4，5，6 4 5 6 11 23 42 56 78 90）

---

``` js

 <script>

        function foo(arr) {

            let AMOUNT = arr.length

            if (!AMOUNT) return false;

            if (AMOUNT === 3) return arr;

            arr.sort((a, b) => a - b);

            let total = 0;

            let maxNumberTotal = 0;

            for (let i = 0; i < AMOUNT; i++) {

                total += arr[i];

            }

            maxNumberTotal = total / 3;

            let tempTotal = arr[AMOUNT - 1];



            let firstArr = [arr[AMOUNT - 1]];

            let delIndex = [AMOUNT - 1];

            let firstIndex = -1;



            // 获取第一份数组

            for (let i = AMOUNT - 2; i > 0; i--) {

                const el = arr[i];

                tempTotal += el; // 每次拿最大的;

                firstArr.push(el);

                delIndex.push(i);

                if (tempTotal === maxNumberTotal) { // 刚好等于最大值跳出循环

                    break;

                } else if (tempTotal > maxNumberTotal) { // 发现超过最大值, 减回去

                    tempTotal -= el;

                    delIndex.pop();

                    firstArr.pop();

                } else if (tempTotal < maxNumberTotal) { // 发现超过最小值, 处理边界问题

                    let nextTotal = tempTotal + arr[i + 1]

                    if (maxNumberTotal - tempTotal < Math.abs(maxNumberTotal - nextTotal)) { // 当前总值比上一个总值大; 这里是临界值, 说明上一个总值肯定是一个比最大值大, 所以这里需要和绝对值比较

                        if (maxNumberTotal - tempTotal > arr[0]) { // 如果下一个平局值和总值相减, 比数组第一个数还大, 说明还可以继续走下去;

                            continue;

                        } else {

                            break;

                        }

                    }

                }

            }

            for (let i = 0; i < delIndex.length; i++) {

                arr.splice(delIndex[i], 1)

            }



            AMOUNT = arr.length; // 注意每次的arr都是不一样的

            let secondArr = [arr[AMOUNT - 1]];

            delIndex = [AMOUNT - 1];

            let secondIndex = -1;

            tempTotal = arr[AMOUNT - 1];

            // 获取第二份数组

            for (let i = AMOUNT - 2; i > 0; i--) {

                const el = arr[i];

                tempTotal += el; // 每次拿最大的;

                secondArr.push(el);

                delIndex.push(i);

                if (tempTotal === maxNumberTotal) { // 刚好等于最大值跳出循环

                    break;

                } else if (tempTotal > maxNumberTotal) { // 发现超过最大值, 减回去

                    tempTotal -= el;

                    delIndex.pop();

                    secondArr.pop();

                } else if (tempTotal < maxNumberTotal) { // 发现超过最小值, 处理边界问题

                    let nextTotal = tempTotal + arr[i + 1]

                    if (maxNumberTotal - tempTotal < Math.abs(maxNumberTotal - nextTotal)) { // 当前总值恒小于下一个总值; 这里是临界值

                        if (maxNumberTotal - tempTotal > arr[0]) {

                            continue;

                        } else {

                            break;

                        }

                    }

                }

            }

            for (let i = 0; i < delIndex.length; i++) {

                arr.splice(delIndex[i], 1)

            }

            // 公平处理, 当出现极差情况就需要做公平处理了, 这里暂时不考虑极差情况

            return [firstArr, secondArr, arr]

        }

    </script>

```

---

### 工厂模式创建对象

---

```javascript
<script>

        var obj = {};



        function CJDX(name, age, sex) {

            // var obj = new Object();

            this.name = name;

            this.age = age;

            this.sex = sex;

            // obj.sayName = function() {



            // };

            // return obj;

        };

        //原型中添加公共的方法，提高运行效率

        CJDX.prototype.sayName = function() {

            console.log("我是谁:" + this.name);

            //console.log("nihao");

        }

        var frist = new CJDX("孙悟空", 18, "男");

        var second = new CJDX("猪八戒", 20, "男");

        var three = new CJDX("沙和尚", 28, "男");

        frist.sayName();

    </script>

```

---

### 合并二维有序数组成一维有序数组，归并排序的思路

---

```javascript
<script>

        // let arr = [11, [1, 2, 3], 11, [1, 4, 5, [76, 8, 9, 0]]];

        // //扁平化处理

        // let arr1 = arr.toString().split(',').map(item => parseFloat(item));

        // //去重

        // let result = [...new Set(arr1)];

        // //排序

        // let pai=

        // console.log(result);

        /**

         * 解题思路：

         * 双指针 从头到尾比较 两个数组的第一个值，根据值的大小依次插入到新的数组中

         * 空间复杂度：O(m + n)

         * 时间复杂度：O(m + n)

         * @param {Array} arr1

         * @param {Array} arr2

         */



        function merge(arr1, arr2) {

            var result = [];

            while (arr1.length > 0 && arr2.length > 0) {

                if (arr1[0] < arr2[0]) {

                    /*shift()方法用于把数组的第一个元素从其中删除，并返回第一个元素的值。*/

                    result.push(arr1.shift());

                } else {

                    result.push(arr2.shift());

                }

            }

            return result.concat(arr1).concat(arr2);

        }



        function mergeSort(arr) {

            let lengthArr = arr.length;

            if (lengthArr === 0) {

                return [];

            }

            while (arr.length > 1) {

                let arrayItem1 = arr.shift();

                let arrayItem2 = arr.shift();

                let mergeArr = merge(arrayItem1, arrayItem2);

                arr.push(mergeArr);

            }

            return arr[0];

        }

        let arr1 = [

            [1, 2, 3],

            [4, 5, 6],

            [7, 8, 9],

            [1, 2, 3],

            [4, 5, 6]

        ];

        let arr2 = [

            [1, 4, 6],

            [7, 8, 10],

            [2, 6, 9],

            [3, 7, 13],

            [1, 5, 12]

        ];

        mergeSort(arr1);

        console.log(arr1);

        mergeSort(arr2);

    </script>

```

---

### 垃圾回收机制

---

基本的垃圾回收算法为“标记-清除”，定期执行垃圾回收

#### 第一步：标记空间中的【可达】值

> 1.1 V8 采用的是可达性 (reachability) 算法来判断堆中的对象应不应该被回收。
>
> 1.2 这个算法的思路是这样的：
>
> 1.3 从根节点（Root）出发，遍历所有的对象。
>
> 1.4 可以遍历到的对象，是可达的（reachable）。
>
> 1.5 没有被遍历到的对象，不可达的（unreachable）。
>
> 1.6 在浏览器环境下，根节点有很多，主要包括这几种：
>
> 1.7 全局变量 window，位于每个 iframe 中
>
> 1.8 文档 DOM 树
>
> 1.9 存放在栈上的变量...
>
> 1.10 这些根节点不是垃圾，不可能被回收。

#### 第二步：回收 不可达 的值占用的内存

> 2.1 在所有的标记完成之后，统一清理内存中所有不可达的对象。

#### 第三步，做内存整理

> 3.1 在频繁回收对象后，内存中就会存在大量不连续空间，专业名词叫「内存碎片」。
>
> 3.2 当内存中出现了大量的内存碎片，如果需要分配较大的连续内存时，就有可能出现内存不足的情况。
>
> 3.3 所以最后一步是整理内存碎片。(但这步其实是可选的，因为有的垃圾回收器不会产生内存碎片，比如接下来我们要介绍的副垃圾回收器。)

##### 什么时候进行垃圾回收

> 3.4 浏览器进行垃圾回收的时候，会暂停 JavaScript 脚本，等垃圾回收完毕再继续执行。
>
> 3.5 对于普通应用这样没什么问题，但对于 JS 游戏、动画对连贯性要求比较高的应用，如果暂停时间很长就会造成页面卡顿。
>
> 3.6 这就是我们接下来谈的关于垃圾回收的问题：什么时候进行垃圾回收，可以避免长时间暂停。
>
> 3.7 类数组和数组的区别，dom 的类数组如何转换成数组

---

---

### 类数组转换为数组转换方法

> 1.1 使用 `Array.from()`
>
> 1.2 使用 `Array.prototype.slice.call()`
>
> 1.3 使用 `Array.prototype.forEach()` 进行属性遍历并组成新的数组

#### 转换须知

> 转换后的数组长度由 length 属性决定。索引不连续时转换结果是连续的，会自动补位。

#### 代码示例

---

``` js
 <script>

        // 原型关系和原始值转换

        let arrayLike = {

            length: 10,

        };

        console.log(arrayLike instanceof Array); // false

        console.log(arrayLike.__proto__.constructor === Array); // false

        console.log(arrayLike.toString()); // [object Object]

        console.log(arrayLike.valueOf()); // {length: 10}



        let array = [];

        console.log(array instanceof Array); // true

        console.log(array.__proto__.constructor === Array); // true

        console.log(array.toString()); // ''

        console.log(array.valueOf()); // []

    </script>

```

``` js
    <script>

        let al1 = {

            length: 4,

            0: 0,

            1: 1,

            3: 3,

            4: 4,

            5: 5,

        };

        console.log(Array.from(al1)) // [0, 1, undefined, 3]

    </script>

```

### 逆序数组元素

``` js
<script>

    //求字符串 'hello world' 对应的ASCII码数组，并按照编码大小逆序。

    //输入： 'hello world’

    //输出：[119, 114, 111, 111, 108, 108, 108, 104, 101, 100, 32]

    const str = 'hello world';

    const array = str.split('').map(letter => {

            return

            letter.charCodeAt();

        }).sort(function() {

                return arguments[1] - arguments[0];

            }

</script>

```

### 求丑数

``` js
<script>

        const getUglyNumber = n => {

            if (n >= 1) {

                const temp = [1],

                    result = [1];

                let i = 1,

                    index2 = 0,

                    index3 = 0,

                    index5 = 0;

                while (result.length < n) {

                    temp[i] = Math.min(temp[index2] * 2, temp[index3] * 3, temp[index5] * 5);

                    if (temp[i] == temp[index2] * 2) {

                        index2++;

                    } else if (temp[i] == temp[index3] * 3) {

                        index3++;

                    } else if (temp[i] == temp[index5] * 5) {

                        index5++;

                    }

                    if (result.indexOf(temp[i]) == -1) {

                        result.push(temp[i]);

                    }

                    i++;

                }

                return result[n - 1];

            }

        }

    </script>

```

### 判断是否是质数

``` js
<script>

        console.time("test");

        var number = parseInt(prompt("请输入一个大于一的数字："));



        if (number <= 1) {

            alert("请输入一个大于一的数字：");

            var number = parseInt(prompt("请输入一个大于一的数字："));

        } else {

            var flag = true;

            for (var i = 2; i < number; i++) {

                for (var j = 2; j <= Math.sqrt(number); j++) {

                    if (number % j == 0) {

                        //则不是质数

                        flag = false;

                        break;

                    }

                }



            }

            if (flag) {

                alert(number + "是质数");

            } else {

                alert(number + "不是质数");

            }

        }

        console.timeEnd("test");

    </script>

```

### 求在第几次买入可以获取最高利润

``` js
<script>

        var arr = [100, 108, 90, 88, 101, 80, 89, 86];

        var max = 0,

            first = 0,

            end = 0;

        arr.forEach((item, i) => {

            for (var j = i + 1; j < arr.length; j++) {

                if (arr[j] - item > max) {

                    max = arr[j] - item;

                    first = i;

                    end = j;

                }

            }

            if (i == arr.length - 1) {

                console.log('在第' + first + '次买入，' + '在第' + end + '次卖出，' + '可获得最高利润' + max);

            }

        })

    </script>

```

### 求数组中元素相加的最大值

``` js
<script>
        function maxNum(numArr) {

            for (var i = 0; i < numArr.length - 2; i++) {

                // console.log(numArr[i + 1].toString().length)

                // if (numArr[i].toString().length == 1 && (numArr[i].toString()[0] == numArr[i + 1].toString()[0])) {

                //     var k = numArr[i + 1];

                //     numArr[i + 1] = numArr[i];

                //     numArr[i] = k;

                // }



            }

            console.log(numArr)

            var newArr = numArr.reverse().join('');

            //console.log(typeof newArr);

            return newArr;



        }

        console.log(maxNum([21, 35, 34, 86, 9, 8, 7]));

        //console.log(typeof newArr);

    </script>

```

### 去掉字符串中的空格

``` js
<script>

        var str = "     Hello World!     ";

        alert(str.replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, ''));

    </script>

字符串中字符出现的次数
<script>

        const str = 'asddfgdfwwqeweqwezczxcsdfgdgd';

        let map = {};

        let maxTimes = 0,

            target;

        for (let i = 0; i < str.length; i++) {

            if (map[str[i]] !== undefined) {

                map[str[i]]++;

            } else {

                map[str[i]] = 1;

            }

            if (map[str[i]] > maxTimes) {

                maxTimes = map[str[i]];

                target = str[i];

            }

        }

        map = null;

        console.log(target, maxTimes);

    </script>

```

### Url中的参数截取
<!-- 编写 JavaScript 函数，其唯一的输入参数为URL字符串，函数返回一个对象。返回对象中的属性包括 URL 中的

    全部查询字符串（Query）字段。例如，输入字符串 “https://www.yonyoucloud.com?name=yonyou&location=beijing” 返回

    { name: “yonyou”, location: “beijing” } -->

``` js
    <script>

        var url =

            'https://www.yonyoucloud.com?name=yonyou&location=beijing';

        var obj = parseQueryString(url);



        function parseQueryString(argu) {

            var str = argu.split('?')[1];

            console.log(str);

            var result = {};

            var temp = str.split('&');

            console.log(temp);

            for (var i = 0; i < temp.length; i++) {

                var temp2 = temp[i].split('=');

                result[temp2[0]] = temp2[1];

            }

            return result;



        }

        console.log(obj);

    </script>

```

### 原型链原理
 <!-- 原型链是用来查找（实例）对象属性 -->

``` js
    <script>

        function Fn() { //内部语句：this.prototype={};



        }

        //每个函数都有一个显示原型prototype:默认指向一个空的object（实例）对象。

        console.log(Fn.prototype);

        var fn = new Fn(); //内部语句：this.__proto__=Fn.prototype

        //每个实例都有一个隐式原型：__proto__

        console.log(fn.__proto__);

        //对象的显示原型等于实例的隐式原型

        //实例对象的隐式原型等于构造函数的显示原型

        console.log(Fn.prototype === fn.__proto__); //true

        Fn.prototype.test = function() {

            console.log('test');

        }

        fn.test(); //test

        //显示原型指向的对象默认是空object实例对象（但object不满足）；

        console.log(Fn.prototype instanceof Object); //true

        console.log(Object.prototype instanceof Object); //false

        console.log(Function.prototype instanceof Object); //true

        //所有的函数都是Function的实例（包含Function）

        console.log(Function.__proto__ === Function.prototype); //true

        //Object的原型对象是原型链的尽头

        console.log(Object.prototype.__proto__); //null

        //读取对象的属性值时：会自动到原型链上查找

        //设置对象属性值时：不会查找原型链，如果当前对象没有次属性，则直接添加属性并且设置值

        //方法一般定义在原型中，属性一般通过构造函数定义在对象的本身上。

    </script>

    <script>

        function A() {



        }

        A.prototype.n = 1;

        //实例b还是指向的A的旧的对象

        var b = new A();

        //此时A指向了一个新的对象

        A.prototype = {

                n: 1,

                m: 2

            }

            //实例c指向的是A的新的对象

        var c = new A();

        console.log(b.n, b.m, c.n, c.m); //1  undefined  1  2

    </script>

    <script>

        function F() {}

        Object.prototype.a = function() {

            console.log('bbb');

        }

        Function.prototype.B = function() {

            console.log('bbbbb');

        }

        var f = new F();

        f.a(); //bbb

        f.B(); //报错

        F.a(); //bbb

        F.B(); //bbbbb

        console.log();

    </script>

```

## css

### 盒子居中

```html
<!DOCTYPE html>

<html lang="en">



<head>

    <meta charset="UTF-8">

    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <style>

        /* .fuji {

            width: 100px;

            display: flex;

            background-color: blue;

            justify-content: center;

            align-items: center;

        }

       

        .zi {

            margin: auto;

            justify-content: center;

        } */

        /* 第一种: 利用margin定位*/

        /* .center {

            width: 100px;

            height: 100px;

            background: red;

            position: absolute;

            top: 0;

            left: 0;

            bottom: 0;

            right: 0;

            margin: auto;

        }

       

        .ziji {

            text-align: center;

            line-height: 100px;

        } */

        /* 第二种：利用table—cell */

        /* .center {

            display: table-cell;

            text-align: center;

            vertical-align: middle;

        }

       

        .ziji {

            display: inline-block;

        } */

        /* 垂直居中 */

        /* .center {

            display: flex;

            justify-content: center;

            align-items: center;

        }

       

        .ziji {} */

        /* 垂直居中结束 */

        /* 第三种：利用相对定位和绝对定位实现 */

        /* .center {

            position: relative;

        }

       

        .ziji {

            position: absolute;

            left: 50%;

            top: 50%;

            transform: translate(-50%, -50%);

        } */

        /* 垂直水平居中 */

        /* 第一中方法 */

        /* .wrap {

            width: 300px;

            height: 300px;

            background-color: #e3e3e3;

            position: relative;

        }

       

        .box {

            width: 100px;

            height: 100px;

            background-color: brown;

            position: absolute;

            top: 50%;

            left: 50%;

            transform: translate(-50%, -50%);

        } */

        /* 第一中方式结束 */

        /* 第二种方式开始 */

       

        .wrap {

            width: 300px;

            height: 300px;

            background-color: #e3e3e3;

            display: flex;

            justify-content: center;

            align-items: center;

        }

       

        .box {

            width: 100px;

            height: 100px;

            background-color: brown;

        }

        /* 第二种方式结束 */

        /* 第三种方式开始 */

       

        .wrap {

            width: 300px;

            height: 300px;

            background-color: #e3e3e3;

            display: table-cell;

            vertical-align: middle;

        }

       

        .box {

            width: 100px;

            height: 100px;

            background-color: brown;

            margin: auto;

        }

        /* 第三种方式结束 */

    </style>

</head>



<body>

    <div class="wrap">

        <div class="box"></div>

    </div>

    <!-- <div class="center">

        <div class="ziji">

            居中

        </div>

    </div> -->

    <!-- <div class="zi">

        盒子

    </div>

    <div class="fuji">

        <div class="zi">

            盒子

        </div>

    </div> -->

</body>



</html>

```

### 三种定位的区别

---
> relative:相对定位，相对于自己的定位，并没有脱离标准文档流
>
> absolute:绝对定位：相对于自己最近的父级元素做定位（先找父元素，父元素如果没定位，继续向上寻找爷爷辈的元素，以此类推），脱离了标准的文档流
>
> fixed:固定定位，相对于可视窗口的定位，脱离了标准的文档流
>
> static:默认的定位，相当于没有定位

---

### Css中的伪类

---

#### 伪类(pseudo-classes)

> 其核⼼就是⽤来选择DOM树之外的信息,不能够被普通选择器选择的⽂档之外的元素，⽤来添加⼀些选择器的特殊效果。
⽐如:hover :active :visited :link :visited :first-child :focus :lang等
>
> 由于状态的变化是⾮静态的，所以元素达到⼀个特定状态时，它可能得到⼀个伪类的样式；当状态改变时，它⼜会失去这个样式。
由此可以看出，它的功能和class有些类似，但它是基于⽂档之外的抽象，所以叫 伪类。

#### 伪元素(Pseudo-elements)

> DOM树没有定义的虚拟元素,核⼼就是需要创建通常不存在于⽂档中的元素。
⽐如::before ::after 它选择的是元素指定内容，表示选择元素内容的之前内容或之后内容。
伪元素控制的内容和元素是没有差别的，但是它本身只是基于元素的抽象，并不存在于⽂档中，所以称为伪元素。⽤于将特殊的效果添加到某些选择器

#### 伪类与伪元素的区别

##### 表示⽅法不同

> CSS2 中伪类、伪元素都是以单冒号:表示
>
> CSS2.1 后规定伪类⽤单冒号表示,伪元素⽤双冒号::表示
>
> 浏览器同样接受 CSS2 时代已经存在的伪元素(:before, :after, :first�line, :first-letter 等)的单冒号写法。
>
> CSS2 之后所有新增的伪元素(如::selection)，应该采⽤双冒号的写法。
>
> CSS3中，伪类与伪元素在语法上也有所区别，伪元素修改为以::开头。浏览器对以:开头的伪元素也继续⽀持，但建议规范书写为::开头

#### 定义不同

> 伪类即假的类，可以添加类来达到效果
>
> 伪元素即假元素，需要通过添加元素才能达到效果

#### 总结

> 伪类和伪元素都是⽤来表示⽂档树以外的"元素"。
>
> 伪类和伪元素分别⽤单冒号:和双冒号::来表示。
>
> 伪类和伪元素的区别，关键点在于如果没有伪元素(或伪类)，
>
> 是否需要添加元素才能达到效果，如果是则是伪元素，反之则是伪类。
>
> 伪类其实就是基于普通DOM元素⽽产⽣的不同状态，他是DOM元素的某⼀特征。
>
> 伪元素能够创建在DOM树中不存在的抽象对象，⽽且这些抽象对象是能够访问到的。

##### 相同之处

> 伪类和伪元素都不出现在源⽂件和DOM树中。也就是说在html源⽂件中是看不到伪类和伪元素的。

---

### 垂直水平居中

``` html
<!DOCTYPE html>

<html lang="en">



<head>

    <meta charset="UTF-8">

    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <style>

        .fulei {

            width: 400px;

            height: 400px;

            background-color: #bfa;

            position: relative;

            margin: 0 auto;

        }

       

        .zilei {

            width: 100px;

            height: 100px;

            background-color: red;

            position: absolute;

            /* 锤子水平居中 */

            left: 0;

            right: 0;

            top: 0;

            bottom: 0;

            margin: auto;

            /* margin-left: auto;

            margin-right: auto; */

        }

    </style>

</head>



<body>

    <div class="fulei">

        <div class="zilei"></div>

    </div>

</body>



</html>

```

### 媒体查询

---
> all：所有设备
>
> print:打印设备
>
> speech:屏幕阅读器
>
> screen:带屏幕的设备
>
> 表示只有屏幕可以使用（老版本的浏览器可以使用） @media only screen {}

---

### 媒体查询的特性

---

> width:视口的宽度
>
> height:视口的高度
>
> min-width:视口的最小宽度
>
> max-width:视口的最大宽度
>
> ,(逗号):或者
>
> and:和
>
> not:除了

---

```css

        @media only screen and (min-width:500px) and (max-width:780px) {

            body {

                background-color: orange;

            }

        }

       

        @media (width:500px) {

            body {

                background-color: #bfa;

            }

        }

       

        @media all {

            body {

                background-color: #bfa;

            }

        }
```

``` css

flex-direction:弹性盒子中元素的排列方式

flex-shrink:收缩性(默认1)

flex-grow：伸展（1）

flex-wrap:wrap;//换行

flex-wrap:nowrap;//不换行

flex-flow: row wrap;//换行并且row排列

justify-content:flex-start//元素沿着排列的起边开始排列

justify-content:flex-end//元素沿着排列的主轴的终边排列

```

### ​关于link与@import的区别

---

::: tip 区别1：

link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。

:::

::: tip 区别2：

link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。

:::

::: tip 区别3：

link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。

:::

::: tip 区别4：

link支持使用Javascript控制DOM去改变样式；而@import不支持。

:::

---

### css可继承属性

> 1.所有元素可继承：`visibility`和`cursor`。
> 2.内联元素可继承：
>>
>> + letter-spacing
>> + word-spacing
>> + white-space
>> + line-height
>> + color
>> + font
>> + font-family
>> + font-size
>> + font-style
>> + font-variant
>> + font-weight
>> + text-decoration
>> + text-transform
>> + direction
> 3.终端块状元素可继承：`text-indent`和`text-align`。
> 4.列表元素可继承：`list-style`、`list-style-type`、`list-style-position`、`list-style-image`。`
> 5.在CSS中，html中的标签元素大体被分为三种不同的类型： `块状元素`、`内联元素(又叫行内元素)`和`内联块状元素`。

### 常用的块状元素有

---

`<div>` `<p>` `<h1>…<h6>` `<ol>` `<ul>` `<dl>` `<table>` `<address>` `<blockquote>` `<form>`

---

### 什么是块级元素？

---

在html中`<div>`、`<p>`、`<h1>`、`<form>`、`<ul>`和`<li>`就是块级元素。设置`display:block`就是将元素显示为块级元素。如下代码就是将内联元素`a`转换为块状元素，从而使`a`元素具有块状元素特点。 `a{display:block;}`

---

### 块级元素特点

---
::: tip 一：
每个块级元素都从新的一行开始，并且其后的元素也另起一行。（真霸道，一个块级元素独占一行）;
:::
::: tip 二：
元素的高度、宽度、行高以及顶和底边距都可设置。
:::
::: tip 三：
元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致），除非设定一个宽度。
:::

---

### 常用的内联元素有

---

`<a>`、`<span>`、`<br>`、`<i>`、`<em>`、`<strong>`、`<label>`、`<q>`、`<var>`、`<cite>`、`<code>` 在html中，`<span>`、`<a>`、`<label>`、`<strong>` 和`<em>`就是典型的内联元素（行内元素）（inline）元素。
当然块状元素也可以通过代码`display:inline;`将元素设置为内联元素。如下代码就是将块状元素div转换为内联元素，从而使div 元素具有内联元素特点。

``` html
div{ display:inline; } ......
<div>我要变成内联元素</div>
 ```

---

### 内联元素特点

---
> 1、和其他元素都在一行上.
> 2、元素的高度、宽度及顶部和底部边距不可设置； （这是答案^-^）
> 3、元素的宽度就是它包含的文字或图片的宽度，不可改变。
---

### 常用的内联块状元素有

---
 `<img>`、`<input>`
内联块状元素（`inline-block`）就是同时具备内联元素、块状元素的特点，代码`display:inline-block`就是将元素设置为内联块状元素。

---

### inline-block元素特点

---

> 1、和其他元素都在一行上.
> 2、元素的高度、宽度、行高以及顶和底边距都可设置。

---

### `display:none`和`visibility:hidden`都能把网页上某个元素隐藏起来，但是两者有区别

---

### display:none

> 1、不为被隐藏的对象保留其物理空间。html对象在页面上彻底消失（`display:none`会让元素完全从渲染树中消失，渲染的时候不占据任何空间）。
>
> 2、是非继承属性，子孙节点消失由于元素从渲染树消失造成的，通过修改子孙节点，属性无法显示。
>
> 3、修改常规文档流元素的`display`通常会造成文档的重排（`reflow`）重绘（`repaint`）。

### visibility:hidden

> 1、为隐藏的对象保留其物理空间，html对象仅仅是在视觉上看不见（完全透明），而它所占据的空间位置仍然存在（`visibility:hidden`不会让元素从渲染树中消失，渲染树元素继续占据空间，只是内容不可见）。
>
> 2、是继承，子孙节点消失由于继承了`hidden`，通过`visibility:visible`可以让子孙节点显示。
>
> 3、修改`visibility`属性只会造成文档的重绘（`repaint`）。

---

### 添加哪个属性可以使超出的文字部分变成「…」

``` css
(text-overflow:ellipsis)
```

### HTML5 中使用的媒体元素？

---
> 1.Source
>
> 2.Audio
>
> 3.Track
---

### 关于positon的属性

---
![position定位的属性](/images/position.png)
>
Inhert：规定应该从父元素继承position属性的值

---

### 关于 CSS 布局中的 BFC 是

---

BFC就是“块级格式化上下文”的意思，创建了 BFC的元素就是一个独立的盒子，不过只有Block-level box可以参与创建BFC， 它规定了内部的Block-level Box如何布局，并且与这个独立盒子里的布局不受外部影响，当然它也不会影响到外面的元素。
内部的Box会在垂直方向，从顶部开始一个接一个地放置。
Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生叠加
每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
BFC的区域不会与float box叠加。
BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然。
计算BFC的高度时，浮动元素也参与计算。

---

### Reflow（回流）和 Repaint（重绘）的描述

---

![Reflow（回流）和 Repaint（重绘）](/images/reflowRepaint.png)
>
> 1.ele.clientWidth = 宽度 + padding
>
> 2.ele.offsetWidth = 宽度 + padding + border
>
> 3.ele.scrollTop = 被卷去的上侧距离
>
> 4.ele.scrollHeight = 自身实际的高度（不包括边框）

---

>

---
|  属性   | 描述  |
| :---  | :---  |
| linear  | 动画从头到尾的速度是相同的。 |
| ease  | 默认动画以低速开始，然后加快，在结束前变慢。 |
| ease-in  | 动画以低速开始。 |
| ease-out  | 动画以低速结束。 |
| ease-in-out  | 动画以低速开始和结束。 |
| cubic-bezier(n,n,n,n)  | 在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值。 |

---
<!-- <table>
    <tr>
        <td>属性</td>
        <td>描述</td>
    </tr>
    <tr>
        <td>linear</td>
        <td>动画从头到尾的速度是相同的。</td>
    </tr>
    <tr>
        <td>ease</td>
        <td>默认动画以低速开始，然后加快，在结束前变慢。</td>
    </tr>
    <tr>
        <td>ease-in</td>
        <td>动画以低速开始。</td>
    </tr>
    <tr>
        <td>ease-out</td>
        <td>动画以低速结束。</td>
    </tr>
    <tr>
        <td>ease-in-out</td>
        <td>动画以低速开始和结束。</td>
    </tr>
    <tr>
        <td>cubic-bezier(n,n,n,n)</td>
        <td>在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值。</td>
    </tr>
</table> -->

### 不同浏览器提供的编程环境不一致，所以在编程时才要使用 -ms、-webkit、-moz来实现不同浏览器的兼容性

### JS文件按在HTML中引入的顺序依次载入（不是最后载入），在载入后马上执行，执行时会阻塞页面后续的内容（包括页面的渲染、其它资源的下载）

### 箭头函数不能调用Funciton的bind、apply、call方法（Function类具有的方法），没有继承Function类

### Background-position属性

---

> 1.用处：配合background-image属性一起使用，用于设置背景图片在盒子中的位置
>
> 2.参数：xpos ypos |x% y% |x y三种,
>
> 3.如果只写第一个水平方向的参数，第二个垂直方向的参数会默认为：enter|50%|容器高度的一半px.
>
> 4.Xpos：规定水平方向的对齐方式,值有left,right,center
>
> 5.Ypos：规定垂直方向的对齐方式,值有top,bottom,center
>
> 6.x%:规定图片水平方向的距离。
>
> 7.你会不会以为这个x%就是父级容器宽度的x%？那你就想错了哦，这里的x%指的是父级容器的宽度减去图片的宽度后的差值的x%。
>
> 8.举个栗子：background-position：50%，20%；
>
> 9.图片的宽度为     imgwidth：100px；高度为     imgheight：100px；
>
> 10.容器的宽度为     conwidth：200px；高度为     conheight：200px；
>
> 11.那么此时图片的左顶点距离容器的左顶点的水平距离就是(conwidth-imgwidth)*50%=50px,而不是conwidth*50%=100px；(很好理解的吧，不然盒子宽度200px，图片宽度100px，又距离左边100px，岂不是50%没实现水平居中而紧靠右了吗？)
由此也可以算出图片的左顶点距离容器的左顶点的垂直距离为20px
> 12.y%:对应x%
>
> 13.x:图片距离容器水平方向距离
>
> 14.y:图片距离容器垂直方向距离

---

### 盒模型

---

默认的盒子模型是content-box
Input标签的readonly属性
Readonly规定输入的字段为只读，即用户不可修改，但是用户可以通过tab切换到该字段，还可以选中复制该字段。可以配合js设置条件控制用户是否可以更改或输入内容

---

### Input标签的step属性

---

> 1.Step规定输入字段的合法数字间隔(如step=”2”,则合法数字可为-2，0，2，4等)
>
> 2.Step属性的值为负数或0时默认为1，该属性可以配合max，min属性来创建合法值得范围。
>
> 3.Step，max，min属性适用于`<input>`类型有:number,range,date,datetime,month,time,week

---

### 表单元素

``` html
<input type="text" name="username" placeholder="请输入用户名" autofocus="autofocus" required="required" 
autocomplete="off" />
```

### form标签的enctype属性

---
> 1.规定在发送表单数据之前如何对其编码，可取值有：
>
> 2.application/x-www-form-urlencoded
>
> 3.multipart/form-data
>
> 4.text/plain
>
> 5.form标签的method属性
>
> 6.规定用于发送表单数据的http方法，可取值有：post和get

---

### video标签，H5新标签

---

> 1.用来定义视频，电影片段或其他视频流
> 2.常用属性：
>
>> + 2.1autoplay(视频就绪后马上播放)
>> + 2.2controls(向用户显示播放控件，如按钮)
>> + 2.3loop(循环播放)
> 3可以为没有controls控件属性的video嵌套按钮控件

---

### alc()的运算规则

---

> 1.calc()使用通用的数***算规则，但是也提供更智能的功能：
>
> 2.使用“+”、“-”、“*” 和 “/”四则运算；
>
> 3.可以使用百分比、px、em、rem等单位；
>
> 4.可以混合使用各种单位进行计算；
>
> 5.表达式中有“+”和“-”时，其前后必须要有空格，如"widht: calc(12%+5em)"这种没有空格的写法是错误的；
>
> 6.表达式中有“*”和“/”时，其前后可以没有空格，但建议留有空格。
---

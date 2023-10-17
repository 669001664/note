##### 1.过滤错误值

- ```js
  const array = [1, 0, undefined, 6, 7, '', false];
  
  array.filter(Boolean);
  // [1, 6, 7]
  ```

##### 2.逻辑运算符

- ```js
  if (a > b) {
      func(a)
  }
  
  a > b && func(a)
  ```

##### 3.判断简化

- ```js
  if(a === 's', || a === 'd' || a === 'c') {
      func(a)
  }
  if (['s', 'd', 'c'].include(a)) {
      func(a)
  }
  ```

##### 4.判断代码性能

- ```js
  const startTime = performance.now(); 
  // 某些程序
  for(let i = 0; i < 1000; i++) {
      console.log(i)
  }
  const endTime = performance.now();
  const totaltime = endTime - startTime;
  console.log(totaltime); // 30.299999952316284
  
  允许网页访问某些函数来测量网页和Web应用程序的性能，包括 Navigation Timing API和高分辨率时间数据。
  
  计算页面总加载时间
  const perfData = window.performance.timing;
  const pageLoadTime = perfData.loadEventEnd - perfData.navigationStart;
  计算请求响应时间
  const connectTime = perfData.responseEnd - perfData.requestStart;
  计算页面渲染时间
  const renderTime = perfData.domComplete - perfData.domLoading;
  
  
  window.onload = function() {
    var timing  = performance.timing;
    console.log('准备新页面时间耗时: ' + timing.fetchStart - timing.navigationStart);
    console.log('redirect 重定向耗时: ' + timing.redirectEnd  - timing.redirectStart);
    console.log('Appcache 耗时: ' + timing.domainLookupStart  - timing.fetchStart);
    console.log('unload 前文档耗时: ' + timing.unloadEventEnd - timing.unloadEventStart);
    console.log('DNS 查询耗时: ' + timing.domainLookupEnd - timing.domainLookupStart);
    console.log('TCP连接耗时: ' + timing.connectEnd - timing.connectStart);
    console.log('request请求耗时: ' + timing.responseEnd - timing.requestStart);
    console.log('白屏时间: ' + timing.responseStart - timing.navigationStart);
    console.log('请求完毕至DOM加载: ' + timing.domInteractive - timing.responseEnd);
    console.log('解释dom树耗时: ' + timing.domComplete - timing.domInteractive);
    console.log('从开始至load总耗时: ' + timing.loadEventEnd - timing.navigationStart);
  }
  performance.memory属性  用于显示当前的内存占用情况；
  console.log(performance.memory);
  /* MemoryInfo {
    totalJSHeapSize: 11735319,
    usedJSHeapSize: 9259919,
    jsHeapSizeLimit: 2197815296
  } */
  usedJSHeapSize表示：JS 对象（包括V8引擎内部对象）占用的内存数
  totalJSHeapSize表示：可使用的内存
  jsHeapSizeLimit表示：内存大小限制
  usedJSHeapSize不能大于totalJSHeapSize，如果大于，有可能出现了内存泄漏。
  ```

##### 5.拼接数组

- ```js
  const start = [1, 2] 
  const end = [5, 6, 7] 
  const numbers = [9, ...start, ...end, 8] // [9, 1, 2, 5, 6, 7 , 8]
  
  
  const start = [1, 2, 3, 4] 
  const end = [5, 6, 7] 
  start.concat(end); // [1, 2, 3, 4, 5, 6, 7]
  
  但是使用concat()方法时，如果需要合并的数组很大，那么concat() 函数会在创建单独的新数组时消耗大量内存。这时可以使用以下方法来实现数组的合并
  Array.prototype.push.apply(start, end)
  
  ```

##### 6.可选连接符

- ```js
  const parent = {
      child: {
        child1: {
          child2: {
            key: 10
        }
      }
    }
  }
  
  parent && parent.child && parent.child.child1 && parent.child.child1.child2
  
  parent?.child?.child1?.child2 // 效果一样 避免某一级不存在报错
  
  const array = [1, 2, 3];
  array?.[5]
  可选链运算符允许我们读取位于连接对象链深处的属性的值，而不必明确验证链中的每个引用是否有效。在引用为空(null 或者 undefined) 的情况下不会引起错误，该表达式短路返回值是 undefined。与函数调用一起使用时，如果给定的函数不存在，则返回 undefined。
  
  ```

##### 7.验证null和undefined

- ```js
  if(a === null || a === undefined) {
      doSomething()
  }
  a ?? doSomething()
  空值合并操作符（??）是一个逻辑操作符，当左侧的操作数为 null 或者 undefined 时，返回其右侧操作数，否则返回左侧操作数
  ```

##### 8.数组元素转换数字

- ```js
  const array = ['12', '1', '3.1415', '-10.01'];
  array.map(Number);  // [12, 1, 3.1415, -10.01]
  
  ```

##### 9.动态声明对象属性

- ```js
  const dynamic = 'color';
  var item = {
      brand: 'Ford',
      [dynamic]: 'Blue'
  }
  console.log(item); 
  // { brand: "Ford", color: "Blue" }
  
  ```

##### 10.数字取整

- ```js
  ~~3.1415926  // 3
  如果是数字类型的字符串，就会转化为纯数字；
  如果字符串包含数字之外的值，就会转化为0；
  如果是布尔类型，true会返回1，false会返回0；
  23.9 | 0   // 23
  -23.9 | 0   // -23
  
  ```

##### 11.检查对象是否为空

- ```js
  Object.keys({}).length  // 0
  Object.keys({key: 1}).length  // 1
  
  ```

##### 12.值转换为布尔值

- ```js
  !!undefined // false
  !!"996"     // true
  !!null      // false
  !!NaN       // false
  ```

##### 13.避免使用eval()和with()

- with() 会在全局范围内插入一个变量。因此，如果另一个变量具有相同的名称，则可能会导致混淆并覆盖该值。
- eval() 是比较昂贵的操作，每次调用它时，脚本引擎都必须将源代码转换为可执行代码。

##### 
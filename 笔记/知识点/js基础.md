##### 1.`JavaScript`规定了几种语言类型

- **基本数据类型**：`string`,`number`,`boolean`,`null`,`undefined`,`symbol`,`bigint(ES2020)`。
  - `BigInt`是一种新的数据类型 用于当整数值大于Number数据类型的支持范围时。这种数据类型允许我们安全的对最大整数执行算术操作，表示高分辨率的时间戳，使用大整数id。要创建`BigInt`，只需要在数字末尾添加n即可。
  - **按值访问，存放在栈中**
- **引用数据类型**：`object`,`Array`,`RegExp`,`Date`,`Function`
  - **按引用访问，存放在堆中**

##### 2.`Symbol`

- Symbol值通过Symbol函数生成，使用typeof，结果为'symbol'

- Symbol函数前不能使用new命令，因为生成的Symbol是基本数据类型不是对象

- instanceof 的结果为false 

- ```js
  var s = Symbol('foo');
  console.log(s instanceof Symbol); // false
  ```

- Symbol函数可以接受一个参数，是对当前Symbol值得描述，相同参数的Symbol返回值是不相等的

- ```js
  var s1 = Symbol('a')
  var s3 = Symbol('a')
  
  log(s1 === s3) false
  ```

- Symbol值可以作为表示符，用作对象的属性名，可以保证不会出现同名属性，Symbol作为属性名，不会被for in 、 for of枚举出，也不能通过Object.Keys()、**Object.getOwnPropertyNames()、**JSON.stringify()返回。 **Object.getOwnPropertySymbols**可以返回所有Symbol属性名。

- ```js
  let s1 = Symbol('a')
  let s2 = Symbol('b')
  let s3 = Symbol('c')
  let obj = {
      a: 'ddd',
      s1: 'dd',
      [s1]: '2323'
  }
  
  obj[s2] = 4
  let obj1 = {}
  Object.defineProperty(obj1, s3, { value: 'ddd' })
  
  
  // for (const item in obj) { //遍历的是键值
  //     console.log(item);
  // }
  // for (const item of obj) { // for of 无法遍历对象  遍历的是值
  //     console.log(item);
  // }
  
  console.log('111', Object.keys(obj));
  console.log('222', Object.getOwnPropertyDescriptor(obj));
  console.log('333', Object.getOwnPropertyNames(obj));
  console.log('444', Object.getPrototypeOf(obj)); // 从子类上获取父类  可以判断一个类是否继承另一个类
  console.log('555', Object.getOwnPropertyDescriptors(obj)); //返回描述对象
  console.log('666', Object.getOwnPropertySymbols(obj));
  
  class Animal {
      constructor(name) {
          this.name = name;
      }
      say() {
          console.log(this.name);
      }
  }
  
  class Cat extends Animal {
      constructor(name) {
          super(name)
      }
  }
  let c = new Cat('miao')
  c.say()
  console.log(Object.getPrototypeOf(Cat)); // 返回父类
  console.log(Object.getPrototypeOf(c)); //示例返回类
  ```

- `Symbol.for`接受一个字符串作为参数，然后再全局搜索是否有这个字符描述的symbol值，如果有则返回，**否则就新建并返回一个以该字符串为名称的 Symbol 值**

- **Symbol.keyFor 方法返回一个已登记的 Symbol 类型值的 key。**

- ```js
  var s1 = Symbol.for("foo");
  console.log(Symbol.keyFor(s1)); // "foo"
  
  var s2 = Symbol("foo");
  console.log(Symbol.keyFor(s2) ); // undefined
  ```

##### 3.`JavaScript`中的变量在内存中的具体存储形式

- JavaScript中的变量分为基本类型和引用类型 基本类型是保存在栈内存中的简单数据段，它们的值都有固定的大小，保存在栈空间，通过按值访问

  引用类型是保存在堆内存中的对象，值大小不固定，栈内存中存放的该对象的访问地址指向堆内存中的对象，JavaScript不允许直接访问堆内存中的位置，因此操作对象时，实际操作对象的引用。

- **在栈内存中的数据发生复制行为时，系统会自动为新的变量分配一个新值，最后这些变量都是相互独立互不影响的**

##### 4.基本类型对应的内置对象，以及他们之间的装箱拆箱操作

- ```js
  读取一个基本类型时，后台会为此类型创建一个对应的基本类型包装对象。在这个基本类型上调用方法，实际上是在包装对象上调用方法，这个包装对象是临时的，只存在于调用的一瞬间，调用结束包装对象销毁
  num.toFixed(1);
  
  // 在后台的具体执行如下：
  
  const c = new Number(12.345);
  
  c.toFixed(1);
  
  c = null;
  
  ```


##### 5.null和undefined的区别

- 
### 2021/8/9

#### npm包管理

`npm install === npm i`

`npm --save === npm -S`	(项目依赖 dependency：运行、发布生产环境) 

`npm --save--dev === npm -D`	(工程构建依赖 devDependency：开发、打包)

#### ajax创建过程

```js
const xhr = new XMLHttpRequest()
xhr.open('Method', 'URL'[, 'flag', 'name', 'password'])
xhr.send()
xhr.onload = () => {} // 注意和onReadyStateChange的区别
```

#### Promise

1. 状态只能由 Pending --> Fulfilled 或者 Pending --> Rejected，且一但发生改变便不可二次修改

2. Promise实例`.then((val)=>{})`中回调接收的参数val来自于传入resolve中的值

3. `Promise.all()`接收一个可以迭代的数据类型(数组)，如果其中有一个Promise实例reject，则整个reject并返回第一个reject的结果

#### 深拷贝

方法一：

```js
function deepClone(target) {
    const map = new Map()
    function clone (target) {
        if (isObject(target)) {
            let cloneTarget = isArray(target) ? [] : {};
            if (map.get(target)) {
                return map.get(target)
            }
            map.set(target,cloneTarget)
            for (const key in target) {
                cloneTarget[key] = clone(target[key]);
            }
            return cloneTarget;
        } else {
            return target;
        }
    }
    return clone(target)
}
```

方法二：

```js
function deepClone(target){
    // 根据类型制造一个新的数组或对象 => 指向一个新的空间
    // 由于数组的typeof也是'object',所以用Array.isArray(obj)
    var new_target = Array.isArray(target) ? [] : {};
    // 首先判断target的类型
    // 普通类型
    if( typeof target != 'object' ){
        // 这里不能直接返回obj,不然就是浅拷贝的性质
        return  new_target = target
    }
    //引用类型
    //数组
    if( target instanceof Array ){
        for(i = 0; i < target.length; i++ ){
            new_target[i] = target[i];
            if(typeof new_target[i] == 'object'){
                deepClone(new_target[i])
            }
        }
    }else{ //对象
        for (let key in target) {
            if (target.hasOwnProperty(key)) {
                // 对象中的数组和对象
                if (typeof target[key] == 'object') {
                    new_target[key] = deepClone(target[key]); 
                }else{//对象中没有引用类型
                    new_target[key] = target[key]
                }  
            }
        }
    }
    return new_target;
}
```

#### 异步加载JS

https://www.cnblogs.com/qiqingfu/p/12404976.html

1. async 为异步加载，在HTML解析阶段并行下载外部的 js 文件，下载完成后暂停 HTML 解析器执行 js 文件。执行完毕后继续 HTML 的解析。

2. defer 为延迟脚本。在 HTML 解析阶段并行下载外部的 js 文件，下载完成后并不会立即执行，而是在 HTML 解析完成后 DOMContentLoaded 事件触发之前执行 js 文件。延迟加载也保证在文档中出现的顺序执行。

#### call和apply

1. 都是`Function.prototype`里的方法

2. 都可以用来代替另一个对象调用一个方法，将一个函数的对象上下文从初始的上下文改变为由thisObj指定的新对象

`call(this, a, b, c)` 在第一个参数之后的，后续所有参数就是传入该函数的值

`apply(this, [a, b, c])` 只接收两个参数。第一个是对象，第二个是数组，这个数组就是该函数的参数

#### 判断数据类型

1. **`typeof`**只能区分**基本类型**，即：`number`、`string`、`undefined`、`boolean`、`object`
   对于`null`、`array`、`function`、`object`来说统一返回 `object`
2. 要想区分对象、数组、函数、单纯使用`typeof`是不行的。在JS中，可以通过**`Object.prototype.toString.call()`**方法，判断某个对象之属于哪种内置类型
   分为`null`、`string`、`boolean`、`number`、`undefined`、`array`、`function`、`object`、`date`、`math`
3. **`Array.isArray()`**判断数组类型
4. **`instanceof`**对象运算符，用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上是。可以用来判断引用数据类型

#### new关键字

```js
function _new(constructor, ...arg) {
  // 创建一个空对象
  var obj = {};
  // 空对象的`__proto__`指向构造函数的`prototype`, 为这个新对象添加属性 
  obj.__proto__ = constructor.prototype; 
  // 构造函数的作用域赋给新对象(this指向实例对象)
  var res = constructor.apply(obj, arg); 
  // 返回新对象.如果没有显式return语句，则返回this(返回实例对象)
  return Object.prototype.toString.call(res) === '[object Object]' ? res : obj; 
}
```

#### 箭头函数不适用情况

- 当想要函数被提升时(箭头函数是匿名的)
- 使用命名函数(箭头函数是匿名的)
- 使用函数作为构造函数时(箭头函数**没有构造函数**)
- 要在函数中使用`this/arguments`时，由于箭头函数本身不具有`this/arguments`，因此它们取决于外部上下文
- 当想在对象字面是以将函数作为**属性**添加并在其中使用对象时，因为咱们无法访问 `this` 即对象本身。






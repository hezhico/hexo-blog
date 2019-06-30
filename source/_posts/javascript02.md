---
title: javascript基础备忘
date: 2019-05-13 21:19:22
tags: javascript基础
---

### 基本数据类型

> javascript 基本数据类型 string number boolean null undefined



```js
  var _toString = Object.prototype.toString;
  function log(value){
    let result = typeof value
    let result1 = _toString.call(value)
    document.body.innerHTML = document.body.innerHTML +"<br>" + 
    "typeof :: " + result + ' || ' + 'toString :: ' + result1
  }
  // 字符串类型
  var str = "abc";
  // 检测类型
  log(str);
  // 数字类型
  var num = 123;
  // 检测类型
  log(num);
  // 布尔类型
  var bool = true;
  log(bool)
  // undefine
  var un = undefined
  var unde; // 只申明未赋值
  log(un)
  log(unde)
  // 空对象
  var isnull = null;
  log(isnull)
  // 特殊数字类型NaN
  var isNaN = Math.pow('2');
  log(isNaN);
```

### 字符串的常规操作方法

1. substring(start, end) 截取制定索引的字符串
2. split() 按照指定的标识符将字符分割成数组
3. indexOf() 寻找指定字符串的索引，未匹配到返回-1
4. replace()
5. String() 将指定目标转化成字符串
```
  3.toSring() // 程序报错
```

### 数组的常用方法
1. forEach
2. sort
3. map
4. shift  unshift
5. pop    push
6. concat
7. Array.from()

8. 数组的去重
```js
  new Set([1,12,3,3])  // => Set(3) {1, 12, 3}
```

9. 剩余参数
```js
  function arg(one, ...args){
    // ...args   => [2,3]
  }
  arg(1, 2,3)
```



### 对象的常用方法
1. 对象的浅拷贝 Object.assign()
2. Object.keys() Object.value() Object.entires()
3. 对象的解构赋值 const { name } = {name:hezhi, age: 18}
4. 对象的深拷贝

```js
  function deepclone(obj) {
    let temp;
    if(typeof obj === "sting" ) {
      return obj
    }

    if(Object.prototype.toString(obj) === "object Object"){
      for(var key in object){
        if(Object.hasOwnproperty(key)){
          if(typeof obj === "object") {
            temp  = deepclone(key)
          }else {
            temp = key
          }
        }
      }
    }

    return temp;
  }
```

5. 正则对象

```js
  // 动态正则
  let ranNum = Matn.random()*10
  let reg = new RegExp(`\^\\d${ranNum}\$`)
  // 使用正则对象实例化的特殊字符需要转译
```


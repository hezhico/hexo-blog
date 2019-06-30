---
title: javascript设计模式之策略模式--表单验证
date: 2019-05-10 00:04:13
tags: 
---

策略模式--表单验证目的是为了简化表单验证的if嵌套，便于阅读理解

### 定义验证规则策略

```js
    class Strategy {

      isNull(value, msg) {
        if(!!!value){
          return msg
        }
      }

      maxValue(value, target, msg) {
        if(value > target) {
          return msg
        }
      }

    }

```

### 定义表单构造器

```js
    class Validtor {
      constructor(strategies) {
        this.cache = []
        this.strategies = strategies;
      }
      //添加验证规则
      add(value,rules, errorMsg) {
        if(typeOf rule === "string") {
          const ary = rules.split(':'); // 把 strategy 和参数分开
          _this.cache.push(() => { // 把校验的步骤用空函数包装起来，并且放入 cache
          const strategy = ary.shift();// 用户挑选的 strategy
          ary.unshift(value); // 把 input 的 value 添加进参数列表
          ary.push(errorMsg); // 把 errorMsg 添加进参数列表
          return _this.strategies[strategy].apply(null, ary);
          });
        }else if(Object.prototype.toString.call(rule) === '[object Array]') {
            let _this = this;
            for (let index = 0; index < rule.length; index += 1) {
              (function (rules) {
                const ary = rules.strategyname.split(':'); // 把 strategy 和参数分开
                _this.cache.push(() => { // 把校验的步骤用空函数包装起来，并且放入 cache
                const strategy = ary.shift();// 用户挑选的 strategy
                ary.unshift(value); // 把 input 的 value 添加进参数列表
                ary.push(rules.errorMsg); // 把 errorMsg 添加进参数列表
                return _this.strategies[strategy].apply(null, ary);
                });
              }(rule[index]));
              console.log(this.cache)
            } 
        }else {
            throw('rule type is valid');
        }
      }
    }
    // 开始验证
    start() {
      for(let i = 0, i< this.cache.length, i++){
        var msg = this.cache[i];
        if(msg){
          console.log("表单验证失败");
          return msg;
        } else {
          console.log("表单验证成功")
        }
      }
    }

```






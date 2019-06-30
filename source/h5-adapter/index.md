---
title: h5-adapter
date: 2019-05-02 20:34:04
---
主要是对工作中遇到的适配问题做一个备注
<!-- more -->

### 1. 手机号码在ios自动显示蓝色

```html
   // head标签中添加如下代码
  <meta name = "format-detection" content = "telephone=no">
```

### 2. 去掉点击链接和文本框对象时默认的灰色半透明覆盖层(iOS)或者虚框(Android)

```css
  -webkit-tap-highlight-color:rgba(0,0,0,0); //透明度设置为0，
```

### 3. ios input 聚焦文本框 光标过大

```css
    input {
      font-size: 14px;
      height: 40px;
      line-height: 40px;
    }

    Android 光标 14px   ios 光标 40px

    文本框内容上下居中，不要使用line-height
```

### 4. ios 滚动不流畅 ，部分机型弹窗无法滚动

```css
  over-flow: auto;     /* winphone8和android4+ */
  -webkit-overflow-scrolling: touch;    /* ios5+ */
```

### 5. ios文本框聚焦 fixed定位的banner错位

```js
  // 针对需要做特殊处理的 设置自定义属性 ios='focus'
  let iosList = document.querySelectorAll("input[ios='focus']")
  // Array.from(iosList)
  Array.from(iosList).onfocus = () => {
    document.getElementsByTagName('html')[0].setAttribute("class" , 'ios')
  }
  Array.from(iosList).onblur = () => {
    document.getElementsByTagName('html')[0].removeAttribute("class" , 'ios')
  }

  // 实例
  .header {
    width: 100%;
    heigth: 50px;
    position: fixed;
  }

  .ios .header{
    position: absolute
   }

```

### 6. ios x 底部黑线适配

> 真机测试只有 env(safe-area-inset-bottom)有效果 ，safe-area-inset-bottom底部安全距离


```html
   <meta name="viewport" content="width=device-width, initial-scale=1.0,viewport-fit=cover">
   <div class="footer">
    <div>我的</div>
    <div>我的首页</div>
    <div>个人中心</div>
  </div>
```

```css
   *{
      padding: 0;
      margin: 0;
    }
    html,body {
      height: 100%;
      position: relative;
      box-sizing: border-box;
    }
    .footer {
      display: flex;
      position: fixed;
      bottom: 0;
      width: 100%;
      background: #000;
      /* height: 60px; */
      /* height: calc(60px + constant(safe-area-inset-bottom,40px)); */
      padding-bottom: constant(safe-area-inset-bottom);  /* ios 小于 11.2 */
      padding-bottom: env(safe-area-inset-bottom);
      /* line-height: 60px; */
      border: 5px solid lightblue;
    }

    .footer div {
      flex: 1;
      color: lightblue;
    }
```

### 7. 用户系统字体调大，导致ui异常

#### 方案一 通过js脚本获取html的实际字体大小，与通过rem计算得到的字体大小比较， 计算用户调大系统字体，页面实际字体放大的倍数，从而叫rem计算的结果缩小对应的倍数

#### 方案二 减少rem的使用

#### 方案三 通过客户端提供方法强行阻止字体的放大(未实践)

### 8. ios h5跳转白屏的问题（spa）

```js
// 1. a页面 .../index.html#/
// 2. b页面 .../index.html#/bname

// 当b页面回跳a页面, replace.href 跳转方式
window.location.replace('.../index.html#/bname') // ios白屏
window.location.href = '.../index.html#/bname' // ios白屏
/*
* 单页应用跳转方式使用路由，尽量别使用location
*/
```












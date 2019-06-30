---
title: vue实战
date: 2019-05-13 21:39:35
tags:
---

### 1. vue history模式实践

```js
  location ~* /h5bill { 
   access_log  /opt/nginx-1.4.7/logs/h5bill/h5bill.log; 
    alias  /opt/nginx-1.4.7/html/ued/h5bill; 
     try_files $uri $uri /h5bill/static/index.html; 
  }

  ## 前端路径修改

  1. 设置根目录 index.html
  <base href="/h5bill/">
```

### 2. 表单的封装 左中右

```html
  <template>
    <div class="sp-ipt singleLineBottom">
        <label class="sp-ipt-title">{{iptTitle}}</label>
        <input  v-model.trim="value" 
          @focus="isfocus = true"
          @blur="isfocus = false"
          @input="$emit('input', $event.target.value)"
          ref="ipt"
          autocomplete="off" :placeholder='placeholder' :type="type" class="sp-ipt"> 
        <span class="sp-icon" >
            <svg class="arrow" v-if="isfocus&&value.length" @click="focus"><use xlink:href="#close1"></use></svg>
        </span>
        <slot name="code"></slot>
    </div>
  </template>
```

```js
  export default {
    props: {
      iptTitle: {
        default: '账号',
      },
      placeholder: {
        default: '请输入登录账号',
      },
      value: {
        default: '',
      },
      type: {
        default: 'text',
      },
    },
    data() {
      return {
        isfocus: false,
      };
    },
    methods: {
      focus() {
        this.value = '';
        this.$refs.ipt.focus();
      },
    },
  };
```

```css
    .sp-ipt {
      height: 1.45rem;
      display: flex;
      align-items: center;

      .sp-ipt-title {
        width: auto;
        display: flex;
        min-width: 70px;
      }

      .sp-ipt {
        flex-grow: 1;
      }

      .sp-icon {
        width: auto;
        height: 100%;
        min-width: 30px;
        display: flex;
      }
    }

    .vcode .sp-ipt {
      width: 100px;
    }

```

### 3. 路由切换，新的页面需要回到页面顶部

```js
  
  1. window.scrollTo(0,0)
   // 这个功能只在支持 history.pushState 的浏览器中可用。
  2. 路由的滚动行为
  scrollBehavior (to, from, savedPosition) {
    return { x: 0, y: 0 }
  }
```

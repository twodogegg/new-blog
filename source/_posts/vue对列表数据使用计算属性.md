---
title: vue对列表数据使用计算属性
date: 2021-03-28 11:01:34
description: vue 在 v-for 里面使用 compute 计算属性来渲染所需的数据
tags:
  - vue
categories:
  - 前端
---


## 痛点

在 `vue` 里面中，通常计算属性都使用在单个值上面，对于列表的显示，通常都会在请求完成了以后对数据进行再赋值例如下面的例子

```javascript
let list = [
    {
        id: 3,
        status: 2,
    },
];
var status_arr = ["待付款", "待发货", "待收货"];
this.list = list.map(item => {
    item["statusText"] = status_arr[item.status];
    return item;
});
```

这样也能实现我们的效果，不过这样带来的问题也是很明显的。主要体现在以下几个方面：

1. 代码执照划分不清晰，这里应该是用来请求和获取数据的部分，不应该处理业务逻辑
2. 变量定位不明确，当页面上出现 `item.statusText` 使用的时候第一反应，当然是查接口怎么返回的，结果发现他是前端自己处理的。当需要处理的数据字段变多的时候定位是前端处理还是后台处理是一件麻烦的事
3. 代码臃肿,以我们公司的订单列表为例。请求的代码也就几行，但是处理渲染结果的代码占了80多行，需要渲染的数据全部都放到这里处理挺不合理的，和第一点说的有点像

## 解决办法

### 1、对需要渲染的数据，进行单个计算和显示

优点：
全部解决上诉问题：
1. 代码不再有请求的地方处理，拆分到了计算属性
2. 通过类似于方法的什么，直接定位到修改的位置。
3. 每个变量的修改都是单独的，不同变量有不同的计算属性
缺点：
1. 数据量过大的话可能会有性能问题，每次列表数据变动都会全部重新计算，适用于分页加载或者数据量不是特别大的场景


### 2、对列表定义一个新的计算属性，在计算属性中来处理业务的渲染

优点：
解决上诉问题：
1. 代码不再有请求的地方处理，拆分到了计算属性
缺点：

1. 还是无法区分是接口数据还是自己定义的，需要到计算属性里去看
2. 数据量过大的话可能会有性能问题，每次列表数据变动都会全部重新计算，适用于分页加载或者数据量不是特别大的场景
3. 如果需要处理的字段比较多代码就比较长

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      [v-cloak] {
        display: none;
      }
    </style>
  </head>
  <body>
    <div id="app">
      <div v-cloak>
        用计算属性取得单个变量对应的值
        <ul>
          <li v-for="item in list" :index="item.id">
            订单状态：{{statusText(item.status)}}
          </li>
        </ul>
        用计算属性取得整个列表对应的值
        <ul>
          <li v-for="item in mList" :index="item.id">
            订单状态：{{item.statusText}}
          </li>
        </ul>
      </div>
    </div>

    <!-- <script src="./js//vue/vue.min.js"></script> -->
    <script src="https://unpkg.com/vue/dist/vue.js"></script>

    <script>
      window.onload = function () {
        var status_arr = ["待付款", "待发货", "待收货"];
      var app = new Vue({
        el: "#app",
        data() {
          return {
            list: [
              {
                id: 1,
                status: 0,
              },
              {
                id: 2,
                status: 1,
              },
            ],
          };
        },
        computed: {
          statusText() {
            return (status) => {
              console.log("运行了单个计算属性");
              return status_arr[status];
            };
          },
          mList() {
            return this.list.map((item) => {
              console.log("运行了列表计算属性");
              item["statusText"] = status_arr[item.status];
              return item;
            });
          },
        },
        created() {
          setTimeout(() => {
            this.list.push({
              id: 3,
              status: 2,
            });
          });

          let list = [
            {
              id: 3,
              status: 2,
            },
          ];
          var status_arr = ["待付款", "待发货", "待收货"];
          this.list = list.map(item => {
            item["statusText"] = status_arr[item.status];
            return item;
          });

        },
      });
      }
    </script>
  </body>
</html>

```

## 在线示例

[链接地址](https://codepen.io/twodogegg/pen/QWdEKvZ)



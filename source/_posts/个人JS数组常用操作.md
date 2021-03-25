---
title: 个人JS数组常用操作
date: 2021-03-25 23:17:58
tags: 数组
---

## 1、filter

对数组的每一项运行指定的函数，返回结果为 `true` 的数组

> 当前选中的列表

```javascript
let list = [
  {
    id: 1,
    checked: false,
  },
  {
    id: 2,
    checked: true,
  },
];

let checkedList = list.filter((item) => item.checked);
// [{"id":2,"checked":true}]
```

## 2、find

传入一个回调函数，找到数组中符合当前搜索规则的第一个元素，返回它，终止搜索。

> 根据 id 查找数组中匹配的元素，返回该元素

```javascript
let list2 = [
  {
    id: 1,
    checked: false,
  },
  {
    id: 2,
    checked: true,
  },
];

let res = list2.find((item) => item.id === 2);
// {"id":2,"checked":true}
```

## 3、findIndex

传入一个回调函数，找到数组中符合当前搜索规则的第一个元素，返回它的下标，终止搜索。

> 根据 id 查找数组中匹配的元素，返回下标

```javascript
let list3 = [
  {
    id: 1,
    checked: false,
  },
  {
    id: 2,
    checked: true,
  },
];

let res = list3.find((item) => item.id === 2);
// 1
```

## 4、concat()

连接两个或多个数组，返回一个新的数组，不会改变原来的数组

> 应用场景，加载更多

```javascript
let list4 = [
  {
    id: 1,
    checked: false,
  },
];
let data = [
  {
    id: 2,
    checked: false,
  },
];

list4 = list4.concat(data);
// [{"id":1,"checked":false},{"id":2,"checked":false}]
```

## 5、map

对数组的每一项都运行给定的函数，返回每次函数调用的结果组成一个新数组

> 应用场景示例：给数组添加一个 checked 属性，方便 vue 组件使用 v-model

```javascript
let list6 = [
    {
        id: 1,
    },
    {
        id: 2,
    }
]

list6 = list6.map(item => {
    item.checked = false;
    return item;
})

// [{"id":1,"checked":false},{"id":2,"checked":false}]
```



## 6、join

join() 方法用于把数组中的所有元素放入一个字符串。元素是通过指定的分隔符进行分隔的，默认使用','号分割，不改变原数组。

> 应用场景，配合 filter 和 map 逗号分隔数组拼接 id，将选中的元素，用逗号分隔，拼接成字符串发送给后台

```javascript
let list5 = [
  {
    id: 1,
    checked: false,
  },
  {
    id: 2,
    checked: true,
  },
  {
    id: 3,
    checked: true,
  },
];

let ids = list5.filter((item) => item.checked)
    .map((item) => item.id).join(",");

// 2,3
```

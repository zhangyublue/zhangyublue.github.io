---
layout:        post
title:         "彻底整理一次splice、split、slice相关用法"
menutitle:     "彻底整理一次splice、split、slice相关用法"
date:          2020-06-04
category:      JavaScript
author:        张于蓝
cover:         /assets/cover1.jpg
redirect_from:
comments:      false
published:     true
---
# splice、split、slice
工作中经常会用到的api，虽然很简单，但是有时还是会傻傻分不清楚，每次用每次查，查了用用了忘。效率很低下，于是下定决心一次性彻底的弄清楚这些api的用法，及参数的含义。
## splice
- 中文意思为v：绞接，捻接(两段绳子)；胶接，粘接(胶片、磁带等)； n：胶接处；粘接处；绞接处。
- 作用：用于处理数组，「添加」，「替换」，「删除」。
- 参数：array.splice(start, deleteCount, item1, item2, ...); 
    - start：指定修改的位置（从0开始）。如果超出了数组的长度，则从数组末尾开始添加内容。如果是负值，则表示从数组末尾开始的第几位（意味着-n是倒数第n个元素并等价于array.length - n），如果负值的绝对值大于数组的长度，则表示开始位置为0；
    
    ```javascript
    // start超出数组长度
    let a = [];
    a.splice(2, 0, 1);
    console.log(a); // [1]
    ```
    ```javascript
    // start 是负值
    let a = [1,2,3,4,5,6];
    a.splice(-2, 2, "zzz", "xxxx");
    console.warn(a); // [1, 2, 3, 4, "zzz", "xxxx"]
    ```
    ```javascript
    // start 是负值且绝对值大于数组长度
    let a = [1,2,3,4,5,6];
    a.splice(-8, 2, "zzz", "xxxx");
    console.warn(a); // ["zzz", "xxxx", 3, 4, 5, 6]
    ```
    - deleteCount(可选)：整数表示，要移除数组元素的个数。如果deleteCoutnt大于start之后的元素的总数。则从start后（包括start位）之后的元素都会被删除。如果deleteCount被省略了，那么start之后数组的所有元素也都会被删除。如果deleteCount为0或者负数，则不移除元素。
    
    ```javascript
    // deleteCount被省略
    let a = [1,2,3,4,5,6];
    a.splice(2);
    console.warn(a); // [1, 2]
    ```
    - item1，item2...（可选）：要添加进数组的元素，如果不指定，则splice只删除元素。
### splice的返回值
由被删除的元素组成的数组，如果没有删除元素，则返回空数组。

### splice的用法

1. 添加  从第 2 位开始删除 0 个元素，插入"drum"

```javascript
let myFish = ["angel", "clown", "mandarin", "sturgeon"];
let removed = myFish.splice(2, 0, "drum");
```

2. 删除

- 从第 3 位开始删除 1 个元素

```javascript
let myFish = ['angel', 'clown', 'drum', 'mandarin', 'sturgeon'];
let removed = myFish.splice(3, 1);

// 运算后的 myFish: ["angel", "clown", "drum", "sturgeon"]
// 被删除的元素: ["mandarin"]
```
- 从第 2 位开始删除 2 个元素，插入“trumpet”

```javascript
var myFish = ['angel', 'clown', 'drum', 'sturgeon'];
var removed = myFish.splice(2, 1, "trumpet");

// 运算后的 myFish: ["angel", "clown", "trumpet"]
// 被删除的元素: ["drum", "sturgeon"]
```

3. 替换 替换就是deleteCount为添加的item1，item2...的长度，其实是删除了item相同长度的元素然后插入了item1，item2...效果就等同于替换了

```javascript
var myFish = ['angel', 'clown', 'drum', 'sturgeon'];
var removed = myFish.splice(2, 1, "trumpet");

// 运算后的 myFish: ["angel", "clown", "trumpet", "sturgeon"]
// 被删除的元素: ["drum"]

```
### 小结
彻底整理一波splice发现远远简单于之前所想的，在这次整理后，以后工作用到将会更加的有效率，这次整理很值！
## split

- 中文意思为v：分裂，使分裂(成不同的派别)；分开，使分开(成为几个部分)；分担；分摊；分享； n：分歧；分裂；分离；划分；分别；份额；裂缝；
- 作用：用于处理字符串，把字符串分割成字符串数组。
- 参数：str.split(separator， limit)；
    - separator：指定每个应拆分的字符串。separator也可以是正则表达式。如果省略separator，则会返回一个由整个字符串组成的数组。如果separator为空字符串，则将str所有字符串分隔，并返回。
    
    ```javascript
    // 省略separator
    let str = 'string';
    let result = str.split();
    console.warn(result); // ['string'];
    ```
    
    ```javascript
    // separator为空字符串
    let str = 'string';
    let result = str.split('');
    console.warn(result); // ['s', 't', 'r', 'i', 'n', 'g']
    ```
    - limit：一个整数，限定了返回分隔片段的数量。
### split返回值
返回源字符串以分隔符出现位置分隔而成的一个 Array 。
### split的用法

    





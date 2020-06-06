---
layout:        post
title:         "你真的懂splice、split、slice？"
menutitle:     "你真的懂splice、split、slice？"
date:          2020-06-04
category:      JavaScript
author:        张于蓝
cover:         /assets/cover1.jpg
redirect_from:
comments:      false
published:     true
---
# 你真的懂splice、split、slice？
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

- 添加  从第 2 位开始删除 0 个元素，插入"drum"

```javascript
let myFish = ["angel", "clown", "mandarin", "sturgeon"];
let removed = myFish.splice(2, 0, "drum");
```

- 删除

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

- 替换 替换就是deleteCount为添加的item1，item2...的长度，其实是删除了item相同长度的元素然后插入了item1，item2...效果就等同于替换了

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
    console.warn(result);// ['s', 't', 'r', 'i', 'n', 'g']
    ```
    - limit：一个整数，限定了返回分隔片段的数量。
### split返回值
返回源字符串以分隔符出现位置分隔而成的一个 Array 。

### split的用法
- 分隔字符串(不包括分隔字符)

```javascript
const a = 'dbdfsafdsafdsfds';
const b = a.split('d');
console.warn(b); //  ["", "b", "fsaf", "saf", "sf", "s"]
```

- 使用正则来匹配分隔字符串

```javascript
const a = "Hello 1 word. Sentence number 2."
const b = a.split(/\d/);
console.warn(b); // ["Hello ", " word. Sentence number ", "."]
```

- 保留分隔字符串 如果 separator 包含捕获括号，则其匹配结果会保留在返回数组中

```javascript
const a = "Hello 1 word. Sentence number 2."
const b = a.split(/(\d)/);
console.warn(b); // ["Hello ", "1", " word. Sentence number ", "2", "."]
```

- 限制返回值的数组长度

```javascript
const a = "Hello World. How are you doing?";
const b = myString.split(" ", 3);
console.log(b); // ["Hello", "World.", "How"]
```

- 使用数组作为分隔符

```javascript
const a = 'ca,bc,a,bca,bca,bc';
const b = a.split(['a','b']); 
// a.split(['a','b']) 就等于 a.split(String(['a','b'])) 等于 a.split('a,b');
console.warn(b); // ["c", "c,", "c", "c", "c"]
```

### 小结
令我万万没想到的是，split出人意料的花样很多，限制返回值数组的长度，以及正则匹配分隔符，保留分隔符，数组作为分隔符，都是工作中不曾用到的。这些运用得当，可以领工作更有效率，代码更为优雅。

## slice
- 中文意思为 v：把…切成(薄)片；切；割；划；削(球)；斜切打； n：部分；(切下的食物)薄片，片；份额；锅铲；(餐桌用)小铲；
- 作用：用于在数组中获取某部分，并且不改变原数组。
- 参数：array.slice(begin, end);
    - begin（可选）：1）提取起始处的索引（从0开始）；2）如果begin大于数组的长度，则返回空数组；3）如果该参数为负值如-n，则表示从该数组的倒数第n个数开始；4）如果该参数为负值且负值的绝对值大于数组的长度，则表示从0开始;
    - end（可选）：1）提取终止出的索引（从0开始），在该索引出停止提取元素。会提取数组中索引从begin开始到end结束的所有元素。（```包含begin，但不包含end```）；2）如果该参数为负值如-n，则表示从该数组的倒数第n个数开始；3）如果end被省略，则 slice 会一直提取到末尾；4)如果 end 大于数组的长度，slice 也会一直提取到数组的末尾；
    
### slice的返回值

一个含有被提取元素的新数组，且不改变原数组。

- 引用对象仅为浅拷贝。如果该元素是个对象引用 （不是实际的对象），slice 会拷贝这个对象引用到新的数组里。两个对象引用都引用了同一个对象。如果被引用的对象发生改变，则新的和原来的数组中的这个元素也会发生改变。

- 基础数据类型。对于字符串、数字及布尔值来说（不是 String、Number 或者 Boolean 对象），slice 会拷贝这些值到新的数组里。在别的数组里修改这些字符串或数字或是布尔值，将不会影响另一个数组。

### slice的用法
-  正常提取元素

```javascript
const a = [0, 1, 2, 3, 4, 5];
const b = a.slice(2, 5);
console.warn(b); // [2, 3, 4]
```

- MDN上未提及的如果end在数组中指针在begin之前的情况

```javascript
// 结果显示返回空数组
const a = [0, 1, 2, 3, 4, 5, 6];
const b = a.slice(5, 2);
console.warn(b); // []
```

- 转化类数组对象（Array-like）为数组

```javascript
function list() {
  return Array.prototype.slice.call(arguments);
}

const a = list(1, 2, 3); 
console.warn(a); // [1, 2, 3]
```

看到这里我又想起了另外一些类数组，比如```document.getElementsByXXX系列```那赶紧试一把。

```javascript
// 首先随便打开个网页，打开控制台
const a = document.getElementsByTagName('div');
function list(params) {
  return Array.prototype.slice.call(params);
}
a.forEach(item => {console.warn('是数组了')})
// Uncaught TypeError: a.forEach is not a function at <anonymous>:1:3
// 不出所料报错了，还不是数组
// slice 处理下
const b = list(a);
b.forEach(() => { console.warn('是数组了') }); // 110 是数组，在遍历了
```
这也太酷了吧，马不停蹄赶紧查下还有哪些(Array-like)；查过网上资料之后发现常见的类数组对象也就是arguments对象以及上面的那种DOM对象

### 小结
上文未提及String.prototype.slice(),用法与Array的slice大同小异，甚至可以看做为string.split('').slice().join()；
slice也同样给我带来了惊喜，让我了解到了类数组的概念，之前一直只是有个模糊的映象，现在更为具体生动。



    





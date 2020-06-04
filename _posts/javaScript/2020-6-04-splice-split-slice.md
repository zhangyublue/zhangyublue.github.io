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
- 

1. 添加
从第2位开始删除0个元素，插入"drum"
```javascript
let myFish = ["angel", "clown", "mandarin", "sturgeon"];
let removed = myFish.splice(2, 0, "drum");
```
    





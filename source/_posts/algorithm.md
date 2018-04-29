---
title: algorithm
tags: tags
date: 2018-04-29 10:37:33
---
### 排序
- 冒泡排序
每次比较两个相邻的元素，错误就交换，每一趟只能确定一个数归位，n个数需要n-1趟
时间复杂度O(n²)
```javascript
// 升序
const oriArr = [12, 35, 99, 18, 5]
const length  = oriArr.length
function bubbleSort(arr) {
  oriArr.forEach(() => {
    for (let i = 0; i < length - 1; i++) {
      let curItem = oriArr[i]
      let compareItem = oriArr[i + 1]
      if (curItem > compareItem) {
        [oriArr[i], oriArr[i + 1]] = [compareItem, curItem] // exchange
      }
    }  
  })
}
bubbleSort(oriArr)
```

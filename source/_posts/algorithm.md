---
title: algorithm
tags: algorithm
date: 2018-04-29 10:37:33
---
### 排序
- 冒泡排序
每次比较两个相邻的元素，错误就交换，每一趟只能确定一个数归位，n个数需要n-1趟
时间复杂度O(n²)
```javascript
// 升序
const oriArr = [12, 35, 99, 18, 5]
const length = oriArr.length;
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
<!-- more -->
- 快速排序
选取基准数，将大于基准数的放在右边，小于基准数的放在左边，每趟将这一轮的基准数归位
对左右区间重复操作，直到各区间只剩一个数
```javascript

const oriArr = [6, 1, 2, 7, 9, 3, 4, 5, 10, 8]
function quickSort(quickArr, left, right) {
  console.log('start', left, right)
  let base = quickArr[left]
  let baseIndex = left
  let i = left
  let j = right
  if (i >= j) {
    console.log('ending', quickArr)
    return
  }
  while(i < j) {
    while(i < j && quickArr[j] >= base) {
      j-- // forward
    }
    [quickArr[j], quickArr[baseIndex]] = [base, quickArr[j]]
    baseIndex = j
    console.log('after exchange', quickArr)
    while (i < j && quickArr[i] <= base) {
      i++
    }
    [quickArr[i], quickArr[baseIndex]] = [base, quickArr[i]]
    baseIndex = i
    console.log('after exchange', quickArr)
  }
  quickSort(quickArr, left, baseIndex -1)
  quickSort(quickArr, baseIndex + 1, right)
}
quickSort(oriArr, 0, oriArr.length - 1)
```
### 队列 FIFO
```javascript
// 删除第一个元素，将下一个元素插入队尾，按照删除顺序打印数组
const oriArr = [6, 3, 1, 7, 5, 8, 9, 2, 4]
let res = []
function queue(arr) {
for (let i = 0; i < oriArr.length; i++){
  let length = arr.length
  res.push(arr[0])
  if (length > 1) {
    arr = [...arr, arr[1]]
    let [arr0, arr1, ...rest] = arr
    arr = rest
  }
}
}
queue(oriArr) // res: [6, 1, 5, 9, 4, 7, 2, 8, 3]
```

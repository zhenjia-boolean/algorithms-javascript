
## 插入排序

### 1. 算法说明

插入排序是一种对于少量元素排序非常有效的排序算法，在日常生活中最常见的例子就是插入扑克牌，我们总是喜欢将某张扑克牌插入到已排序的扑克中。

![插入排序](https://raw.githubusercontent.com/ziyi2/algorithms-javascript/master/img/algorithms-base/insert-sort.gif)


[插入排序](https://github.com/ziyi2/algorithms-javascript/blob/master/src/algorithms-base/insertion-sort.js)的实现过程如上图所示，`javascript`实现如下：

``` javascript
function insertionSort(arr) {
  let array = [...arr] 
  let key, i
  for(let j = 1; j <= array.length - 1; ++j) {
    // 希望排序的数也称为关键词
    key = array[j]
    i = j - 1
    // 待插入的数据小于当前数据，则当前数据往后移
    while(i >= 0 && array[i] > key) {
      array[i + 1] = array[i]
      -- i
    }
    // 将待插入数据插入合适位置
    array[i + 1] = key
  }
  return array
}
```


### 2. 算法证明

> 在`for`循环的每次迭代开始时，元素`array[0]~array[j-1]`始终是原数组的元素，且是一个排序好的子数组。以`[6,5,3,1,8,7,2,4]`为例，第一次循环默认`[6]`就是已经排序好的子数组，那么第二次循环`[5,6]`就是已经排序好的子数组，我们称这样的子数组为**循环不变式**。

**循环不变式**可以帮助理解算法的正确性。关于**循环不变式**必须证明三条性质：

- **初始化**：循环的第一次迭代之前，它为真。
- **保持**：循环的某次迭代之前它为真，那么下次迭代之前它仍然为真。
- **终止**：在循环终止时，不变式有助于证明算法的正确性。

以`[6,5,3,1,8,7,2,4]`应用于插入排序证明该排序的正确性：

- **初始化**：当`j=1`时，**循环不变式**为`array[0]~array[1-0]`，即第一次迭代之前的**循环不变式**为原数组的`[6]`，在子数组只有一个元素的前提下，该元素默认可以归为已经排序好的元素，表明第一次迭代之前**循环不变式**成立。
- **保持**：非形式化的，插入第`j`个元素，将`array[j-1]`、`array[j-2]`、`array[j-3]`等向右移动一个位置，直到找到`array[j]`的合适位置进行插入操作。首先，移动后的`arrary[0]~array[j]`仍然是移动前的元素`array[0]~array[j]`，只是元素的位置发生了变化。其次，此前`array[0]~array[j-1]`是一个排序好的数组，那么`array[0]~array[j]`仍然是一个排序好的数组。因此，下一次循环迭代增加`j`**循环不变式**仍然保持不变。
- **终止**：在循环终止时，由`j<=array.length-1`可以确定终止条件为`j=array.length`，此时说明数组`array[0]~array[array.length-1]`是原来数组的所有元素，且已经按序排列，因此算法正确。


### 3. 小结

主要讲解一个算法设计与分析的框架：说明**插入排序**算法，证明该算法能正确的排序。


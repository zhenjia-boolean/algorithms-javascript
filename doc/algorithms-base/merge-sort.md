## 归并排序

[插入排序](https://github.com/ziyi2/algorithms-javascript/blob/master/doc/%E7%AE%97%E6%B3%95%E5%9F%BA%E7%A1%80/%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F.md)采用的是**增量**方法解决排序问题（将待排序的数插入到已排序好的数组中），**归并排序**则采用**分治法**设计，**分治法**的优点是最坏运行时间比**插入排序**要少得多，同时该方法更容易确定算法的运行时间。

### 1. 分治法

将原问题分解为几个规模较小但类似于原问题的子问题，递归地求解这些子问题，最终合并这些子问题的解来建立原问题的解。分治法在每层递归时都有三个步骤：
- **分解**：分解原问题为若干个子问题，这些子问题是原问题规模较小的一个实例。
- **解决**：递归求解这些子问题。如果问题的规模足够小，则直接求解。
- **合并**：合并子问题的解成原问题的解。

### 2. 算法说明

**归并排序**采用**分治法**进行设计，因此也有三个步骤：
- **分解**：将$n$个待排序的元素组成的数组分解成各具$n \over 2$个元素的两个子数组（左右子数组）。
- **解决**：使用归并排序递归的排序左右两个子数组。
- **合并**：合并两个已排序的子数组以产生排序后的数组。

![插入排序](https://raw.githubusercontent.com/ziyi2/algorithms-javascript/master/img/algorithms-base/merge-sort_1.gif)


排序左右子数组的`javascript`实现如下：

``` javascript
function merge(arr, leftStart, leftEnd, rightEnd) {
  // 计算左子数组的长度
  let leftNum = leftEnd - leftStart + 1,
      // 计算右子数组的长度
      rightNum = rightEnd - leftEnd,
      lefts = [],
      rights = [],
      i,j
	
  // 赋值左子数组	
  for(i=0; i<leftNum; i++) {
    lefts[i] = arr[leftStart+i]
  }
  
  // 赋值右子数组
  for(j=0; j<rightNum; j++) {
    rights[j] = arr[leftEnd+1+j]
  }

  // 哨兵值，一旦只剩下哨兵值则表明当前数组中的元素已经排序完成
  lefts[i++] = Infinity
  rights[j++] = Infinity

  i = 0
  j = 0

  // 将左右子数组中的元素按从小到大重新插入数组arr
   for(let k=leftStart; k<=rightEnd; k++) {
    arr[k] = lefts[i] <= rights[j] ? lefts[i++] : rights[j++]
  }
}
```
> 在左右子数组（前提是已经排好序）末尾各加入了一个$\infty$值，用于简化代码，一旦某个数组中的元素全部排序完毕，那么通过该$\infty$值的判断（未排序完毕数组中的剩余元素始终小于无穷大$\infty$）从而可以将未排序完的元素全部插入已排序元素的末尾。

[归并排序](https://github.com/ziyi2/algorithms-javascript/blob/master/src/algorithms-base/merge-sort.js)的`javascript`实现如下：

```javascript
function mergeSort(arr, start, end) {
  // start>=end则说明数组中只剩下一个元素，单个元素默认排好序，不要进行merge排序
  if(start < end) {
    let division = Math.floor((start + end)/2)
    mergeSort(arr, start, division)
    mergeSort(arr, division + 1, end)
    merge(arr, start, division, end)
  }
}
```

例如该算法要对数组`[38,27,43,3,9,82,10]`进行排序，首先会分解成一个个单独的元素，默认单独元素排好顺序，然后不断地进行合并排序`merge`，直至整个序列排好顺序。

![插入排序](https://raw.githubusercontent.com/ziyi2/algorithms-javascript/master/img/algorithms-base/merge-sort_2.png)


### 3. 分析算法

#### 3.1 分治算法的分析

分治算法的运行时间计算依据于分治法的三个步骤：**分解**、**解决**和**合并**，将三个步骤的运行时间相加即为分治算法的总运行时间。当算法包含其自身调用的时候，例如上面的`mergeSort`函数，可以使用**递归方程**和**递归式**来描述算法的运行时间。

假设输入规模为$n$的总运行时间为$T(n)$，如果分解后的子问题规模足够小，例如常量$c$，当$n \le c$时则需要常量时间$ \Theta(1)$，否则将$n$分解成了$a$个子问题，每个子问题规模是原来的$1 \over b$，那么求解$a$个子问题需要代价$aT({n \over b})$，假设分解问题需要代价$D(n)$，合并子问题的解成原问题需要代价$C(n)$，那么可得到**递归式**：

$$ T(n) = \begin{cases}\Theta(1) & 若n \le c  \\\\ aT({ n \over b }) + D(n) + C(n)	& 其他			\end{cases}  $$


#### 3.2 归并排序的分析


在**归并排序**中，分解仅仅是计算数组的中间位置，因此$D(n)=\Theta(1)$，解决问题问题需要$2T({n \over 2})$的运行代价(因为每次都将问题分解成2个子问题，每个子问题的规模是原来的$1 \over 2$)，合并子问题需要代价$\Theta(n)$，因此可得出归并排序最坏情况的运行代价$T(n)$的**递归式**：

$$ T(n) = \begin{cases}\Theta(1) & 若n = 1 \\\\ 2T({ n \over 2}) + \Theta(n)	& 若n > 1 \end{cases}  $$

> 需要注意这里合并子问题的时间计算，查看`merge`函数我们可以发现在最坏情况下，`for`循环需要遍历$n$次，在函数中有多个循环遍历，因此合并需要的代价$T(n) = an + b$，运行时间记为$\Theta(n)$。同时在这里$D(n) = \Theta(1)$将被省略，因为它不是一个重要的项，不影响最后的增长量级计算。

为了进行精确计算，把**递归式**重写为：

$$ T(n) = \begin{cases} c & 若n = 1 \\\\ 2T({ n \over 2}) + cn	& 若n > 1 \end{cases}  $$

> 常量$c$：求解规模为1的问题所需的时间 + 分解步骤时间 + 合并步骤时间。

下图展示了如何求解上述递归式，假设$n$正好是2的幂，在递归的顶层，输入规模为$n$的运行代价为$cn$，将问题一分为二需要的运行代价为$2* {cn \over 2}$。以此类推，如图中所示，每一层中虽然解决子问题的数量增多了，但是该层解决问题的代价仍然为$cn$。

![插入排序](https://raw.githubusercontent.com/ziyi2/algorithms-javascript/master/img/algorithms-base/merge-sort_3.png)

问题在于解决总问题需要多少$cn$，也就是需要计算分解了多少次子问题(在上图中可以理解为除了顶层树有多少层)。

如图中所示，假设顶层为第0层，可以发现第$i$层解决单个子问题需要的代价为$cn \over {2^i}$，问题规模下降到1后，解决单个子问题需要的代价为$c$，因此求解的$i$值是树的总层数，也是分解问题的次数，即有

$$ c = {cn \over {2^i}}  $$
$$ i = lgn$$ 

总问题分解了$lgn$次，每次运行代价为$cn$，加上顶层的运行代价，总代价为：

$$ T(n) = cnlgn + cn  $$

去掉不重要的项，**归并排序**的运行时间为$\Theta(nlgn)$。

> 需要注意这里的$lg$是以2为底，实时上在计算机中2可以方便计算，采用其他数量为底只是相差了常数倍而已，如果不是特别清晰可查看参考文献。

### 4. 小结

引入用于算法设计的**分治法**并使用该方法设计**归并排序**算法，分析其运行时间。如果$T(n) = aT({n \over b}) + f(n)$，该递归式求解需要的时间为$\Theta(nlgn)$，同时从下图可以发现，**归并排序**的最坏情况运行时间比**插入排序**要小的多。

![算法运行时间比对](https://raw.githubusercontent.com/ziyi2/algorithms-javascript/master/img/algorithms-base/insert-merge-sort.png)




### 参考文献

[为什么算法渐进复杂度中对数的底数总为2](http://blog.codinglabs.org/articles/why-logarithm-base-of-asymptotic-time-complexity-always-two.html)


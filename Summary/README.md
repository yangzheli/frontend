## 工作总结

### 内存泄漏

内存泄漏是指不再需要的对象仍然存在于内存（栈/堆）中，根据 JS 的垃圾回收机制，垃圾收集器会定时、周期性地找出不再继续使用的变量，然后释放其占用的内存。

标识无用变量的策略通常有两种：

- 标记清除（最常用）：垃圾收集器会给内存中所有变量都加上标识，然后去掉环境中的变量和被环境中变量引用的变量的标识，之后仍然被加上标识的变量就会被垃圾收集器回收所占用的内存。
- 引用计数：跟踪每个值被引用的次数，当这个值的引用次数变为 0，其占用的内存空间就会被回收。

会造成内存泄漏的操作有：

- 全局变量
- 闭包
- DOM 泄漏
- 被遗忘的定时器
- console.log
- 循环引用

避免内存泄漏问题的最佳方式就是为执行中的代码只保留必要的数据，一旦数据不再有用，就解除该值的引用（例如：将该值设置为 null）。

### 排序算法及优化

- 冒泡排序

```javascript
function bubble_sort(arr) {
  // 比较相邻元素的大小，直到没有可以交换的元素（每轮循环后未排序序列中最大元素为该序列最后一个元素）
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j + 1] < arr[j]) {
        swap(arr, j, j + 1);
      }
    }
  }
  return arr;
}
```

优化 1：对于已经排好序的数组，或经过几轮交换后排好序的数组，通过统计交换次数判断数组是否已经有序，提前结束循环。例如：[1, 2, 3, 4, 5, 10, 9]

```javascript
function bubble_sort(arr) {
  for (let i = 0; i < arr.length; i++) {
    // 该趟循环交换的次数，当交换次数为0说明数组已经有序
    let count = 0;
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j + 1] < arr[j]) {
        swap(arr, j, j + 1);
        count++;
      }
    }
    if (count === 0) {
      return arr;
    }
  }
  return arr;
}
```

优化 2：优化 1 对于前面大部分无序，后面小部分有序的数组排序效率也不可观，对于这种类型数据，可以记录下最后一次交换的位置，后面没有交换，下次排序就从记录的位置结束。例如：[1, 7, 5, 4, 6, 8, 9, 10]

```javascript
function bubble_sort(arr) {
  // 记录最后一次交换的索引
  let index = arr.length - 1;
  for (let i = 0; i < arr.length; i++) {
    let tmp = 0;
    for (let j = 0; j < index; j++) {
      if (arr[j + 1] < arr[j]) {
        swap(arr, j, j + 1);
        tmp = j;
      }
    }
    index = tmp;
    // 数组已经有序
    if (index === 0) {
      return arr;
    }
  }
  return arr;
}
```

优化 3：如果最小值在数组末尾，优化 2 效率也不可观，可以通过正反交替扫描，正向找到最大值，反向找到最小值。例如：[1, 2, 3, 4, 7, 0]

```javascript
function bubble_sort_opt3(arr) {
  for (let i = 0; i < arr.length; i++) {
    // 统计交换次数
    let count = 0;
    // 正向扫描
    for (let j = i; j < arr.length - i - 1; j++) {
      if (arr[j + 1] < arr[j]) {
        swap(arr, j, j + 1);
        count++;
      }
    }
    if (count === 0) {
      return arr;
    }
    count = 0;
    // 反向扫描
    for (let j = arr.length - i - 1; j > i; j--) {
      if (arr[j - 1] > arr[j]) {
        swap(arr, j - 1, j);
        count++;
      }
    }
    if (count === 0) {
      return arr;
    }
  }

  return arr;
}
```

- 快速排序

```javascript
function quick_sort(arr) {
  return sort(arr, 0, arr.length - 1);
}

function sort(arr, left, right) {
  if (left >= right) {
    return arr;
  }
  // 切分后的数组index左边的值都都小于arr[index]，index右边的值都大于arr[index]
  let index = partition(arr, left, right);
  sort(arr, left, index - 1);
  sort(arr, index + 1, right);
  return arr;
}

function partition(arr, left, right) {
  // 切分元素
  let p = arr[left];
  let i = left,
    j = right;
  while (i < j) {
    while (i < j && arr[j] >= p) {
      j--;
    }
    while (i < j && arr[i] <= p) {
      i++;
    }
    swap(arr, i, j);
  }
  swap(arr, left, i);
  // 返回索引
  return i;
}
```

优化 1：由于快速排序中基准（切分元素）的选择对排序效率有很大影响，如果选择固定的基准，例如数组中的第一个元素，当数组已经基本有序时，效率十分低下，可以采用随机基准或者三数取中的方式对其进行优化（三数取中即从数组开头、中间和结尾三个元素中选中间值作为基准）。例如：[1, 2, 3, 4, 5, 6]

```javascript
```

优化 2：当快速排序到达一定的深度，划分的区间较小时（5~20 之间），再使用递归切分的方式进行排序的效率不高，此时可以使用插入排序

```javascript
```

优化 3：尾递归优化

- 插入排序

```javascript
function insertion_sort(arr) {
  // 从前向后构建有序序列
  for (let i = 0; i < arr.length; i++) {
    // 从后往前遍历，直到找到小于等于该元素的索引
    let index = i,
      val = arr[index];
    while (index >= 1 && arr[index - 1] > val) {
      arr[index] = arr[index - 1];
      index--;
    }
    // 找到目的索引
    arr[index] = val;
  }
  return arr;
}
```

优化 1：对于某个未排序元素，需要从后往前遍历找到小于等于该元素的索引，可以通过二分查找的方式加快查找过程

```javascript
function insertion_sort(arr) {
  // 从前向后构建有序序列
  for (let i = 0; i < arr.length; i++) {
    // 从后往前遍历，直到找到小于等于该元素的索引
    let val = arr[i];
    // 二分查找
    let low = 0,
      high = i - 1;
    while (low <= high) {
      let mid = low + Math.floor((high - low) / 2);
      if (arr[mid] > val) {
        high = mid - 1;
      } else {
        low = mid + 1;
      }
    }

    // 移动元素
    for (let j = i - 1; j > high; j--) {
      arr[j + 1] = arr[j];
    }
    arr[high + 1] = val;
  }
  return arr;
}
```

- 希尔排序：也是插入排序的一种优化

```javascript
function shell_sort(arr) {
  // 动态间隔，间隔每次/2
  for (
    let gap = Math.floor(arr.length / 2);
    gap > 0;
    gap = Math.floor(gap / 2)
  ) {
    // 从前向后以间隔为gap构建部分有序序列
    for (let i = gap; i < arr.length; i++) {
      let index = i,
        val = arr[index];
      // 从后往前遍历
      while (index - gap >= 0 && arr[index - gap] > val) {
        arr[index] = arr[index - gap];
        index -= gap;
      }
      arr[index] = val;
    }
  }
  return arr;
}
```

- 选择排序

```javascript
function selection_sort(arr) {
  // 每轮筛选出未排序序列中的最小元素，放在已排序序列的末尾
  for (let i = 0; i < arr.length; i++) {
    let minIndex = i;
    for (let j = i; j < arr.length; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    swap(arr, i, minIndex);
  }
  return arr;
}
```

- 堆排序

```javascript
// 每个节点的值大于或等于左右孩子节点的值，为大根堆；每个节点的值小于或等于左右孩子节点的值，为小根堆；
// 一般升序采用大根堆，降序采用小根堆
function heap_sort(arr) {
  let N = arr.length;
  for (let k = Math.floor(N / 2) - 1; k >= 0; k--) {
    // 最后一个非叶子节点索引为 N/2-1
    // 构建大根堆
    sink(arr, k, N);
  }

  // 将堆顶元素与数组末尾元素进行交换，再重新调整堆中元素、交换位置，直到整个数组有序
  while (N > 1) {
    swap(arr, 0, --N); // 交换
    sink(arr, 0, N);
  }

  return arr;
}

function sink(arr, k, N) {
  let left = 2 * k + 1; // 2*k+1是k的左子树，因为根节点索引是0(而不是1)
  while (left < N) {
    if (left + 1 < N && arr[left] < arr[left + 1]) {
      // 2*k+2是k的右子树
      left++;
    }
    if (arr[k] >= arr[left]) {
      // 不用交换
      break;
    }
    swap(arr, k, left);
    k = left;
    left = left * 2 + 1;
  }
}
```

- 归并排序

```javascript
function merge_sort(arr) {
  if (arr.length < 2) {
    return arr;
  }
  let mid = Math.floor(arr.length / 2);
  let left = merge_sort(arr.slice(0, mid)),
    right = merge_sort(arr.slice(mid));
  // 合并两个排好序的数组
  return merge(left, right);
}

function merge(left, right) {
  let res = [];
  // 双指针
  let i = 0,
    j = 0;

  while (i < left.length && j < right.length) {
    if (left[i] < right[j]) {
      res.push(left[i++]);
    } else {
      res.push(right[j++]);
    }
  }

  while (i < left.length) {
    res.push(left[i++]);
  }

  while (j < right.length) {
    res.push(right[j++]);
  }

  return res;
}
```

优化：对小规模子数组使用插入排序

- 基数排序

```javascript
function radix_sort(arr) {}
```

- 计数排序：输入数据必须为有确定范围的数组

```javascript
function counting_sort(arr, maxValue) {
  let bucket = new Array(maxValue + 1);
  // 统计不同元素出现的次数
  for (let i = 0; i < arr.length; i++) {
    // 初始化为0
    if (!bucket[arr[i]]) {
      bucket[arr[i]] = 0;
    }
    bucket[arr[i]]++;
  }

  let index = 0;
  // 根据bucket重新构件数组
  for (let i = 0; i < bucket.length; i++) {
    while (bucket[i] > 0) {
      arr[index++] = i;
      bucket[i]--;
    }
  }

  return arr;
}
```

- 桶排序

```javascript
function bucket_sort(arr) {}
```

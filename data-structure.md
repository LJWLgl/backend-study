# 排序
## 插入排序
直接插入排序是一种最简单的排序方法，其基本操作是将记录一条记录插入到已排好序的有序表中，从而得到一个新的，记录数量增1的有序表

排序过程如图：
<div align="center"> <img src="http://tc.ganzhiqiang.wang/1560068871.png" width="500px"> </div>
```Java
/**
 * 直接插入排序
 * @param array 待排序数据
 */
public static void insertSort(int[] array) {
    int temp;
    for (int i = 1; i < array.length; i++) {
        // 待插入的记录暂存到temp
        temp = array[i];
        int j = i - 1;
        for (;j>=0 && temp < array[j]; j--) {
            // 记录逐个后移，直到找到插入位置
            array[j+1] = array[j];
        }
        array[j + 1] = temp;
    }
}
```
复杂度
- 时间复杂度：O(n^2)
- 空间复杂度：O(1)

## 选择排序
## 快速排序
```java
public static int partition(int[] arr, int low, int high) {
    // 选择第一个元素作为枢纽
    int temp = arr[low];
    while (low < high) {  // 从表的两端交替向中间扫描
        while (low < high && arr[high] >= temp) high--;
        arr[low] = arr[high];  // 比枢纽小的移到低端
        while (low < high && arr[low] <= temp) low++;
        arr[high] = arr[low]; // 比枢纽大的移到高端
    }
    arr[low] = temp;  // 此时low=high
    return low; // 返回枢纽位置
}

public static void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int key = partition(arr, low, high);
        // 对左子表递归排序
        quickSort(arr, low, key - 1);
        // 对右子表递归排序
        quickSort(arr, key + 1, high);
    }
}
```
**算法复杂度** 
- 时间复杂度：O(nlog2n)
- 空间复杂度：O(n)
**算法特点**
- 非稳定排序
- 当n较大时，在平均情况下快速排序是所有内部排序中最快的
- 适合对无需的数组，n较大的情况
- 很难用于链式结构
## 堆排序

# 二叉树
## 二叉排序树（二叉搜索树）
## 平衡二叉树（AVL树）
## 红黑树
- [红黑树(一)之 原理和算法详细介绍](https://www.cnblogs.com/skywang12345/p/3245399.html)
红黑树的特性：
1. 每个节点或者是黑色，或者是红色。
2. 根节点是黑色。
3. 每个叶子节点（NIL）是黑色。 [注意：这里叶子节点，是指为空(NIL或NULL)的叶子节点！]
4. 如果一个节点是红色的，则它的子节点必须是黑色的。
5. 从一个节点到该节点的子孙节点的所有路径上包含相同数目的黑节点。
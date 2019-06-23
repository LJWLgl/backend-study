# 链表
# 二叉树
二叉树的定义：它是n（n>=0）个结点的有限集合，该集合或者为空集（称为空二叉树），或者`由一个根结点和两棵互不相交的、分别称为根结点的左子树和右子树的二叉树组成。`
它具有以下特点：
- 每个结点最多有两颗子树，`所有二叉树中不存在度大于2的结点`
- 左子树和右子树是有顺序的，不能任意颠倒
- 即使树中某结点只有一棵子树，也要区分它是左子树还是右子树
二叉树节点定义如下代码所示
```java
public class TreeNode<T> {
    private T value;
    private TreeNode<T> left;
    private TreeNode<T> right;
    ...
}
```
### 创建二叉树
二叉树的创建一般采用前序遍历，下面代码是创建如图所示的二叉树，其中`“#”`代表`null`
<div align="center"> <img src="http://tc.ganzhiqiang.wang/binaytree1.png" width="400px"><p>图1-1</p> </div><br/>  

```java
public BinaryTree() {
    Scanner scanner = new Scanner("1 2 4 8 # # 9 # # 5 # # 3 6 # # 7 # #");
    root = createTree(root, scanner);
}

public TreeNode<T> createTree(TreeNode<T> node, Scanner scn) {
    String temp = scn.next();
    if (temp.trim().equals("#")) {
        return null;
    } else {
        node = new TreeNode<>((T)temp);
        node.setLeft(createTree(node.getLeft(), scn));
        node.setRight(createTree(node.getRight(), scn));
        return node;
    }
}
```
### 前序遍历
前序遍历的递归算法比较简单，先打印节点，再递归左子树和右子树即可
```java
/**
 * 递归先序遍历
 */
public void preTraver(TreeNode<T> node) {
    if (node != null) {
        System.out.print(node.getValue() + " ");
        preTraver(node.getLeft());
        preTraver(node.getRight());
    }
}
```
前序非递归算法使用栈来实现，思想就是先将根节点和根节点全部入栈，再逐个弹出栈顶元素，将栈顶元素的右子树也全部入栈，直至栈为空，步骤如图所示
<div align="center"> <img src="http://tc.ganzhiqiang.wang/prebintree.jpg" width="400px"> <p>图1-2</p></div><br/>

```java
/**
 * 先序遍历非递归
 */
public void preTraver() {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode node = root;
    while (node != null || ! stack.isEmpty()) {
        while (node != null) { // 将根节点和左子树的根节点入栈，直到左子树为空
            System.out.print(node.getValue() + " ");
            stack.push(node);
            node = node.getLeft();
        }
        node = stack.pop();
        node = node.getRight();
    }
}
```
### 中序遍历
```java
public void midTraver(TreeNode<T> node) {
    if (node != null) {
        midTraver(node.getLeft());
        System.out.print(node.getValue() + " ");
        midTraver(node.getRight());
    }
}
```
中序遍历非递归算法思想和先序差不多，不过它是在即将访问右子树时才打印当前节点的value
```java
public void midTraver() {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode node = root;
    while (node != null || ! stack.isEmpty()) {
        while (node != null) { // 将根节点和左子树的根节点入栈，直到左子树为空
            stack.push(node);
            node = node.getLeft();
        }
        node = stack.pop();
        System.out.print(node.getValue() + " ");
        node = node.getRight();
    }
}
```
### 后序遍历
```java
public void afterTraver(TreeNode<T> node) {
    if (node != null) {
        afterTraver(node.getLeft());
        afterTraver(node.getRight());
        System.out.print(node.getValue() + " ");
    }
}
```

```java
public void afterTraver() {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode node = root;
    TreeNode preNode = null; // 表示最近一次访问的节点
    while (node != null || !stack.isEmpty()) { // 右子树不为空，或者栈不为空（其子树已经处理过）
        while (node != null) { // 将根节点和左子树的根节点入栈，直到左子树为空
            stack.push(node);
            node = node.getLeft();
        }

        node = stack.peek(); // stack.peek()查找栈顶对象，但不移除它 查看栈顶元素
        if (node.getRight() == null || node.getRight() == preNode) { // 该节点的右子树为空，或者其右子树已经被访问过
            System.out.print(node.getValue() + " "); // 访问该节点
            node = stack.pop();
            preNode = node;
            node = null; // 将node置为空，用于判断栈中的下一元素
        } else {
            node = node.getRight();
        }
    }
}
```
### 层序遍历
二叉树的层序遍历，采用队列实现，遍历流程大致，先将树的根节点入队，如果队列不空，则循环执行123步
1.  将队首元素出队，并输出它；
2. 如果该队首元素有左孩子，则将其左孩子入队；
3. 如果该队首元素有右孩子，则将其右孩子入队；
```java
public void levelTraver() {
    Queue<TreeNode> queue = new ArrayDeque<>();
    queue.offer(root); // root节点进队列
    while (! queue.isEmpty()) {
        TreeNode parent = queue.poll(); // 队首
        System.out.print(parent.getValue() + " ");
        if (parent.getLeft() != null) { // 左孩子进入队列
            queue.offer(parent.getLeft());
        }
        if (parent.getRight() != null) { // 右孩子进入队列
            queue.offer(parent.getRight());
        }
    }
}
```
# 排序
## 插入排序
直接插入排序是一种最简单的排序方法，其基本操作是将记录一条记录插入到已排好序的有序表中，从而得到一个新的，记录数量增1的有序表

排序过程如图：
<div align="center"> <img src="http://tc.ganzhiqiang.wang/bs-1-5.png" width="400px"> <p>图1-5 直接插入排序过程</p> </div><br/>

```java
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
**算法思想**
在待排序的n个记录中任取一个记录（通常取第一个）作为`枢纽`，经过一趟排序后，把记录中值比枢纽值小的交换到前面，把所有值比`枢纽值`大的交换到后面，即将待排序的记录分成两个子表，将枢纽放在分界位置，然后对左右子表再进行上述过程，直至每个子表只有一个记录时，排序完成。
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
- 适合对无序的数组，n较大的情况，
    - 如果数组已有序，那么枢纽节点可能为最小值或最大值，造成了分布极不均匀
- 很难用于链式结构
## 堆排序
堆排序是利用了完全二叉树的性质：`树中所有非终节点均不大于（或不小于）其左右孩子节点的值`，堆排序分为两步`建初堆`和`调整堆`，它们都利用`筛选法`来实现。

**筛选法的算法步骤：**
从r[2s]和r[2s+1]中选出较大的，假设r[2s]较大，则比较r[s]和r[2s]的大小：
1. 若r[s]  >= r[2s]，说明以r[s]为根的子堆已是大根堆（小根堆），不做任何调整。
2. 若r[s]  < r[2s]，则s=2s，r[s] = r[2s]，即继续向下筛选，重复以上过程，直至到叶子节点。  

**用筛选法调整堆：**
<div align="center"> <img src="http://tc.ganzhiqiang.wang/1-6.png" width="500px"><p>图1-6 筛选法</p> </div><br/>

```java
public class HeapSort {
    private static int length; // 数组长度

    public static void heapAdjust(int[] array, int s, int m) {
        // 动态规划的做法，假设array[s + 1, m]已是大根堆
        int value = array[s];
        for (int j=2 * s;j <= m; j*=2) {
            if (j<m && array[j] < array[j+1]) // 沿着较大的key，向下比较
                ++j;
            if (value >= array[j]) // value比array[j, m]都大，value应该放在这
                break;
            array[s] = array[j]; //array[j]移到父节点
            s = j;
        }
        array[s] = value;
    }

    public static void createHeap(int[] array) {
        // 完全二叉树中，叶子节点没有孩子节点，故从length/2开始，利用筛选法将数组调整成大根堆
        for (int i = length / 2; i > 0; i--) {
            heapAdjust(array, i, length);
        }
    }

    public static void heapSort(int[] array) {
        createHeap(array); // 将array调整成大根堆
        for (int i = length;i > 1; i--) {
            int tmp = array[i];
            array[i] = array[1];
            array[1] = tmp;
            heapAdjust(array, 1, i - 1); // 堆顶元素移至尾节点，将array[1, i-1]重新调整成大根堆
        }
    }

    public static void main(String[] args) {
        // 第一个数0只是用来占位，保证从数组的第1位开始排序
        int[] array = {0,49,38,65,97,76,13,27,49};
        // 0是用来占位，故实际排序长度为array.length - 1
        length = array.length - 1;
        heapSort(array);
        System.out.println(Arrays.toString(array));
    }
}
```

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
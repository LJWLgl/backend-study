## HashMap
- [《Java7/8 中的 HashMap 和 ConcurrentHashMap 全解析》](https://javadoop.com/post/hashmap)
- [《Java容器》](https://github.com/CyC2018/CS-Notes/blob/master/notes/Java%20%E5%AE%B9%E5%99%A8.md)
** HashMap总结 **
1. hashMap底层存储结构：数组+链表，JDK1.8通过数组+链表+红黑树实现
2. hashMap table表每次扩容是原数组长度的2倍，长度始终是2^n倍，可方便通过 hash & table.length - 1计算出索引的位置
3. hashMap插入数据始终插在表头，JDK1.8在链表的表尾
4. hashMap是非线程安全
** ConcurrentHashMap **
1. ConcurrentHashMap通过segement

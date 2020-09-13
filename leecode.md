# 模拟问题

## 十进制转二进制

### 移位运算

```java
// 10进制转2进制，采用移位运算
// 思想：循环int最大长度（2的31次方）,按从左至右的顺序将每一位移至最后移位，然后&1，可得该位是0还是1
public static String tenToTen(int n) {
  StringBuilder builder = new StringBuilder();
  for (int i = 31;i >=0; i--) {
    builder.append(n >>> i & 1);
  }
  return builder.toString();
}
```



# 递归问题

# 动态规划问题
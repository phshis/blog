---
title: x 的平方根
tags: 'LeetCode'
categories: 
  - 'LeetCode'
  - '算法'
abbrlink: 13349
description: leetcode x 的平方根
date: 2021-04-18 22:06:28
keywords: 
  - 'LeetCode'
top_img: images/leetcode/sqrtx.jpg
cover: images/leetcode/sqrtx-canva.jpg

---

- 日期：2021年4月18日
- 描述：🐷大猪来找我，一个周没写了，惭愧，今天又要开始继续，一天不能落。

### x 的平方根

原文链接：[x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

1. **问题描述：**

实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

2. **示例 1：**

```
输入: 4
输出: 2
```

3. **示例 2：**

```
输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
由于返回类型是整数，小数部分将被舍去。
```

#### 自己思考

##### 方式一

`代码`

```java
public int mySqrt(int x) {
  double indx = 0;
  for (double i = 0; i <= (double) x; i++) {
    double a = i * i;
    if (a > (double) x) {
      break;
    }
    indx = i;
  }
  return (int) indx;
}
```

`提交结果:`

```
执行用时：62 ms, 在所有 Java 提交中击败了5.00%的用户
内存消耗：35.3 MB, 在所有 Java 提交中击败了88.80%的用户
```

`总结:` 暴力法，从零开始循环依次平方，找到刚好大于目标值的那个值。这执行用时，实在是拉垮。

**注意：**这个int会存在值溢出的情况，刚开始就一直不对一直没想到是int值超过最大值的问题。

#### 官方解答

##### 方式一

`代码`

```java
public int mySqrt(int x) {
  int l = 0, r = x, ans = -1;
  while (l <= r) {
    int mid = l + (r - l) / 2;
    if ((long) mid * mid <= x) {
      ans = mid;
      l = mid + 1;
    } else {
      r = mid - 1;
    }
  }
  return ans;
}
```

`提交结果`

```
执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：35.4 MB, 在所有 Java 提交中击败了81.84%的用户
```

总结：性能是真的好。（二分法查找法自己还得练一下）

##### 方式二

`代码：`

```java
public int mySqrt(int x) {
  if (x == 0) {
    return 0;
  }

  double C = x, x0 = x;
  while (true) {
    double xi = 0.5 * (x0 + C / x0);
    if (Math.abs(x0 - xi) < 1e-7) {
      break;
    }
    x0 = xi;
  }
  return (int) x0;
}
```

`提交结果：`

```
执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：35.7 MB, 在所有 Java 提交中击败了29.51%的用户
```

`总结：`牛顿迭代。内存消耗有点小高，但是相对于二分法是更快的。没看懂。

#### 路人解答

##### 方式一

思路：

`( 4 + 2/ 4 ) / 2 = 2.25`

`( 2.25 + 2/ 2.25 ) / 2 = 1.56944..`

`( 1.56944..+ 2/1.56944..) / 2 = 1.42189..`

`( 1.42189..+ 2/1.42189..) / 2 = 1.41423..`

`代码：`

```java

class Solution {
  int s;

  public int mySqrt(int x) {
    s=x;
    if(x==0) return 0;
    return ((int)(sqrts(x)));
  }

  public double sqrts(double x){
    double res = (x + s / x) / 2;
    if (res == x) {
      return x;
    } else {
      return sqrts(res);
    }
  } 
}
```

`提交结果：`

```
执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：35.3 MB, 在所有 Java 提交中击败了95.22%的用户
```

`总结：递归牛顿迭代。很巧妙，突然觉得我的数学白学了。。
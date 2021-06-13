---
title: 实现strStr()
tags: 'LeetCode'
categories: 
  - 'LeetCode'
  - '算法'
abbrlink: 13336
description: leetcode实现strstr()函数
date: 2021-04-4 21:54:28
keywords: 
  - 'LeetCode'
top_img: images/leetcode/implement-strstr.jpg
cover: images/leetcode/implement-strstr-canva.jpg


---

- 日期：2021年4月4日
- 描述：好几天没写了，今天可不能再休息了

#### 实现 strStr()

原文链接：[实现 strStr()](https://leetcode-cn.com/problems/implement-strstr/)

1. **问题描述：**

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1

2. **示例 1：**

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

3. **示例 2：**

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

4. **提示**

- 当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

  对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。


#### 自己思考

##### 方式一

`代码`

```java
public static int strStr(String haystack, String needle) {
  if (needle == null || "".equals(needle)) {
    return 0;
  } else if (!haystack.contains(needle)) {
    return -1;
  }
  int length = needle.length();
  char c = needle.charAt(0);
  for (int i = 0; i <= haystack.length() - length; i++) {
    char c1 = haystack.charAt(i);
    if (c == c1) {
      String substring = haystack.substring(i, i + length);
      if (needle.equals(substring)) {
        return i;
      }
    }
  }
  return -1;
}
```

`提交结果:`

```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：36.8 MB, 在所有 Java 提交中击败了94.71%的用户
```

`总结:` 刚开始想了很久，但是总是没有好的思路，休息了一会回来，突然想到并不是所有都需要判断，所以加上了contains的语句，然后，接下来判断原语句中必然存在相等的代码块，只需要找出位置即可，但是，由于可以走到下面的，必然会至少存在一个，所以直接取出第一个，只有第一个相等了在进行截取，可以很大程度的剔除不满足的目标。

#### 官方解答

##### 方式一

`代码`

```java
public int strStr(String haystack, String needle) {
	int L = needle.length();
  int n = haystack.length();
  for (int start = 0; start < n - L + 1; start++) {
    if (haystack.substring(start, start + L).equals(needle)) {
      return start;
    }
  }
  return -1;      
}
```

`提交结果`

```
执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：38.6 MB, 在所有 Java 提交中击败了17.15%的用户
```

`总结：`和我的想法差不多，只不过我添加相应的执行条件，而他直接不管什么时候都是直接执行的。
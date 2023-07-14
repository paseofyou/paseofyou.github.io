---
title: "level2"
date: 2023-07-15T01:11:34+08:00
draft: false
weight: 10
---

# 认识O(NlogN)的排序

## 剖析递归行为和递归行为时间复杂度的估算

用递归方法找一个数组中的最大值

master公式的使用

T(N) = a*T(N/b) + O(N^d)

> T(N) 母问题是N规模的数据，每一次的子过程都是b的规模（只划分了总规模的1/b），该子过程调用了a次（递归调用调了a次），其他执行语句的时间复杂度为d。

1. log(b,a) > d -> 复杂度为O(N^log(b,a))
2. log(b,a) = d -> 复杂度为O((N^d)*log(N))
3. log(b,a) < d -> 复杂度为O(N^d)

```java
//求arr数组里面的最大值
private static int getMax() {
   return get(arr, 0, arr.length - 1);
}

private static int get(int[] arr, int left, int right) {
    if (left == right) return arr[left];
    int mid = left + ((right - left) >> 1);
    int l = get(arr, left, mid);
    int r = get(arr, mid + 1, right);
    return Math.max(l, r);
}
```



### 归并排序

1. 整体就是一个简单递归，左边排好序，右边排好序，让其整体有序
2. 让其整体有序的过程用了排外序方法
3. 利用master公式来求解时间复杂度
4. 归并排序的实质

时间复杂度为O(N*log(N)) ，额外空间复杂度为O(N)
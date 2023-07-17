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

```java
private static void sort() {
    if (arr == null || arr.length < 2) return;
    process(arr, 0, arr.length - 1);
}

private static void process(int[] arr, int L, int R) {
    if (L == R) return;
    int mid = L + ((R - L) >> 1);
    process(arr, L, mid);
    process(arr, mid + 1, R);
}

private static void merge(int[] arr, int L, int M, int R) {
    int i = 0, p1 = L, p2 = M + 1;
    int[] help = new int[R - L + 1];
    while (p1 <= M && p2 <= R) help[i++] = arr[p1] <= arr[p2] ? arr[p1] : arr[p2];
    while (p1 <= M) help[i++] = arr[p1++];
    while (p2 <= M) help[i++] = arr[p2++];
    for (int j = 0; j < help.length; j++) arr[L++] = help[j++];
}
```

为什么比其他的O(N^2)时间复杂度更快？

因为选择，冒泡，插入排序，在每一次遍历比较过程中，只选择好了一个数据顺序，导致大量的比较结果被丢弃造成浪费。

### 归并排序的扩展

小和问题

在一个数组中，每一个数左边比当前数小的数累加起来，叫做这个数组的小和。求一个数组的小和。

```java
private static int process(int[] arr, int L, int R) {
    if (L == R) return 0;
    int sum = 0;
    int mid = L + ((R - L) >> 1);
    sum += process(arr, L, mid);
    sum += process(arr, mid + 1, R);
    return sum + calc(arr, L, mid, R);
}

private static int calc(int[] arr, int L, int M, int R) {
    int sum = 0;
    int[] help = new int[R - L + 1];
    int i = 0, p1 = L, p2 = M + 1;
    while (p1 <= M && p2 <= R) {
        sum+=arr[p1]<arr[p2]?arr[p1]*(R-p2+1):0;
        help[i++] = arr[p1]<arr[p2]?arr[p1++]:arr[p2++];
    }
    while (p1 <= M) help[i++] = arr[p1++];
    while (p2 <= R) help[i++] = arr[p2++];
    for (int j = 0; j < help.length; j++) {
        arr[L++] = help[j];
    }
    return sum;
}
```



逆序对问题

在一个数组中，左边的数如果比右边的数大，则这两个数构成一个逆序对，请打印所有逆序对。

> 与“小和问题”问题等价

### 荷兰国旗问题

问题一

给定一个数组arr，和一个数num，请把小于等于num的数放在数组左边，大于num的数放在数组右边，要求额外空间复杂度O(1),时间复杂度O(N)

1. [i]<=num：[i]和<=区的下一个数据交换，<=区向右边扩充，i++
2. [i]>num：i++

问题二（荷兰国旗问题）

给定一个数组arr，和一个数num，请把小于num的数放在数组的左边，等于num的数放在数组的中间，大于num的数放在数组右边。要求额外空间复杂度O(1)，时间复杂度为O(N)。

1. [i]<num：[i]和<=区的下一个数据交换，<=区向右边扩充，i++
2. [i]==num：i++
3. [i]>num：[i]和>=区的前一个数据交换，>=区向右边扩充，i不动


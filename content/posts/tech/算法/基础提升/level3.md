---
title: "level3"
date: 2023-07-17T01:11:34+08:00
draft: false
weight: 10
---

# 详解桶排序以及排序内容大总结

## 不改进的快速排序

1. 把数组范围中的最后一个数作为划分值，然后把数组通过荷兰国旗问题分成三个部分：

   左侧<划分值、中间==划分值、右侧>划分值

2. 对左侧范围和右侧范围，递归执行

分析：

1. 划分值越靠近两侧，复杂度越高；划分值越靠近中间，复杂度越低
2. 可以轻而易举的举出最差的例子，所以不改进的快速排序时间复杂度为O(N^2)

## 随机快速排序（改进的快速排序）

1. 在数组范围中，等概率随机选一个数作为划分值，然后把数组通过荷兰国旗问题分成三个部分

左侧<划分值、中间==划分值、右侧>划分值

2. 对左侧范围和右侧范围，递归执行
3. 时间复杂度为O(N*logN)

```java
//leetcode 第75题
class Solution {
    public void sortColors(int[] nums) {
        sort(nums,0,nums.length-1);
        System.out.println(Arrays.toString(nums));
    }

    private void sort(int[] nums,int L,int R){
        if(L>=R) return;
        swapArr(arr, (int) (Math.random() * (R - L + 1))+L, R);
        int[] p = partition(nums,L,R);
        sort(nums,L,p[0]-1);
        sort(nums,p[1]+1,R);
    }

    private void swapArr(int[] arr, int L,int R){
        int tmp = arr[L];
        arr[L]= arr[R];
        arr[R] = tmp;
    }
    private int[] partition(int[] arr,int L,int R){
        int less = L-1;
        int more = R;
        while(L<more){
            if(arr[L]>arr[R]){
                swapArr(arr,L,--more);
            }else if(arr[L]<arr[R]){
                swapArr(arr,L++,++less);
            }else{
                L++;
            }
        }
        swapArr(arr,R,more);
        return new int[]{less+1,more};
    }
}
```

## 堆

1. 堆结构就是用数组实现的完全二叉树结构
2. 完全二叉树中如果每颗子树的最大值都在顶部就是最大根堆
3. 完全二叉树中如果每颗子树的最小值都在顶部就是最小根堆
4. 堆结构的heapInsert与heapify操作
5. 堆结构的增大和减少
6. 优先级队列结构，就是堆结构

堆上，插入，删除，heapifiy的时间复杂度为O(logN)级别，空间复杂度O(1)

## 堆排序

1. 先让整个数组都变成大根堆结构，建立堆的过程：
   1. 从上到下的方法，时间复杂度为O(N*logN)：堆结构增加的方法
   2. 从下到上的方法，时间复杂度为O(N)：倒序遍历进行大根堆调整

2. 把堆的最大值和堆末尾的值交换，然后减少堆的大小之后，再去调整堆，一直周而复始，时间复杂度为O(N*logN)
3. 堆的大小减少成0之后，排序完成

```java
private static void sort(int[] arr) {
    if (arr==null|| arr.length<2)return;
    for (int i = 0; i < arr.length; i++) {
        heapInsert(arr, i);
    }
    int heapSize = arr.length;
    while (heapSize>0){
        heapify(arr,0,--heapSize);
        swapArr(arr,0,heapSize);
    }
}

private static void heapInsert(int[] arr, int index) {
    while (arr[index] > arr[(index - 1) / 2]) {
        swapArr(arr, index, (index - 1) / 2);
        index = (index - 1) / 2;
    }
}

private static void heapify(int[] arr, int index, int heapSize) {
    int left = index * 2 + 1;
    while (left < heapSize) {
        int largest = (left + 1) < heapSize && arr[left] < arr[left + 1] ? left + 1 : left;
        largest = arr[largest] > arr[index] ? largest : index;
        if (largest == index) break;
        swapArr(arr, index, largest);
        index = largest;
        left = index * 2 + 1;
    }
}
```

## 堆排序扩展题目

已知一个几乎有序的数组，几乎有序是指，如果把数组排好顺序的话，每个元素的距离可以不超过k，并且k相对于数组来说比较小。请选择一个合适的排序算法针对这个数据进行排序。

```java
private static void sort(int[] arr,int k) {
    Queue<Integer> heap = new PriorityQueue<>();
    int index = 0;
    for (;index < Math.min(k,arr.length);index++){
        heap.add(arr[index]);
    }
    int i = 0;
    for (;index<arr.length;i++,index++){
        heap.add(arr[index]);
        arr[i] = heap.poll();

    }
    while (!heap.isEmpty()){
        arr[i++] = heap.poll();
    }
}
```

## 比较器的使用

1. 比较器的实质就是重载比较运算符
2. 比较器可以很好的应用在特殊标准的排序上
3. 比较器可以很好的应用在根据特殊标准排序的结构上

```java
static class AComp implements Comparator<Integer>{
    @Override
    public int compare(Integer o1, Integer o2) {
        return o1-o2;
    }
}
```

1. 如果返回负数，认为第一个参数放在上面
2. 如果返回正数，认为第二个参数应该放在上面
3. 如果返回0，谁都能放在最上面

## 桶排序思想下的排序

1. 计数排序：统计词频率的排序
2. 基数排序

分析：

1. 桶排序思想下的排序都是不基于比较的排序
2. 时间复杂度为O(N)，额外空间复杂度O(M)
3. 应用范围有限，需要样本数据状况满足桶的划分
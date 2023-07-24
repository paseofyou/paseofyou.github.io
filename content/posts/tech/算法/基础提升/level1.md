---
title: "level1"
date: 2023-07-14T23:19:34+08:00
draft: false
weight: 10
---

# 认识复杂度和简单排序算法

## 认识时间复杂度

常数时间的操作

- 常数操作：一个操作如果和样本的数据量没有关系，每次都是固定时间内完成的操作。
- 时间复杂度为一个算法流程中，常数操作数量的一个指标。常用O(读作big 0)来表示。具体来说，先要对一个算法流程非常熟悉，然后去写出这个算法流程中，发生了多少常数操作，进而总结出常数操作数量的表达式。
- 时间复杂度为0(f(N))：在表达式中，只要高阶项，不要低阶项，也不要高阶项的系数，剩下的部分的为f(N)。
- 评价算法流程：先看时间复杂度的指标，然后再分析不同数据样本下的实际运行时间，也就是“常数项时间。

## 选择排序、冒泡排序细节的讲解与复杂度分析

时间复杂度0(N^2)，额外空间复杂度0(1)（只需要有限几个变量就可以排序，不需要额外的数组）

### 选择排序

```java
public static void selectionSort(int Arr[]){
    if(arr == null || arr.length < 2){
        return;
    }
    for(int i = 0; i< arr.length -1; i++){
        int minIndex = i;
        //确定最小值的索引，方便与其交换
        for(int j = i; j< arr.length; j++){
            minIndex = arr[j]<arr[minIndex] ? j : minIndex;
        }
        swap(arr,i,minIndex);
    }
}

public static void swap(int[] arr,int i,int j){
	int tmp = arr[i];
    arr[i]= arr[j];
    arr[j]= tmp;
}
```

### 冒泡排序

```java
public static void bubbleSort(int[] arr){
    if(arr == null || arr.length< 2){
        return;
    }
    for(int e = arr.length-1; e>0; e--){
        for(int i = 0; i<e; i++){
            if(arr[i]> arr[i+1]){
                swap(arr,i,i+1);
            }
        }
    }
}

public static void swap(int[] arr, int i, int j){
    arr[i] = arr[i]^ arr[j];
    arr[j] = arr[i]^ arr[j];
    arr[i] = arr[i]^ arr[j];
}
```

## 插入排序细节的讲解与复杂度分析
时间复杂度0(N^2)，额外空间复杂度0(1)

```java
public static void InsertSort(int[] arr){
    if(arr == null || arr.length< 2){
        return;
    }
    // 0~i-1 已经有序  想使得   0~i有序
    for(int i=1; i<arr.length; i++){
        for(int j = i-1; j>=0 && arr[j]>arr[j+1]; j--){
            swap(arr,j,j+1);
        }
    }
}
```

## 二分法的详解与扩展
1. 在一个有序数组中，找某个数是否存在
2. 在一个有序数组中，找>=某个数最左侧的位置（在第一步的基础上继续二分，找到最靠左的值）
3. 局部最小值问题

练习：在无序数组中，找到局部最小的数

## 异或运算的性质与扩展

1. 0^N == N       N^N == 0
2. 异或运算满足交换律和结合率
3. 不用额外变量交换两个数
4. 一个数组中，有一个数为奇数次，其他为偶数次，找出这个数
5. 一个数组中，有两个数为奇数次，其他为偶数次，找出这两个数

```java
// 一个数组中，有一个数为奇数次，其他为偶数次，找出这个数
private static void work1() {
    int eor = 0;
    for (int curNum : arr2) {
        eor ^= curNum;
    }
    System.out.println(eor);
}
// 一个数组中，有两个数为奇数次，其他为偶数次，找出这两个数
private static void work2() {
    int eor = 0;
    for (int curNum : arr) {
        eor ^= curNum;
    }

    int rightOne = (~eor + 1) & eor;
    int onlyOne = 0;
    for (int curNum : arr) {
        if ((rightOne & curNum) == 0) {
            onlyOne^=curNum;
        }
    }
    System.out.println("a=" + onlyOne + ";b=" + (eor ^ onlyOne));
}
```



## 对数器的概念和使用
意思就是：用一个简单粗暴的方法来验证待测方法是否正确。

1，有一个你想要测的方法a
2，实现复杂度不好但是容易实现的方法b3，实现一个随机样本产生器
4，把方法a和方法b跑相同的随机样本，看看得到的结果是否一样。
5，如果有一个随机样本使得比对结果不一致，打印样本进行人工干预，改对方法a或者方法b
6，当样本数量很多时比对测试依然正确，可以确定方法a已经正确。

```java
//for test
public static void comparator(int[] arr){
    Arrays.sort(arr);
}
//for test
public static int[] generateRandomArray(int maxSize, int maxValue){
	// Math.random()  [0,1)所有的小数，等概率返回一个
    // Math.random()*N [0,N)所有的小数，等概率返回一个
    // (int)(Math.random()*N) [0,N-1]所有的整数，等概率返回一个
    int[] arr = new int[(int)((maxSize + 1) * Math.random())];
    for(int i = 0; i< arr.length; i++){
        arr[i] = (int) ((maxValue + 1) * Math.random()) - (int)((maxValue + 1) * Math.random());
    }
    return arr;
}
//for test
public static void copyArray(int[] arr){
    if(arr==null){
        return null;
    }
    int[] res = new int[arr.length];
    for(int i = 0;i<arr.length;i++){
        res[i] = arr[i]; 
    }
    return res;
}

//for test
public static void main(String[] args){
    int testTime = 5000000;
	int maxSize = 100;
    int maxValue = 100;
	boolean succeed = true;
    for (int i = 0; i < testTime; i++){
        int[] arr1 = generateRandomArray(maxSize，maxValue);
        test(arr1);
        comparator(arr2);
        if (!isEqual(arr1,arr2)){
            succeed = false;
            break;
        }
        System.out.println(succeed ? "Nice!" : "False! ");
        int[] arr = generateRandomArray(maxSize, maxValue);
		printArray(arr);
		test(arr);
        printArray(arr);
    }
}
```


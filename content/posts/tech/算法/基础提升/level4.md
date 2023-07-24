---
title: "level4"
date: 2023-07-21T20:20:34+08:00
draft: false
weight: 10
---

# 链表

## 排序算法的稳定性及其汇总

同样值的个体之间，如果不因为排序而改变相对次序，就是这个排序是有稳定性的；否则就没有。

不具备稳定性的排序：

选择排序（直接交换数字），快速排序（partition交换数字），堆排序（大根堆转换）

具有稳定性的排序：

冒泡排序，插入排序，归并排序、一切桶排序思想下的排序

目前没有找到时间复杂度为O(N*logN)，额外空间复杂度O(1)，又稳定的排序

|            | 时间      | 空间    | 稳定性 |
| ---------- | --------- | ------- | ------ |
| 选择       | O(N^2)    | O(1)    | N      |
| 冒泡       | O(N^2)    | O(1)    | Y      |
| 插入       | O(N^2)    | O(1)    | Y      |
| 归并       | O(N*logN) | O(N)    | Y      |
| 快排（随） | O(N*logN) | O(logN) | N      |
| 堆         | O(N*logN) | O(1)    | N      |

- 基于比较的排序的时间复杂度<O(N*logN)：不行
- 时间复杂度O(N*logN)，并且空间复杂度O(N)以下，且稳定：不行

## 常见的坑

1. 归并排序的额外空间复杂度可以变成O(1)，但非常难，不需要掌握，有兴趣可以搜索：归并排序 内部缓存法

2. “原地归并排序”的帖子都是垃圾，会让归并排序的时间复杂度变成O(N^2)

3. 快速排序可以做到稳定性问题，但是非常难，还会让空间复杂度变为O(N)，不需要掌握，可以搜索：01 stable sort

4. 所有改进都不重要，因为目前没有找到时间复杂度为O(N*logN)，额外空间复杂度为O(1)，又稳定的排序

5. 有一道题目，是奇数放在数组左边，偶数放在数组右边，还要求原始相对次序不变，这个题是论文级别难度

   当奇数放在数组左边，偶数放在数组右边，属于01标准，并且左边的奇数维持稳定性，右边的偶数维持稳定性，但经典快排无法做到稳定性，只有论文级别的快排可以。

## 工程上对排序的改进

1. 充分利用O(N*logN)和O(N^2)排序各自的优势

- 在大样本的调度算法，用快排

- 在小样本的算法，用插入。虽然是O(N^2)，但瓶颈不明显，反而插入的常数项是极低的，所以更快

2. 稳定性的考虑

- 基础类型用快排，非基础类型，使用归并

## 哈希表的简单介绍

1. 哈希表在使用层面上可以理解为一种复合结构
2. 如果只有key，没有伴随数据value，可以使用HashSet结构
3. 如果既有key，又有伴随数据value，可以使用HashMap结构
4. 如果无伴随数据，是HashMap和HashSet唯一的区别；底层的实际结构是一回事
5. 使用哈希表增（put），删（remove），改（put），查（get）的操作，可以认为时间复杂度为O(1)，但是常数时间比较大
6. 放入哈希表的东西，如果是基础类型，内部按值传递，内存占用就是这个东西的大小
7. 放入哈希表的东西，如果不是基础类型，内部按引用传递，内存占用是这个东西内存地址的大小

## 有序表的简单介绍

1. 有序表在使用层面可以理解为一种集合结构
2. 如果只有key，没有伴随数据value，可以使用TreeSet结构
3. 如果既有key，又有伴随数据value，可以使用TreeMap结构
4. 有无伴随数据是TreeSet和TreeMap唯一区别，底层的实际结构是一回事
5. 有序表和哈希表的区别是，有序表把key按照顺序组织起来，而哈希表完全不组织
6. 红黑树，AVL树，size-balance-tree和调表等都属于有序表结构，只是底层具体实现不同
7. 放入哈希表的东西，如果是基础类型，内部按值传递，内存占用就是这个东西的大小
8. 不管是什么底层具体实现，只要是有序表，都有以下固定的基本功能和固定的时间复杂度

## 有序表的固定操作

1. void put(K key, V value)：将一个(key, value)记录加入表中，或者将key的记录更新成value。
2. V get(K key)：根据给定的key，查询value并返回。
3. void remove(K key)：移除key的记录
4. boolen containsKey(K key)：询问是否有关于key的记录。
5. K firstKey()：返回所有键值的排序结果中，最左（最小）的那个。
6. K lastKey()：返回所有键值的排序结果中，最右（最大）的那个。
7. K floor(K key)：如果表中存入过key，返回key；否则返回所有键值对的排序结果中，key的前一个。
8. K ceilingKey(K key)：如果表中存入过key，返回key；否则返回所有键值的排序结果中，key的后一个。

## 单链表的节点结构

```java
Class Node<V>{
	V value;
    Node next;
}
```

由以上结构的节点依次连接起来所形成的链叫单链表结构。

## 双链表的节点结构

```java
Class Node<V>{
    V value;
    Node next;
    Node last;
}
```

由以上结构的节点依次连接起来形成的链叫双链表结构。

单链表和双链表结构都只需要给定一个头部节点head，就可以找到剩下的所有的节点。

## 反转单向和双向链表

【题目】分别实现反转单向链表和反转双向链表的函数

【要求】如果链表长度为N，时间复杂度要求为O(N)，额外空间复杂度要求为O(1)

如果返回反转，有换头操作，应该返回头部，后面连接一系列节点，如`head=f(head)`。

## 打印两个有序链表的公共部分

【题目】给定两个有序链表的头指针head1和head2，打印两个链表的公共部分。

【要求】如果链表的长度之和为N，时间复杂度要求为O(N)，额外空间复杂度要求为O(1)

- 谁小谁移动，相等都移动，谁到头就停

## 面试时链表解题的方法论

1. 对于笔试，不用太在乎空间复杂度，一切为了时间复杂度
2. 对于面试，时间复杂度依然放在第一位，但是一定要找到空间最省的方法。

重要技巧：

1. 额外数据结构记录（哈希表等）
2. 快慢指针（一定要自己线下写熟）

## 判断一个链表是否为回文结构

【题目】给定一个单链表的头节点head，请判断该链表是否为回文结构。

【例子】1->2->1，返回true；1->2->2->1，返回true；15->6->15，返回true；1->2->3，返回false。

【例子】如果链表长度为N，时间复杂度达到O(N)，额外空间复杂度达到O(1)。

存在一个对称轴，就是回文。

笔试：装到栈里，然后弹出对比。

如何确定中间的节点：快慢指针（一定要自己把他写熟），快的一次走两步，慢的走一步。

面试：在中点位置时，把后面的指针逆序，然后两个指针一一对比，相同则把逆序指针复原，再返回。

```java
public class isPalindrome {
public static class Node {
    public int value;
    public Node next;

    public Node(int data) {
        this.value = data;
    }
}

public static boolean isPalindrome1(Node head) {
    Deque<Node> stack = new ArrayDeque<>();
    Node cur = head;
    while (cur != null) {
        stack.push(cur);
        cur = cur.next;
    }
    while (head != null) {
        if (head.value != stack.pop().value) {
            return false;
        }
        head = head.next;
    }
    return true;
}

public static boolean isPalindrome2(Node head) {
    if (head == null || head.next == null) {
        return true;
    }
    Node right = head.next;
    Node cur = head;
    while (cur.next != null && cur.next.next != null) {
        right = right.next;
        cur = cur.next.next;
    }
    Deque<Node> stack = new ArrayDeque<>();
    while (right != null) {
        stack.push(right);
        right = right.next;
    }
    while (!stack.isEmpty()) {
        if (head.value != stack.pop().value) {
            return false;
        }
        head = head.next;
    }
    return true;
}

public static boolean isPalindrome3(Node head) {
    if (head == null || head.next == null) {
        return true;
    }
    //使用快慢指针查找中点
    Node n1 = head;
    Node n2 = head;
    while (n1.next != null && n2.next.next != null) {
        n1 = n1.next;
        n2 = n2.next.next;
    }
    //右半部分逆序
    n2 = n1.next;
    n1.next = null;
    Node n3 = null;
    while (n2 != null) {
        n3 = n2.next;
        n2.next = n1;
        n1 = n2;
        n2 = n3;
    }
    //对比逆序后的节点是否一一匹配
    n3 = n1;
    n2 = head;
    boolean res = true;
    while (n1 != null && n2 != null) {
        if (n1.value != n2.value) {
            res = false;
            break;
        }
        n1 = n1.next;
        n2 = n2.next;
    }
    //复原逆序
    n1 = n3.next;
    n3.next = null;
    while (n1 != null) {
        n2 = n1.next;
        n1.next = n3;
        n3 = n1;
        n1 = n2;
    }
    return res;
}

}
```



## 将单向链表按某值划分为左边小，中间相等，右边大的形式

【题目】给定一个单链表的头节点head，节点的值类型是整形，再给定一个数pivot。实现一个调整链表的函数，将链表调整为左部分都是值小于pivot的节点，中间部分都是值等于pivot的节点，右部分都是值大于pivot的节点。

解：首先创建三对指针，分别指向头节点和尾节点。小于pivot，使得头尾节点都为该节点，后续遍历原节点序列时，遇到相同小于的节点时，把该节点放在头节点的下一位，尾节点更新为此节点。其余等于pivot和大于pivot的操作类似。遍历完源节点序列时，得到三对指针，分别是三串序列，串在一起即可（串在一起时，一定要考虑每对是否为null）。

【进阶】在实现原问题功能的基础上增加如下的要求

- 调整后所有小于pivot的节点之间的相对顺序和调整前一样
- 调整后所有等于pivot的节点之间的相对顺序和调整前一样
- 调整后所有大于pivot的节点之间的相对顺序和调整前一样
- 时间复杂度请达到O(N)，额外空间复杂度请达到O(1)。

```java
public static Node listPartition1(Node head, int pivot) {
    if (head == null) {
        return head;
    }
    Node cur = head;
    int i = 0;
    while (cur != null) {
        i++;
        cur = cur.next;
    }
    Node[] nodeArr = new Node[i];
    for (int j = 0; j < nodeArr.length; i++) {
        nodeArr[j] = cur;
        cur = cur.next;
    }
    arrPartition(nodeArr, pivot);
    for (i = 1; i < nodeArr.length; i++) {
        nodeArr[i - 1].next = nodeArr[i];
    }
    nodeArr[i].next = null;
    return nodeArr[0];
}

public static void arrPartition(Node[] nodeArr, int pivot) {
    int small = -1;
    int big = nodeArr.length;
    int index = 0;
    while (index != big) {
        if (nodeArr[index].value > pivot) {
            swap(nodeArr, index, --big);
        } else if (nodeArr[index].value < pivot) {
            swap(nodeArr, index++, ++small);
        } else {
            index++;
        }
    }
}

public static void swap(Node[] arr, int i, int j) {
    Node tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}

public static Node listPartition2(Node head, int pivot) {
    Node sH = null;
    Node sT = null;
    Node eH = null;
    Node eT = null;
    Node mH = null;
    Node mT = null;
    Node next = null;
    while (head != null) {
        next = head.next;
        head.next = null;
        if (head.value < pivot) {
            if (sH == null) {
                sH = head;
                sT = head;
            } else {
                sT.next = head;
                sT = head;
            }
        } else if (head.value == pivot) {
            if (eH == null) {
                eH = head;
                eT = head;
            } else {
                eT.next = head;
                eT = head;
            }
        } else {
            if (mH == null) {
                mH = head;
                mT = head;
            } else {
                mT.next = head;
                mT = head;
            }
        }
        head = next;
    }
    if (sT != null) {
        sT.next = eH;
        eT = eT == null ? sT : eT;
    }
    if (eT != null) {
        eT.next = mH;
    }
    return sH != null ? sH : (eH != null ? eH : mH);
}
```

## 复制含有随机指针节点的链表

【题目】一种特殊的单链表节点类描述如下：

```java
class Node{
    int value;
    Node next;
    Node rand;
    Node(int val){
        this.value = val;
    }
}
```

rand 指针是单链表节点结构中新增的指针，rand可能指向链表中任何一个节点，也可能指向null。给定一个由Node节点类型组成的无环单链表的头节点head，请实现一个函数完成这个链表的复制，并返回复制的新链表的头节点。

【要求时间复杂度O(N),额外空间复杂度)(1)】

方法一：使用哈希表来复制

```java
public static Node CopyListWithRand(Node head){
    HashMap<Node,Node> map = new HashMap<>();
    Node cur = head;
    while (cur!=null){
        map.put(cur,new Node(cur.value));
        cur = cur.next;
    }
    cur = head;
    while (cur!=null){
        map.get(cur).next = map.get(cur.next);
        map.get(cur).rand = map.get(cur.rand);
        cur = cur.next;
    }
    return map.get(head);
}
```

方法二：创建新节点在老链表中，一对一对的处理

```java
public static Node CopyListWithRand2(Node head) {
    if (head == null) return null;
    Node cur = head;
    Node next = null;
    while (cur != null) {
        next = cur.next;
        cur.next = new Node(cur.value);
        cur.next.next = next;
    }
    cur = head;
    Node curCopy = null;
    while (cur != null) {
        next = cur.next.next;
        curCopy = cur.next;
        curCopy.rand = cur.rand != null ? cur.rand.next : null;
        cur = next;
    }
    Node res = head.next;
    cur = head;
    while (cur != null) {
        next = cur.next.next;
        curCopy = cur.next;
        curCopy.next = next != null ? next.next : null;
        cur = next;
    }
    return res;
}
```


---
title: "level5"
date: 2023-07-25T20:20:34+08:00
draft: false
weight: 10
---

# 二叉树

## 两个单链表相交的一系列问题

【题目】给定两个有环也可能无环的单链表，头节点head1和head2。请实现一个函数，如果两个链表相交，请返回相交的第一个节点。如果不相交，返回null。

快慢指针：快指针不会超过两圈。然后快指针指向开头，此时快慢指针继续前进，他们一定会在入环第一个节点处相遇。

```java
public static Node getLoopNode(Node head) {
    if (head == null || head.next == null || head.next.next == null) {
        return null;
    }
    Node n1 = head.next;
    Node n2 = head.next.next;
    while (n1 != n2) {
        if (n1.next == null || n2.next.next == null) {
            return null;
        }
        n2 = n2.next.next;
        n1 = n1.next;
    }
    n2 = head;
    while (n1 != n2) {
        n1 = n1.next;
        n2 = n2.next.next;
    }
    return n1;
}
```

【要求】如果两个链表长度之和为N，时间复杂度请达到O(N)，额外空间复杂度请达到O(1)。

1. 如果两个链表都无环，则求出两个链表的末尾以及长度，如果末尾不相同，则无相交；若末尾相同，则长度更长的先走差值步，再一起同时走链表，第一次相等则为第一次相遇节点。

```java
public static Node noLoop(Node head1,Node head2){
    if (head1==null|| head2==null){
        return null;
    }
    Node cur1 = head1;
    Node cur2 = head2;
    int n = 0 ;
    while (cur1.next!=null){
        n++;
        cur1 = cur1.next;
    }
    while (cur2.next!=null){
        n--;
        cur2= cur2.next;
    }
    //让cur1锁定在长列表上
    if (cur1!=cur2){
        return null;
    }
    cur1 = n>0?head1:head2;
    cur2 = cur1==head1?head2:head1;
    n = Math.abs(n);
    while (n!=0){
        n--;
        cur1 = cur1.next;
    }
    while (cur1!=cur2){
        cur1=cur1.next;
        cur2=cur2.next;
    }
    return cur1;
}
```

2. 一个链表有环，一个链表无环。不可能出现这种情况。（自己随便脑补，总之不可能出现这种情况）

3. 两个链表都有环。
   1. 两个链表都有独自的环
   2. 入环节点为同一个（即入环节点为同一个，当作两个无环链表处理）
	3. 入环节点是不同的
	```java
	public static Node bothLoop(Node head1, Node loop1, Node head2, Node loop2) {
       Node cur1 = null;
       Node cur2 = null;
       if (loop1 == loop2) {
           cur1 = head1;
           cur2 = head2;
           int n = 0;
           while (cur1 != loop1) {
               n++;
               cur1 = cur1.next;
           }
           while (cur2 != loop2) {
               n--;
               cur2 = cur2.next;
           }
           cur1 = n > 0 ? head1 : head2;
           cur2 = cur1 == head1 ? head2 : head1;
           n = Math.abs(n);
           while (n != 0) {
               n--;
               cur1 = cur1.next;
           }
           while (cur1 != cur2) {
               cur1 = cur1.next;
               cur2 = cur2.next;
           }
           return cur1;
       } else {
           cur1 = loop1.next;
           while (cur1 != loop1) {
               if (cur1 == loop2) {
                   return loop1;
               }
               cur1 = cur1.next;
           }
           return null;
       }
   }
   public static Node getIntersectNode(Node head1, Node head2) {
       if (head1 == null || head2 == null) {
           return null;
       }
       Node loop1 = getLoopNode(head1);
       Node loop2 = getLoopNode(head2);
       if (loop1 == null && loop2 == null) {
           return noLoop(head1, head2);
       }
       if (loop1 != null && loop2 != null) {
           return bothLoop(head1, loop1, head2, loop2);
       }
       return null;
   }
   ```

## 二叉树节点结构

```java
class Node<V>{
    V value;
    Node left;
    Node right;
}
```

用递归和非递归两种方式实现二叉树的先序、中序、后序遍历

如何直观打印一颗二叉树

如何完成二叉树的宽度优先遍历（常见题目：求一颗二叉树的宽度）

1. 递归序列·

```java
public static void f(Node head){
    if(head==null){
        return;
    }
    f(head.left);
    f(head.right);
}
```

2. 先序（只在第一次来到节点才打印这个值）、中序（只在第二次来到节点才打印这个值）、后序（只在第三次来到节点才打印这个值）

```java
public static void preOrderRecur(Node head){
    if(head==null){
        return;
    }
    System.out.println(head.value);
    preOrderRecur(head.left);
    preOrderRecur(head.right);
}
public static void inOrderRecur(Node head){
    if(head==null){
        return;
    }
    inOrderRecur(head.left);
    System.out.println(head.value);
    inOrderRecur(head.right);
}
public static void posOrderRecur(Node head){
    if(head==null){
        return;
    }
    posOrderRecur(head.left);
    posOrderRecur(head.right);
    System.out.println(head.value);
}
```

3. 非递归序列（就是自己压栈）
- 先序遍历
    1. 从栈中弹出一个节点cur
    2. 打印处理cur
    3. 先压右后压左（如果有的话）
    4. 返回第一步，周而复始，直到所有节点用完


```java
	public static void preOrderUnRecur(Node head) {
	if (head != null) {
	    Deque<Node> stack = new ArrayDeque<>();
	    stack.add(head);
	    while (!stack.isEmpty()) {
	        head = stack.pop();
	        System.out.print(head.value + " ");
	        if (head.right != null) {
	            stack.push(head.right);
	        }
	        if (head.left != null) {
	            stack.push(head.left);
	        }
	    }
	}
	System.out.println();
	}
```

- 后序遍历
    1. 从栈中弹出一个节点cur
    2. cur放入收集栈
    3. 先压左后压右
    4. 返回第一步，周而复始，直到所有节点用完
    5. 把收栈弹出到结果栈中（将收栈逆序）

```java
public static void posOrderUnRecur(Node head){
    if (head!=null){
        Deque<Node> s1 = new ArrayDeque<>();
        Deque<Node> s2 = new ArrayDeque<>();
        s1.push(head);
        while (!s1.isEmpty()){
            head = s1.pop();
            s2.push(head);
            if (head.left!=null){
                s1.push(head.left);
            }
            if (head.right!=null){
                s1.push(head.right);
            }
        }
        while (!s2.isEmpty()){
            System.out.print(s2.pop().value+" ");
        }
    }
    System.out.println();
}
```

- 中序遍历
  1. 每个子树整个颗树左边界进栈
  2. 依次弹的过程中，打印
  3. 对弹出节点的右树周而复始 
---
title: 代码随想录算法训练营第三天 | 链表Part01
author: JunZhe
copyright: true
mathjax: true
date: 2025-05-19 15:37:16
tags:
  - 数组
  - 算法
categories: 代码随想录
abbrlink: codecamp-day3-linkedlist
---

## 链表理论基础

我突然在想为什么新建链表节点必须用 new ListNode()，而不能直接用 ListNode()呢？
因为链表是动态分配的，new ListNode()会在堆上分配内存，而 ListNode()是在栈上分配内存。栈上的变量在函数结束后会被自动销毁，而堆上的变量需要手动释放。  
如果用 ListNode()，这个函数结束了会自动销毁变量，造成悬空指针，而链表一般需要全局区调用，所以不能放在栈上。

理解了这个点，这对于内存的堆空间和栈空间应该就更明白了

## LeetCode203.移除链表元素

[题目链接：203.移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/description/)

### 题目要点与解题思路

这是非常基础的链表删除操作，不是很想展开讲了，只需要记住下面几点：

- 建议使用 dummy 节点，避免处理头节点的特殊情况
- 删除节点只需要用到一个 cur 指针，cur-> next = cur->next->next; 这样就可以了
- 别忘记 delete dummy 和要删除的节点

### 实现代码

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy = new ListNode(-1, head);
        ListNode* cur = dummy;
        ListNode* tmp; // 用于删除节点
        while (cur->next) {
            if (cur->next->val == val) {
                tmp = cur->next;
                cur->next = cur->next->next;
                delete tmp;
            } else {
                cur = cur->next;
            }
        }
        head = dummy->next;
        delete dummy;
        return head;
    }
};
```

删除本身操作的复杂度是$O(1)$，但是我们需要遍历链表找到 val，所以时间复杂度是$O(n)$，空间复杂度是$O(1)$

### 遇到的问题与总结

一开始写的时候还用了 prev 指针，不过其实只需要用一个 cur 指针就行（tmp 用于暂存不计入指针数目）。后面见到删除链表的题目会使用双指针的

## LeetCode707.设计链表

[题目链接：707.设计链表](https://leetcode.cn/problems/design-linked-list/description/)

> 简单看了一下代码随想录的答案，自己没写，先留个坑

## LeetCode206.反转链表

[题目链接：206.反转链表](https://leetcode.cn/problems/reverse-linked-list/description/)

### 题目要点与解题思路

- 需要原地的反转
- 使用双指针
- 本题不需要 dummy 节点

模拟过程如下，很清楚了不再赘述(我大一学的时候没有看代码随想录，一直就没搞清这个问题，捂脸)，现在是彻彻底底搞懂了
![](https://file1.kamacoder.com/i/algo/206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.gif)

### 实现代码

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* cur = head;
        ListNode* prev = nullptr;
        ListNode* tmp;

        while(cur){
            tmp=cur->next;
            cur->next=prev;
            prev=cur;
            cur=tmp;
        }
        return prev;
    }
};
```

每次要把 cur->next 用 tmp 存住，好让 cur 往前走
有没有发现这个特别像交换两个数的逻辑 swap(a, b)？

### 遇到的问题与总结

反转链表就用**双指针**！

## 参考资料

[代码随想录-反转链表](https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html)

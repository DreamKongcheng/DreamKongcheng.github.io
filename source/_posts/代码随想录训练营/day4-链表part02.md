---
title: 代码随想录算法训练营第四天 | 链表Part02
author: JunZhe
copyright: true
mathjax: true
date: 2025-05-19 23:28:11
tags:
  - 数组
  - 算法
categories: 代码随想录
abbrlink: codecamp-day4-linkedlist
---

## LeetCode24.两两交换链表中的节点

[题目链接：24.两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/description/)

### 题目要点与解题思路

这题考察的是模拟，因为在操作的时候一些链会断开，所以一定要想清楚如何暂存节点，并且本题适合用 dummy 处理，因为 head 没有人指着，和后面的逻辑有所不同

![](https://file1.kamacoder.com/i/algo/24.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B91.png)

我的解法是步骤 3-步骤 2-步骤 1，代码如下：

### 实现代码

```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummy = new ListNode(-1, head);
        ListNode* cur = dummy;
        ListNode* tmp;
        while (cur && cur->next && cur->next->next) {
            tmp = cur->next->next; // 存下2号，因为1-2断开变成1-3
            cur->next->next = cur->next->next->next; // 步骤三，实现1-3
            tmp->next = cur->next;                   // 步骤二
            cur->next = tmp;                         // 步骤一
            cur = cur->next->next; // 走到下一个要交换的节点，即2（此时的2不就是相当于3的dummy吗？）
        }
        head = dummy->next;
        delete dummy;
        return head;
    }
};
```

- 时间复杂度$O(n)$
- 空间复杂度$O(1)$

- 通过使用 dummy 统一了处理头结点和处理后续节点的问题

- 注意 while 的条件，必须要有两个节点可以交换，所以要有 cur->next 和 cur->next->next（我多写了个 cur，其实 cur 是一定被保证的）

### 遇到的问题与总结

模拟起来比较麻烦，注意保存被断开的节点

## LeetCode19.删除链表的倒数第 N 个结点

[题目链接：19.删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/description/)

### 题目要点与解题思路

链表不可以随机访问，所以看起来倒数第几个有点难以定位，第一次做会想是不是要先遍历一遍链表，得到长度，然后再遍历（长度- n） 下来确定删除的位置

其实可以用双指针来解决（快慢指针），让快指针先跑，等快指针跑到最后一个节点的时候，慢节点就正好在要删除的节点的前一个节点上

### 实现代码

```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(-1, head);
        ListNode *fast = dummy, *slow = dummy;
        while (n--) {
            fast = fast->next;
        }
        while (fast->next) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        head = dummy->next;
        delete dummy;
        return head;
    }
};
```

- 时间复杂度$O(n)$
- 空间复杂度$O(1)$

### 遇到的问题与总结

想到快慢指针就行，看到“链表倒数第几个”这样的内容就可以考虑快慢指针了

## LeetCode 面试题 02.07.链表相交

[题目链接：面试题 02.07.链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/description/)

### 题目要点与解题思路

只能说这道题实在是太巧了，这哪是算法题，这妥妥的脑筋急转弯！！

先讲常规解法，非常简单，先遍历一遍链表 A，得到长度，然后遍历一遍链表 B，得到长度，然后让长的链表先走（长度差），然后两个链表一起走，直到相遇

但是其实有一个很巧妙的解法，来自 leetcode-cn 的题解：[面试题 02.07. 链表相交（双指针，清晰图解）](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/solutions/1190240/mian-shi-ti-0207-lian-biao-xiang-jiao-sh-b8hn/)

![](https://pic.leetcode-cn.com/1615224578-EBRtwv-Picture1.png)

指针 A,B 分别从链表 A 和 B 的头节点出发，走到链表的尾部，然后指向另一个链表的头节点，继续走到尾部，如果在公共节点相遇，则他们走的路径是相同的，所以相遇的节点就是交点，原理证明如下：

- A 走到尾部再去 B 的头部开始走，总长度为
  $$a+(b-c)$$

- B 走到尾部再去 A 的头部开始走，总长度为
  $$b+(a-c)$$

所以两者走的路一样，会重合，分为如下两种：

- 如果有交点，即 c>0，两个指针同时指向公共交点
- 如果没有交点，即 c=0，两个指针同时指向 NULL

### 实现代码

#### 常规解法

```cpp
class Solution {
    class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* curA = headA;
        ListNode* curB = headB;
        int lenA = 0, lenB = 0;
        while (curA != NULL) { // 求链表A的长度
            lenA++;
            curA = curA->next;
        }
        while (curB != NULL) { // 求链表B的长度
            lenB++;
            curB = curB->next;
        }
        curA = headA;
        curB = headB;
        // 让curA为最长链表的头，lenA为其长度
        if (lenB > lenA) {
            swap (lenA, lenB);
            swap (curA, curB);
        }
        // 求长度差
        int gap = lenA - lenB;
        // 让curA和curB在同一起点上（末尾位置对齐）
        while (gap--) {
            curA = curA->next;
        }
        // 遍历curA 和 curB，遇到相同则直接返回
        while (curA != NULL) {
            if (curA == curB) {
                return curA;
            }
            curA = curA->next;
            curB = curB->next;
        }
        return NULL;
    }
};
};
```

这个是卡哥的解法，比较常规，时间复杂度$O(a+b)$，空间复杂度$O(1)$

#### 巧妙解法

```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *a = headA, *b = headB;
        while( a != b) {
            a = a != nullptr ? a->next : headB;
            b = b != nullptr ? b->next : headA;
        }
        return a;
    }
};
```

- 时间复杂度$O(a+b)$
- 空间复杂度$O(1)$

### 遇到的问题与总结

这道题的巧妙解法是真的挺有意思的，感觉是一个脑筋急转弯的题目，常规解法也很简单，面试遇到肯定还是追求先写常规解法

另外我在二刷的时候一直遇到一个 bug，代码如下

```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *a = headA, *b = headB;
        while (a != b) {
            a = a->next;
            if (a == NULL) a = headB;
            b = b->next;
            if (b == NULL) b = headA;
        }
        return a;
    }
};
```

这样相当于我提前把 a 跳转到了 headB，会导致两者遇不上（正确的代码会在 null 上停留一轮），考虑如下情景：**链表没有交点**

交换过后，两者应该同时到了 null，但是一达到 null 就跳转了，导致两者变成了 headB 和 headA，会一直遇不到导致死循环

## LeetCode142.环形链表 II

[题目链接：142.环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/description/)

> 一刷被震撼到，二刷还是没一下子想出来，我先放一下

## 参考资料

[代码随想录-两两交换链表中的节点](https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[面试题 02.07. 链表相交（双指针，清晰图解）](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/solutions/1190240/mian-shi-ti-0207-lian-biao-xiang-jiao-sh-b8hn/)
[代码随想录-链表相交](https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html#%E6%80%9D%E8%B7%AF)
[代码随想录-环形链表 II](https://programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html)

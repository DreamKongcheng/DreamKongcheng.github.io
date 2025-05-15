---
title: 代码随想录算法训练营第一天 | 数组Part01
author: JunZhe
tags:
  - 数组
  - 算法
categories: 代码随想录
mathjax: true
abbrlink: codecamp-day1-arrays
date: 2025-05-14 22:51:20
---

# LeetCode704.二分查找
[题目链接：704.二分查找](https://leetcode.cn/problems/binary-search/description/)

## 题目要点与解题思路
首先我们明确一下二分查找的条件：
1.  数组是有序的
2.  数组中没有重复元素（否则返回的下标可能会不唯一）

然后要注意二分查找的边界条件，有两种写法，左闭右开和左闭右闭，我是用的左闭右闭的写法。

<!--more-->

## 实现代码
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        int mid;
        while (left <= right) {
            mid = (left + right) / 2;
            if (target > nums[mid]) {
                left = mid + 1;
            } else if (target < nums[mid]) {
                right = mid - 1;
            } else {
                return mid;
            }
        }
        return -1;
    }
};
```
- 时间复杂度O(logn)
- 空间复杂度O(1)


## 遇到的问题与总结
注意两个地方：
1.  `left <= right`，这个是二分查找的条件，左闭右闭中是小于等于
2.  `else if (target < nums[mid])` right = mid - 1;


# LeetCode27.移除元素
[题目链接：27.移除元素](https://leetcode.cn/problems/remove-element/description/)

## 题目要点与解题思路
乍一看会想到用两层for循环，第一层检测要删除的元素，第二层是一个个位移填补空缺，这样是$O(n^2)$的时间复杂度

我们希望能优化到$O(n)$，此时容易想到双指针

双指针法（快慢指针法）： 通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。
- 快指针：寻找符合条件的元素位置
- 慢指针：定位更新的位置

这样讲有点抽象，直接看代码

## 实现代码
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slow = 0;
        for (int fast = 0; fast < nums.size(); fast++) {
            if (nums[fast] != val) {
                nums[slow] = nums[fast];
                slow++;
            }
        }
        return slow;
    }
};
```
- 时间复杂度O(n)
- 空间复杂度O(1)

当fast发现元素不是val的时候，会把现在的fast赋给现在的slow，并且slow也往前进。如果fast指向要删除的元素，就会把fast只会管自己往前走，此时slow就停下来了，等待下一个fast指向的非val的元素

## 遇到的问题与总结
第一次遇到想不到用双指针

本题是双指针的经典应用，很多数组问题中都可以使用双指针进行优化，必须很清楚两个指针都代表什么含义



# LeetCode977.有序数组的平方
[题目链接：977.有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/description/)

## 题目要点与解题思路
想要在O(n)的时间复杂度内完成这个题目，我们可以使用双指针法。
平方其实是个二次函数，最大的值会出现在两端，所以可以用左右两个指针不断向中间进行遍历，然后开辟一个新的数组，从后往前接住两个指针中较大的值的平方。


## 实现代码
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> result(nums.size());
        int k=nums.size()-1;
        for(int i=0,j=k;i<=j;){
            if(nums[i]*nums[i]<nums[j]*nums[j]){
                result[k--]=nums[j]*nums[j];
                j--;
            }else{
                result[k--]=nums[i]*nums[i];
                i++;
            }
        }
        return result;
    }
};
```
- 时间复杂度O(n)
- 空间复杂度O(n)

## 遇到的问题与总结
注意i<=j，如果没有等号，此位置的元素会被遗漏而没有填入到result中。

# 今日总结
今天是代码随想录训练营打卡第一天，温故了一下前段时间做的题目，很有收获！

# 参考资料
[代码随想录-二分查找](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html)
[代码随想录-移除元素](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html)
[代码随想录-有序数组的平方](https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html)
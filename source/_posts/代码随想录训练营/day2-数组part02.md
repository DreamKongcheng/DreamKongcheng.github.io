---
title: 代码随想录算法训练营第二天 | 数组Part02
author: 濬哲
copyright: true
mathjax: true
date: 2025-05-15 20:30:32
tags:
  - 数组
  - 算法
categories: 代码随想录
abbrlink: codecamp-day2-arrays
---

## LeetCode209.长度最小的子数组

[题目链接：209.长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/description/)

### 题目要点与解题思路

#### 暴力解法

不难想到暴力解法，时间复杂度是$O(n^2)$，就是以每一个元素为起始位置，然后往下看，直到找到满足要求的子数组。这种情况下结束位置会被反复遍历

#### 滑动窗口

滑动窗口就是不断调节起始位置和终止位置，然后找到满足要求的子数组
在暴力循环中，一个 for 遍历起始位置，一个 for 遍历结束位置，结束位置是从每个起始位置开始枚举

我们思考能否用一个 for 循环来解决这个问题：
首先应该表示起始位置还是终止位置呢？ 答案是终止位置，因为如果是起始位置的话一定会落入重复遍历终止位置的困境
我们移动终止位置，不断增长窗口，当窗口内的元素和大于等于目标值时，开始移动起始位置，直到窗口内的元素和小于目标值为止

![](https://file1.kamacoder.com/i/algo/209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.gif)

<!--more-->

### 实现代码

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int i = 0; // 滑动窗口起始位置
        int sum = 0; // 滑动窗口内元素和
        int subLength = 0;  // 滑动窗口长度
        int result = INT32_MAX;
        for(int j = 0; j < nums.size(); j++){
            sum += nums[j];
            while(sum >= target){
                subLength = j - i + 1;
                result = result > subLength ? subLength : result;
                sum -= nums[i];
                i++;
            }
        }
        return result == INT32_MAX ? 0 : result;
    }
};
```

- 时间复杂度$O(n)$
- 空间复杂度$O(1)$

```cpp
subLength = j - i + 1;
result = result > subLength ? subLength : result;
```

注意这两个语句的位置，思考为什么是放在 while 的最前面，我二刷有点背答案了，把他放到 while 后面去了，写的时候没有理清逻辑，debug 了几次才过
当 sum 一大于 target 的时候就要进行记录!

### 遇到的问题与总结

二刷的时候没有完全理清逻辑，以后要避免纯背答案
发现一个规律，很多关于“子”的问题，比如子数组，子字符串等问题的时候，都应该想一想滑动窗口的方法

## LeetCode59. 螺旋矩阵 II

[题目链接：59.螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/description/)

### 题目要点与解题思路

这道题没什么算法，主要考察的是模拟过程和对代码的掌控力

代码随想录里面的解法比较繁琐，我自己采用了收缩边界的方法，个人觉得是这道题最实用的方法

### 实现代码

```cpp
lass Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int up = 0, down = n - 1, left = 0, right = n - 1;
        int count = 1;
        vector<vector<int>> vec(n, vector<int>(n, 0));
        while (1) {
            for (int i = left; i <= right; i++) vec[up][i] = count++;
            if (++up > down) break;
            for (int i = up; i <= down; i++) vec[i][right] = count++;
            if (--right < left) break;
            for (int i = right; i >= left; i--) vec[down][i] = count++;
            if (--down < up) break;
            for (int i = down; i >= up; i--) vec[i][left] = count++;
            if (++left > right) break;
        }
        return vec;
    }
};
```

- 时间复杂度$O(n^2)$
- 空间复杂度$O(1)$

这个方法巧妙在每次收缩边界，让代码保持了非常统一的风格，能很好的规避一些边界值的 bug

### 遇到的问题与总结

这道题知道使用边界收缩的方式基本就简单了，没啥问题

## KamaCoder58. 区间和

[题目链接：58. 区间和](https://kamacoder.com/problempage.php?pid=1070)

### 题目要点与解题思路

这道题看起来很简单，但是很容易超时，解决方法是使用**前缀和**

前缀和的思想是重复利用计算过的子数组之和，从而降低区间查询需要累加计算的次数。

前缀和在涉及计算区间和的问题时非常有用！

### 实现代码

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> arr(n,0);
    vector<int> p(n, 0);
    int presum = 0;
    for (int i = 0; i < n; i ++) {
        cin >> arr[i];
        presum += arr[i];
        p[i] = presum;
    }
    int a, b;

    while (cin >> a >> b) {
        int sum = 0;

        if (a == 0) sum = p[b];
        else sum = p[b] - p[a - 1];
        std::cout << sum << std::endl;
    }
}
```

### 遇到的问题与总结

以后见到区间和的问题就要想到前缀和

## 今日总结

今天的几道题都是一刷不大能想到的，重点在于积累思想，以后看到类似的题目都能想到他们对映的解法就行。二刷总体感觉是可以的，就是要更加深对思维逻辑的理解，不要死记硬背

## 参考资料

[代码随想录-长度最小的子数组](https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[代码随想录-区间和](https://programmercarl.com/kamacoder/0058.%E5%8C%BA%E9%97%B4%E5%92%8C.html)

## 数组部分总结

数组部分已经结束了，收获很大，主要是下面几个方面：

- 二分查找：注意统一写法左闭右开 or 左闭右闭
- 双指针：简化暴力解法
- 滑动窗口：“子”问题
- 模拟行为：想清楚边界和每一步
- 前缀和：区间求和

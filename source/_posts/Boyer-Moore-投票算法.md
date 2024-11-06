---
title: Boyer-Moore 投票算法
date: 2024-11-06 22:15:36
tags: 计数类算法，贪心算法
categories: 算法
---

### 一、算法原理

1. **核心思想**：通过不断抵消不同元素找到可能的多数元素，因多数元素出现次数大于数组长度一半，被不同元素抵消后最终剩下的元素很可能是多数元素。
2. **具体步骤**：
   - 初始化候选元素为任意值，计数器为 0。
   - 遍历数组，若计数器为 0，将当前元素设为候选元素并计数器加 1；若计数器不为 0 且当前元素与候选元素相同，计数器加 1，不同则计数器减 1。
   - 遍历结束后需再次遍历数组验证候选元素是否为多数元素。

### 二、示例代码

```java
public class BoyerMooreVoting {
    public static int majorityElement(int[] nums) {
        int candidate = nums[0];
        int count = 1;
        for (int i = 1; i < nums.length; i++) {
            if (count == 0) {
                candidate = nums[i];
                count = 1;
            } else if (nums[i] == candidate) {
                count++;
            } else {
                count--;
            }
        }
        // 验证 candidate 是否为多数元素
        count = 0;
        for (int num : nums) {
            if (num == candidate) {
                count++;
            }
        }
        return count > nums.length / 2? candidate : -1;
    }

    public static void main(String[] args) {
        int[] nums = {2, 2, 1, 1, 1, 2, 2};
        int majority = majorityElement(nums);
        if (majority!= -1) {
            System.out.println("多数元素是：" + majority);
        } else {
            System.out.println("数组中不存在多数元素");
        }
    }
}
```

### 三、算法优势

1. **时间复杂度低**：对数组进行两次遍历，时间复杂度为 O(n)，处理大规模数据效率高。
2. **空间复杂度低**：只需常数级别额外空间存储候选元素和计数器，空间复杂度为 O(1)。

### 四、应用场景

1. **数据集中多数元素的查找**：在选举统计、数据分析等场景快速找出出现次数超过一半的元素。
2. **数据验证和错误检测**：利用多数元素特性进行数据验证，若未找到多数元素可能存在数据错误或异常情况。
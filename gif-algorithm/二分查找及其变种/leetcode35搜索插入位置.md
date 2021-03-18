### leetcode35搜索插入位置

#### 题目描述

> 给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
>
> 你可以假设数组中无重复元素。

示例 1:

> 输入: [1,3,5,6], 5
> 输出: 2

示例 2:

> 输入: [1,3,5,6], 2
> 输出: 1

示例 3:

> 输入: [1,3,5,6], 7
> 输出: 4

示例 4:

> 输入: [1,3,5,6], 0
> 输出: 0

#### 题目解析

这个题目完全就和咱们的二分查找一样，只不过有了一点改写，那就是将咱们的返回值改成了 left，具体实现过程见下图

![搜索插入位置](https://img-blog.csdnimg.cn/img_convert/d806cb5199c4baeebc62bebe29d7eded.gif)

#### 题目代码

```java
class Solution {
    public int searchInsert(int[] nums, int target) {

        int left = 0, right = nums.length-1;
        //注意循环条件
        while (left <= right) {
            //求mid
            int mid = left + ((right - left ) >> 1);
            //查询成功
            if (target == nums[mid]) {
                return mid;
            //右区间    
            } else if (nums[mid] < target) {
                left = mid + 1;   
            //左区间               
            } else if (nums[mid] > target) {
                right = mid - 1;
            }
        }
        //返回插入位置
        return left;
    }
}
```




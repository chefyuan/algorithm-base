> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [35. 搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)

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

Java Code:

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

Go Code:

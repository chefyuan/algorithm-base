> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

# **不完全有�?**

## **查找�?标元素（不含重�?�元素）**

之前我们说二分查找需要在完全有序的数组里使用，那么不完全有序时可以用吗？

例：

![](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/案例1.2wan88b4sdk0.png)

上面的新数组虽然不是完全有序，但�?也可以看成是由一�?完全有序的数组翻折得到的。或者可以理解成两个有序数组，且�?二个数组的最大值小于�??一的最小值，我们将其拼接，拼接成了一�?不完全有序的数组，在这个数组�?我们需要找�? target ，找到后返回其索引，如果没有找到则返�? -1�?

我们�?一次看到这种�?�目时，�?能会想到，我�?�?需要挨�?遍历就好啦，发现后返回索引即�?，这样做当然�?�?以滴，那么我�?�?不可以使用二分查找呢�?

下面我们看一下解决�?��?�的具体思路�?

首先我们设想一�? mid 值会落到�?里，我们一起来想一下�?

�?不是�?有两种情况，�? left 在一�?数组，同时落�? 数组 1 或同时在 数组 2，或者不在一�?数组�? left 在数�? 1，mid 在数�? 2。想到这里咱�?这个题目已经完成一半了�?

![mid值情况](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/mid值情�?.3879bq8s3xk0.png)

那么我们先来思考一下，？我�?�?以根�? nums[mid] �? nums[left] 判断，是因为我们�? mid 一定是会落�? left �? right 之间，那如果 nums[mid] >= nums[left] 时，说明他俩落在一�?数组里了，�?�果 nums[mid] < nums[left] 时，说明他俩落在了不同的数组，�?�时 left 在数�? 1 mid 在数�? 2.

�?：left �? mid 落在同一数组时，不能�? left �? 数组 2 ，mid �? 数组 1 �?？因为咱�?�? mid �?通过 left �? right 的下标求得，所以应该在 left �? right �?�?

如果我们�? mid �? left 在同一�?数组内时？咱�?�? target 会有几�?�情况呢？我�?通过都落�? 数组 1 举例�?

![left�?](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/left�?.6kl90uroee40.png)

无非也是两�?�情况，用我�?上面的例子来说，

1.**落在 mid 的左�?**，当前例子中 情况�?落在 [4,7）区间内，即 4 <= target < 7 ，也就是 target >= nums[left] && target < nums[mid]，�?�时我们�? right = mid -1，�?? left �? right 都落到数�? 1 �?，下次查找我�?就是在数�? 1 �?进�?�了，完全有序，

2.**落在 mid 的右�?**，�?�时例子�? target 不落�? [4,7）区间内，那�? target = 8 �? 0 <= target <= 2 （�?�时我们�? target 均小�? nums[left]�? 两�?�情况，也就�? target > nums[mid] || target < nums[left] 此时我们�? left = mid + 1 即可，也�?为了慢慢�? left �? right 指针赶到一�?有序数组内�?

那我�?在来思考一下当 mid 值落�? **数组 2** �?时，target 会有几�?�情况呢？其实和上面的例子思路一致，情况相反而已�?

![right右](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/right�?.3yvrwxloi3c0.png)

1. target <= nums[right] && target > nums[mid]

   > 这里和上面的对应，�?�时的情况就�?整个落在右半部分，我�?下�?�就�?以在数组 2 内进行查找�?

2. target > nums[right] || target < nums[mid]

   > 这里就是和上面的�?二�?�情况�?�应，落�? mid 的左半部分，我们尽量将两�?指针赶到一�?

希望我的表达能�?��?�大家�?�这�?变�?�理解透彻，�?�果没能让各位理解，或者有表达不当的地方�?�迎各位批评指�?�。然后我�?一起来做一�? leetcode 33 题吧�?

#### [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

#### 题目描述

给你一�?整数数组 nums ，和一�?整数 target �?

该整数数组原�?�?按升序排列，但输入时在�?�先�?知的某个点上进�?�了旋转。（例�?�，数组 [0,1,2,4,5,6,7] �?能变�? [4,5,6,7,0,1,2] ）�?

请你在数组中搜索 target ，�?�果数组�?存在这个�?标值，则返回它的索引，否则返回 -1 �?

示例 1�?

> 输入：nums = [4,5,6,7,0,1,2], target = 0
> 输出�?4

示例 2�?

> 输入：nums = [4,5,6,7,0,1,2], target = 3
> 输出�?-1

示例 3�?

> 输入：nums = [1], target = 0
> 输出�?-1

#### 题目解析

这个题目的解答方法，咱们在上面已经有所描述，下面我�?来看一下下面这�?例子的代码执行过程吧.

> 输入 nums = [4,5,6,7,8,0,1,2] target = 8

下面我们看�?�目代码吧，如果还没有完全理解的同�?�，�?以仔细阅�? if ，else if 里面的�??句，还有注释，一定可以整透的�?

#### 题目代码

```java
class Solution {
    public int search(int[] nums, int target) {
        //左右指针
        int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            int mid = left+((right-left)>>1);
            if (nums[mid] == target) {
                return mid;
            }
            //落在同一数组的情况，同时落在数组1 �? 数组2
            if (nums[mid] >= nums[left]) {
                //target 落在 left �? mid 之间，则移动我们的right，完全有序的一�?区间内查�?
                if (nums[mid] > target && target >= nums[left]) {
                       right = mid - 1;
                // target 落在right�? mid 之间，有�?能在数组1�? 也有�?能在数组2
                } else if (target > nums[mid] || target < nums[left]) {
                       left = mid + 1;
                }
            //不落在同一数组的情况，left 在数�?1�? mid 落在 数组2
            }else if (nums[mid] < nums[left]) {
                //有序的一段区间，target �? mid �? right 之间
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                // 两�?�情况，target 在left �? mid 之间
                } else if (target < nums[mid] || target > nums[right]) {
                    right = mid - 1;
                }
            }
        }
        //没有查找�?
        return -1;

    }
}
```

Go Code:

```go
func search(nums []int, target int) int {
    l, r := 0, len(nums) - 1
    for l <= r {
        m := (l + r) / 2
        if target == nums[m] {
            return m
        }
        // 先判�?�?边是有序�?
        if nums[m] < nums[r] {
            // 再判断target在左右哪�?
            if target > nums[m] && target <= nums[r] {
                l = m + 1
            } else {
                r = m - 1
            }
        } else {
            if target < nums[m] && target >= nums[l] {
                r = m - 1
            } else {
                l = m + 1
            }
        }
    }
    return -1
}
```

## 

> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

## 查找元素�?一�?位置和最后一�?位置

上面我们说了如何使用二分查找在数组或区间里查出特定值的索引位置。但�?我们刚才数组里面都没有重复值，查到返回即可，那么我�?思考一下下面这种情�?

![二分查找变�?�一](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/二分查找变�?�一.3axfe8rq0ei0.png)

此时我们数组里含有�?�个 5 ，我�?查�?�是否含�? 5 �?以很容易查到，但�?我们想获取�??一�? 5 �? 最后一�? 5 的位�?应�?�怎么实现�?？哦！我�?�?以使用遍历，当查询到�?一�? 5 时，我们设立一�?指针进�?�定位，然后到达最后一�? 5 时返回，这样我们就能求的�?一�?和最后一�?五了？因为我�?这个文章的主题就�?二分查找，我�?�?不可以用二分查找来实现呢？当然是�?以的�?

#### [34. 在排序数组中查找元素的�??一�?和最后一�?位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

#### 题目描述

> 给定一�?按照升序排列的整数数�? nums，和一�?�?标�? target。找出给定目标值在数组�?的开始位�?和结束位�?�?
>
> 如果数组�?不存在目标�? target，返�? [-1, -1]�?

示例 1�?

> 输入：nums = [5,7,7,8,8,10], target = 8
> 输出：[3,4]

示例 2�?

> 输入：nums = [5,7,7,8,8,10], target = 6
> 输出：[-1,-1]

示例 3�?

> 输入：nums = [], target = 0
> 输出：[-1,-1]

#### 题目解析

这个题目很�?�易理解，我�?在上面�?�了如何使用遍历解决该�?�，但是这个题目的目的就�?让我�?使用二分查找，我�?来逐个分析，先找出�?标元素的下边界，那么我们如何找到�?标元素的下边界呢�?

我们来重点分析一下刚才二分查找中的这段代�?

```java
  if (nums[mid] == target) {
       return mid;
  }else if (nums[mid] < target) {
      //这里需要注意，移动左指�?
      left  = mid + 1;
  }else if (nums[mid] > target) {
      //这里需要注意，移动右指�?
      right = mid - 1;
  }
```

我们�?需在这段代码中�?改即�?，我�?再来剖析一下这块代码，nums[mid] == target 时则返回，nums[mid] < target 时则移动左指针，在右区间进�?�查找， nums[mid] > target 时则移动右指针，在左区间内进行查找�?

那么我们思考一下，如果此时我们�? nums[mid] = target ,但是我们不能�?�? mid �?否为该目标数的左边界，所以�?�时我们不可以返回下标。例如下面这种情况�?![二分查找下边界](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/二分查找下边�?.m9m083jempc.png)

此时 mid = 4 ，nums[mid] = 5,但是此时�? mid 指向的并不是�?一�? 5，所以我�?需要继�?查找 ，因为我�?要找

的是数的下边界，所以我�?需要在 mid 的值的左区间继�?寻找 5 ，那我们应�?�怎么做呢？我�?�?需�?

target <= nums[mid] 时，�? right = mid - 1 即可，这样我�?就可以继�?�? mid 的左区间继续�? 5 。是不是�?着有点绕，我们通过下面这组图进行描述�?

![左边�?1](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/左边�?1.5o2ihokjfg80.png)

![左边�?2](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/左边�?2.5wazlfm298s0.png)

其实原理很简单，就是我们将小于和等于合并在一起�?�理，当 target <= nums[mid] 时，我们都移动右指针，也就是 right = mid -1，还有一�?需要注意的就是，我�?计算下边界时最后的返回值为 left ，当上图结束�?�?时，left = 3，right = 2，返�? left 刚好时我�?的下边界。我�?来看一下求下边界的具体执�?�过程�?

**动图解析**

![二分查找下边界](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/二分查找下边�?.u1cidx99yio.gif)

```java
int lowerBound(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            //这里需要注意，计算mid
            int mid = left + ((right - left) >> 1);
            if (target <= nums[mid]) {
                //当目标值小于等于nums[mid]时，继续在左区间检�?，找到�??一�?�?
                right = mid - 1;

            }else if (target > nums[mid]) {
                //�?标值大于nums[mid]时，则在右区间继�?检�?，找到�??一�?等于�?标值的�?
                left = mid + 1;

            }
        }
        return left;
    }
```

计算上边界时算是和�?�算上边界时条件相反�?

计算下边界时，当 target <= nums[mid] 时，right = mid -1；target > nums[mid] 时，left = mid + 1�?

计算上边界时，当 target < nums[mid] 时，right = mid -1; target >= nums[mid] �? left = mid + 1;刚好和�?�算下边界时条件相反，返�? right�?

**计算上边界代�?**

```java
int upperBound(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            //求mid
            int mid = left + ((right - left) >> 1);
            //移动左指针情�?
            if (target >= nums[mid]) {
                 left = mid + 1;
            //移动右指针情�?
            }else if (target < nums[mid]) {
                right = mid - 1;
            }

        }
        return left;
    }
```

#### **题目完整代码**

```java
class Solution {
    public int[] searchRange (int[] nums, int target) {
         int upper = upperBound(nums,target);
         int low = lowerBound(nums,target);
         //不存在情�?
         if (upper < low) {
             return new int[]{-1,-1};
         }
         return new int[]{low,upper};
    }
    //计算下边�?
    int lowerBound(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            //这里需要注意，计算mid
            int mid = left + ((right - left) >> 1);
            if (target <= nums[mid]) {
                //当目标值小于等于nums[mid]时，继续在左区间检�?，找到�??一�?�?
                right = mid - 1;

            }else if (target > nums[mid]) {
                //�?标值大于nums[mid]时，则在右区间继�?检�?，找到�??一�?等于�?标值的�?
                left = mid + 1;

            }
        }
        return left;
    }
    //计算上边�?
    int upperBound(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + ((right - left) >> 1);
            if (target >= nums[mid]) {
                 left = mid + 1;
            }else if (target < nums[mid]) {
                right = mid - 1;
            }
        }
        return right;
    }
}
```

Go Code:

```go
func searchRange(nums []int, target int) []int {
    upper := upperBound(nums, target)
    lower := lowerBound(nums, target)

    if (upper < lower) {
        return []int{-1, -1}
    }
    return []int{lower, upper}
}

// upperBound 计算上边�?
func upperBound(nums []int, target int) int {
    l, r := 0, len(nums) - 1
    for l <= r {
        m := l + (r - l) / 2
        if target >= nums[m] {
            l = m + 1
        } else if target < nums[m] {
            r = m - 1
        }
    }
    return r
}

// lowerBound 计算下边�?
func lowerBound(nums []int, target int) int {
    l, r := 0, len(nums) - 1
    for l <= r {
        m := l + (r - l) / 2
        if target <= nums[m] {
            r = m - 1
        } else if target > nums[m] {
            l = m + 1
        }
    }
    return l
}
```


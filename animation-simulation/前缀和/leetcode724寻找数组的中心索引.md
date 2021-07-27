> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

### 前缀和�?�解

今天我们来�?�一下刷题时经常用到的前缀和思想，前缀和思想和滑动窗口会经常用在求子数组和子串问题上，当我们遇到此类�?题时，则应�?�需要想到�?�类解�?�方式，该文章深入浅出描述前缀和思想，�?�完这个文章就会有属于自己的解�?��?�架，遇到�?�类�?题时就能够轻松应对�?

下面我们先来了解一下什么是前缀和�?

前缀和其实我�?很早之前就了解过的，我们求数列的和时，Sn = a1+a2+a3+...an; 此时 Sn 就是数列的前 n 项和。例 S5 = a1 + a2 + a3 + a4 + a5; S2 = a1 + a2。所以我�?完全�?以通过 S5-S2 得到 a3+a4+a5 的值，这个过程就和我们做�?�用到的前缀和思想类似。我�?的前缀和数组里保存的就�?�? n 项的和。�?�下�?

![](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/�?信截图_20210113193831.4wk2b9zc8vm0.png)

我们通过前缀和数组保存前 n 位的和，presum[1]保存的就�? nums 数组�?�? 1 位的和，也就�? **presum[1]** = nums[0], **presum[2]** = nums[0] + nums[1] = **presum[1]** + nums[1]. 依�?�类�?，所以我�?通过前缀和数组可以轻松得到每�?区间的和�?

例�?�我�?需要获�? nums[2] �? nums[4] 这个区间的和，我�?则完全根�? presum 数组得到，是不是有点和我�?之前说的字�?�串匹配算法�? BM,KMP �?�? next 数组�? suffix 数组作用类似。那么我�?怎么根据 presum 数组获取 nums[2] �? nums[4] 区间的和�?？�?�下�?

![前缀和](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/前缀�?.77twdj3gpkg0.png)

好啦，我�?已经了解了前缀和的解�?�思想了，我们�?以通过下面这�?�代码得到我�?的前缀和数组，非常简�?

```java
 for (int i = 0; i < nums.length; i++) {
      presum[i+1] = nums[i] + presum[i];
 }
```

好啦，我�?开始实战吧�?

#### [724. 寻找数组的中心下标](https://leetcode-cn.com/problems/find-pivot-index/)

**题目描述**

> 给定一�?整数类型的数�? nums，�?�编写一�?能�?�返回数�? “中心索引�? 的方法�?
>
> 我们�?这样定义数组 �?心索�? 的：数组�?心索引的左侧所有元素相加的和等于右侧所有元素相加的和�?
>
> 如果数组不存在中心索引，那么我们应�?�返�? -1。�?�果数组有�?�个�?心索引，那么我们应�?�返回最靠近左边的那一�?�?

**示例 1�?**

> 输入�?
> nums = [1, 7, 3, 6, 5, 6]
> 输出�?3

解释�?
索引 3 (nums[3] = 6) 的左侧数之和 (1 + 7 + 3 = 11)，与右侧数之�? (5 + 6 = 11) 相等�?
同时, 3 也是�?一�?符合要求的中心索引�?

**示例 2�?**

> 输入�?
> nums = [1, 2, 3]
> 输出�?-1

解释�?
数组�?不存在满足�?�条件的�?心索引�?

理解了我�?前缀和的概念（不知道好像也可以做，这�?题太简单了哈哈）。我�?�?以一下就能把这个题目做出来，先遍历一遍求出数组的和，然后�?二�?�遍历时，直接进行�?�比左半部分和右半部分是否相同，如果相同则返�? true，不同则继续遍历�?

Java Code:

```java
class Solution {
    public int pivotIndex(int[] nums) {
        int presum = 0;
        //数组的和
        for (int x : nums) {
           presum += x;
        }
        int leftsum = 0;
        for (int i = 0; i < nums.length; ++i) {
            //发现相同情况
            if (leftsum == presum - nums[i] - leftsum) {
                return i;
            }
            leftsum += nums[i];
        }
        return -1;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int presum = 0;
        //数组的和
        for (int x : nums) {
           presum += x;
        }
        int leftsum = 0;
        for (int i = 0; i < nums.size(); ++i) {
            //发现相同情况
            if (leftsum == presum - nums[i] - leftsum) {
                return i;
            }
            leftsum += nums[i];
        }
        return -1;
    }
};
```

Go Code:

```go
func pivotIndex(nums []int) int {
    presum := 0
    for _, num := range nums {
        presum += num
    }
    var leftsum int
    for i, num := range nums {
        // 比较左半和右半是否相�?
        if presum - leftsum - num == leftsum {
            return i
        }
        leftsum += num
    }
    return -1
}
```


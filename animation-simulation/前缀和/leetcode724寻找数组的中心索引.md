> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

### 前缀和详解

今天我们来说一下刷题时经常用到的前缀和思想，前缀和思想和滑动窗口会经常用在求子数组和子串问题上，当我们遇到此类问题时，则应该需要想到此类解题方式，该文章深入浅出描述前缀和思想，读完这个文章就会有属于自己的解题框架，遇到此类问题时就能够轻松应对。

下面我们先来了解一下什么是前缀和。

前缀和其实我们很早之前就了解过的，我们求数列的和时，Sn = a1+a2+a3+...an; 此时 Sn 就是数列的前 n 项和。例 S5 = a1 + a2 + a3 + a4 + a5; S2 = a1 + a2。所以我们完全可以通过 S5-S2 得到 a3+a4+a5 的值，这个过程就和我们做题用到的前缀和思想类似。我们的前缀和数组里保存的就是前 n 项的和。见下图

![](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/微信截图_20210113193831.4wk2b9zc8vm0.png)

我们通过前缀和数组保存前 n 位的和，presum[1]保存的就是 nums 数组中前 1 位的和，也就是 **presum[1]** = nums[0], **presum[2]** = nums[0] + nums[1] = **presum[1]** + nums[1]. 依次类推，所以我们通过前缀和数组可以轻松得到每个区间的和。

例如我们需要获取 nums[2] 到 nums[4] 这个区间的和，我们则完全根据 presum 数组得到，是不是有点和我们之前说的字符串匹配算法中 BM,KMP 中的 next 数组和 suffix 数组作用类似。那么我们怎么根据 presum 数组获取 nums[2] 到 nums[4] 区间的和呢？见下图

![前缀和](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/前缀和.77twdj3gpkg0.png)

好啦，我们已经了解了前缀和的解题思想了，我们可以通过下面这段代码得到我们的前缀和数组，非常简单

```java
 for (int i = 0; i < nums.length; i++) {
      presum[i+1] = nums[i] + presum[i];
 }
```

好啦，我们开始实战吧。

#### [724. 寻找数组的中心下标](https://leetcode-cn.com/problems/find-pivot-index/)

**题目描述**

> 给定一个整数类型的数组 nums，请编写一个能够返回数组 “中心索引” 的方法。
>
> 我们是这样定义数组 中心索引 的：数组中心索引的左侧所有元素相加的和等于右侧所有元素相加的和。
>
> 如果数组不存在中心索引，那么我们应该返回 -1。如果数组有多个中心索引，那么我们应该返回最靠近左边的那一个。

**示例 1：**

> 输入：
> nums = [1, 7, 3, 6, 5, 6]
> 输出：3

解释：
索引 3 (nums[3] = 6) 的左侧数之和 (1 + 7 + 3 = 11)，与右侧数之和 (5 + 6 = 11) 相等。
同时, 3 也是第一个符合要求的中心索引。

**示例 2：**

> 输入：
> nums = [1, 2, 3]
> 输出：-1

解释：
数组中不存在满足此条件的中心索引。

理解了我们前缀和的概念（不知道好像也可以做，这个题太简单了哈哈）。我们可以一下就能把这个题目做出来，先遍历一遍求出数组的和，然后第二次遍历时，直接进行对比左半部分和右半部分是否相同，如果相同则返回 true，不同则继续遍历。

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
        // 比较左半和右半是否相同
        if presum - leftsum - num == leftsum {
            return i
        }
        leftsum += num
    }
    return -1
}
```

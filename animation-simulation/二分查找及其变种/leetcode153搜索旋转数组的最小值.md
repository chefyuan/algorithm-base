> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

## **寻找最小�?**

这�?�情况也很�?�易处理，和咱们�? leetcode33 搜索旋转排序数组，�?�目类似，只不过一�?需要搜索目标元素，一�?搜索最小值，我们搜索�?标元素很容易处理，但�?我们搜索最小值应该怎么整呢？�?�下�?

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210321134701939.png)

我们需要在一�?旋转数组�?，查找其�?的最小值，如果我们数组�?完全有序的很容易，我�?�?需要返回�??一�?元素即可，但�?此时我们�?旋转过的数组�?

我们需要考虑以下情况

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021032113472644.png)

我们见上图，我们需要考虑的情况是

- 数组完全有序 nums[left] < nums[right]，�?�时返回 nums[left] 即可

- left �? mid 在一�?都在前半部分，单调递�?�区间内，所以需要移�? left，继�?查找，left = mid + 1�?

- left 在前半部分，mid 在后半部分，则最小值必�? left �? mid 之间（�?�下图）。则需要移�? right ，right = mid，我�?见上图，如果我们 right = mid - 1，则会漏掉我�?的最小值，因为此时 mid 指向的可能就�?我们的最小值。所以应该是 right = mid �?

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210321134748668.png)

#### [153. 寻找旋转排序数组�?的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

#### **题目描述**

假�?�按照升序排序的数组在�?�先�?知的某个点上进�?�了旋转。例如，数组 [0,1,2,4,5,6,7] �?能变�? [4,5,6,7,0,1,2] �?

请找出其�?最小的元素�?

示例 1�?

> 输入：nums = [3,4,5,1,2]输出�?1

示例 2�?

> 输入：nums = [4,5,6,7,0,1,2] 输出�?0

示例 3�?

> 输入：nums = [1] 输出:1

#### **题目解析**

我们在上面的描述�?已经和大家分析过几�?�情况，下面我们一起来看一下，[5,6,7,0,1,2,3]的执行过程，相信通过这个例子，大家就能把这个题目整透了�?

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210321134814233.png)

**题目代码**

Java Code:

```java
class Solution {
    public int findMin(int[] nums) {

        int left = 0;
        int right = nums.length - 1;

        while (left < right) {

            if (nums[left] < nums[right]) {
                return nums[left];
            }
            int mid = left + ((right - left) >> 1);
            if (nums[left] > nums[mid]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return nums[left];

    }
}
```

C++ Code:

```cpp
class Solution {
public:
    int findMin(vector <int> & nums) {
        int left = 0;
        int right = nums.size() - 1;
        while (left < right) {
            if (nums[left] < nums[right]) {
                return nums[left];
            }
            int mid = left + ((right - left) >> 1);
            if (nums[left] > nums[mid]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return nums[left];
    }
};
```

Go Code:

```go
func findMin(nums []int) int {
    l, r := 0, len(nums) - 1
    for l < r {
        if nums[l] < nums[r] {
            return nums[l]
        }
        m := l + (r - l) / 2
        if nums[l] > nums[m] {
            r = m
        } else {
            l = m + 1
        }
    }
    return nums[l]
}
```


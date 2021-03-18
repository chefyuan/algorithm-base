## **寻找最小值**

这种情况也很容易处理，和咱们的leetcode33搜索旋转排序数组，题目类似，只不过一个需要搜索目标元素，一个搜索最小值，我们搜索目标元素很容易处理，但是我们搜索最小值应该怎么整呢？见下图

![640 (3)](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/640 (3).6ck28790c280.png)

我们需要在一个旋转数组中，查找其中的最小值，如果我们数组是完全有序的很容易，我们只需要返回第一个元素即可，但是此时我们是旋转过的数组。

我们需要考虑以下情况

![640 (4)](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/640 (4).2iwrg2xci9a0.png)

我们见上图，我们需要考虑的情况是

- 数组完全有序 nums[left] < nums[right]，此时返回 nums[left] 即可

- left 和 mid 在一个都在前半部分，单调递增区间内，所以需要移动 left，继续查找，left = mid + 1；

- left 在前半部分，mid在后半部分，则最小值必在 left 和 mid 之间（见下图）。则需要移动right ，right = mid，我们见上图，如果我们 right = mid - 1，则会漏掉我们的最小值，因为此时 mid 指向的可能就是我们的最小值。所以应该是 right = mid 。

  

![640 (5)](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/640 (5).78yd8y1g14w0.png)



### **leetcode 153 寻找旋转数组中的最小值**

#### **题目描述**

假设按照升序排序的数组在预先未知的某个点上进行了旋转。例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] 。



请找出其中最小的元素。

示例 1：

> 输入：nums = [3,4,5,1,2]输出：1

示例 2：

> 输入：nums = [4,5,6,7,0,1,2] 输出：0

示例 3：

> 输入：nums = [1] 输出:1

#### **题目解析**

我们在上面的描述中已经和大家分析过几种情况，下面我们一起来看一下，[5,6,7,0,1,2,3]的执行过程，相信通过这个例子，大家就能把这个题目整透了。

![640 (6)](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/640 (6).1f8qlopg764g.png)

**题目代码**

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


## **查找目标元素（含重复元素）**

我们通过刚才的例子了解了，如果在不完全有序的数组中查找目标元素，但是我们的不完全有序数组中是不包含重复元素的，那如果我们的数组中包含重复元素我们应该怎么做呢？见下图

![640](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/640.667bvokp3980.png)

如上图，如果我们继续使用刚才的代码，则会报错这是为什么呢?我们来分析一下。

![640 (1)](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/640 (1).ue8v83e5fkg.png)

所以我们需要对其进行改进，我们只需将重复元素去掉即可，当我们的 nums[left] == nums[mid] 时，让 left ++ 即可，比如 1，3，1，1，1此时 nums[mid] == nums[left] 则 left ++,那我们此时会不会错过目标值呢？其实并不会，只是去掉了某些重复元素，如果此时我们的目标元素是3，则我们left++，之后情况就变为了上题中的情况。

### leetcode81. 搜索旋转排序数组 II

#### **题目描述**



假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,0,1,2,2,5,6] 可能变为 [2,5,6,0,0,1,2] )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 true，否则返回 false。

示例 1：

> 输入：nums = [2,5,6,0,0,1,2], target = 0 输出：true

示例 2：

> 输入：nums = [2,5,6,0,0,1,2], target = 3 输出：false

#### **题目解析**

这个题目就比刚才的不含重复元素的题目多了一个去除某些重复元素的情况，当 nums[mid] == nums[left] 时，让 left++，并退出本次循环，其余部分完全相同，大家可以结合代码和图片进行理解。

#### **题目代码**

```java
class Solution {
    public boolean search(int[] nums, int target) {
     int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            int mid = left+((right-left)>>1);
            if (nums[mid] == target) {
                return true;
            }
            if (nums[mid] == nums[left]) {
                left++;
                continue;
            }
            if (nums[mid] > nums[left]) {
                if (nums[mid] > target && target >= nums[left]) {
                       right = mid - 1;
                } else if (target > nums[mid] || target < nums[left]) {
                       left = mid + 1;
                } 

            }else if (nums[mid] < nums[left]) {
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else if (target < nums[mid] || target > nums[right]) {
                    right = mid - 1;
                }
            } 
        }
        return false;
    }    
}
```



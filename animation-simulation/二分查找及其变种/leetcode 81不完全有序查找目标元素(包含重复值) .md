> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

## **查找目标元素（含重复元素）**

我们通过刚才的例子了解了，如果在不完全有序的数组中查找目标元素，但是我们的不完全有序数组中是不包含重复元素的，那如果我们的数组中包含重复元素我们应该怎么做呢？见下图

![640](https://img-blog.csdnimg.cn/img_convert/9f77a33a7ff5b3fd8bbb98d77cb8a499.png)

如上图，如果我们继续使用刚才的代码，则会报错这是为什么呢?我们来分析一下。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210321134336356.png)

所以我们需要对其进行改进，我们只需将重复元素去掉即可，当我们的 nums[left] == nums[mid] 时，让 left ++ 即可，比如 1，3，1，1，1 此时 nums[mid] == nums[left] 则 left ++,那我们此时会不会错过目标值呢？其实并不会，只是去掉了某些重复元素，如果此时我们的目标元素是 3，则我们 left++，之后情况就变为了上题中的情况。

#### [81. 搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

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

Java Code:

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

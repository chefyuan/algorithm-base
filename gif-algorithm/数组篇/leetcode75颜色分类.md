### leetcode 75 颜色分类

**题目描述**

> 给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。
>
> 此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

**示例 1：**

> 输入：nums = [2,0,2,1,1,0]
> 输出：[0,0,1,1,2,2]

**示例 2：**

> 输入：nums = [2,0,1]
> 输出：[0,1,2]

示例 3：

> 输入：nums = [0]
> 输出：[0]

示例 4：

> 输入：nums = [1]
> 输出：[1]

**两次遍历**

**解析：**

通过两次遍历，第一遍遍历首先将 0 归位，第二遍遍历将 1 归位，自然 2 也就被归位了，这个方法很容易理解我们直接看代码吧。

**题目代码**

```java
class Solution {
    public void sortColors(int[] nums) {
        int pro = 0;
        //将0归位
        for (int i = 0; i < nums.length; ++i) {
            if (nums[i] == 0) {
                swap(nums,i,pro);
                pro++;
            }        
        }
        //将1归位
        for (int j = pro; j < nums.length; ++j) {
            if(nums[j] == 1) {
                swap(nums,j,pro);
                pro++;
            }
        }
    }
    public void swap(int[] nums,int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

  **一次遍历**

**解析**

两次遍历实现是十分容易的，也很容易实现，那么我们可不可以一次遍历就将其归位呢？其实这里也利用了我们双指针的思想，我们首先定义两个指针，一个位于数组头部，一个位于数组尾部，当我们遇到 0 时则给我们头部指针交换，遇到 2 时，则给尾部指针交换。不过里面有两个细节我们需要注意。

1.遍历数组时，指针的上界，不能是 i < nums.length;应是 i <= right;

2.需要注意交换后，当前指针指向的仍不为1。

干看上面两种注意事项，可能不是特别容易理解，我们来看我们的视频解析，就可以搞懂这两个情况啦。

**动图解析**

![leetcode75颜色分类](https://cdn.jsdelivr.net/gh/tan45du/test1@master/20210122/leetcode75颜色分类.5w4sa458rr40.gif)

**题目代码**

```java
class Solution {
    public void sortColors(int[] nums) {
        int len = nums.length;
        int left = 0;
        int right = len-1;
        //注意看 for 循环的结束条件
        for (int i = 0; i <= right; ++i) {
            if (nums[i] == 0) {
                swap(nums,i,left);
                left++;
            }
            if (nums[i] == 2) {
                swap(nums,i,right);
                right--;
                // 发现此时不为1，则指针不移动，继续交换
                if (nums[i] != 1) {
                    i--;
                }
            }
        }
    }
    public void swap (int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```


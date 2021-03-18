**leetcode 75 颜色分类**

题目描述：

给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

示例 1：

> 输入：nums = [2,0,2,1,1,0]
> 输出：[0,0,1,1,2,2]

示例 2：

> 输入：nums = [2,0,1]
> 输出：[0,1,2]

示例 3：

> 输入：nums = [0]
> 输出：[0]

示例 4：

> 输入：nums = [1]
> 输出：[1]

**做题思路**

这个题目我们使用 Arrays.sort() 解决，哈哈，但是那样太无聊啦，题目含义就是让我们将所有的 0 放在前面，2放在后面，1 放在中间，是不是和我们上面说的荷兰国旗问题一样。我们仅仅将 1 做为 pivot 值。

下面我们直接看代码吧，和三向切分基本一致。

```java
class Solution {
    public void sortColors(int[] nums) {
        int len = nums.length;
        int left = 0;
        //这里和三向切分不完全一致
        int i = left;
        int right = len-1;
        
        while (i <= right) {
             if (nums[i] == 2) {
                 swap(nums,i,right--);
             } else if (nums[i] == 0) {
                 swap(nums,i++,left++);
             } else {
                 i++;
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

另外我们看这段代码，有什么问题呢？那就是我们即使完全符合时，仍会交换元素，这样会大大降低我们的效率。

例如：[0,0,0,1,1,1,2,2,2]

此时我们完全符合情况，不需要交换元素，但是按照我们上面的代码，0,2 的每个元素会和自己进行交换，所以这里我们可以根据  i  和 left 的值是否相等来决定是否需要交换，大家可以自己写一下。

下面我们看一下另外一种写法

这个题目的关键点就是，当我们 nums[i] 和 nums[right] 交换后，我们的 nums[right] 此时指向的元素是符合要求的，但是我们 nums[i] 指向的元素不一定符合要求，所以我们需要继续判断。

![细节地方](https://cdn.jsdelivr.net/gh/tan45du/test@master/photo/微信截图_20210305153911.28capmzljy80.png)

我们 2 和 0 交换后，此时 i 指向 0 ，0 应放在头部，所以不符合情况，所以 0 和 1 仍需要交换。下面我们来看一下动画来加深理解吧。

![leetcode75颜色分类](https://cdn.jsdelivr.net/gh/tan45du/test1@master/20210122/leetcode75颜色分类.5w4sa458rr40.gif)

另一种代码表示

```java
class Solution {
    public void sortColors(int[] nums) {

        int left = 0;
        int len = nums.length;
        int right = len - 1;
        for (int i = 0; i <= right; ++i) {
            if (nums[i] == 0) {             
                swap(nums,i,left);
                left++;
            }
            if (nums[i] == 2) {
                swap(nums,i,right);
                right--;
                //如果不等于 1 则需要继续判断，所以不移动 i 指针，i--
                if (nums[i] != 1) {
                    i--;
                }
            }
        }
        
    }
    public void swap (int[] nums,int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

好啦，这个问题到这就结束啦，是不是很简单啊，我们明天见！


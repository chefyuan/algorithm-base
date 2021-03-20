## **leetcode 485 最大连续 1 的个数**

给定一个二进制数组， 计算其中最大连续1的个数。

示例 1:

> 输入: [1,1,0,1,1,1]
> 输出: 3
> 解释: 开头的两位和最后的三位都是连续1，所以最大连续1的个数是 3.

我的这个方法比较奇怪，但是效率还可以，战胜了 100% , 尽量减少了 Math.max()的使用，我们来看一下具体思路，利用 right 指针进行探路，如果遇到 1 则继续走，遇到零时则停下，求当前 1 的个数。

这时我们可以通过 right - left 得到 1 的 个数，因为此时我们的 right 指针指在 0 处，所以不需要和之前一样通过 right - left + 1 获得窗口长度。 

然后我们再使用 while 循环，遍历完为 0 的情况，跳到下一段为 1 的情况，然后移动 left 指针。 left = right，站在同一起点，继续执行上诉过程。

下面我们通过一个视频模拟代码执行步骤大家一下就能搞懂了。

 ![leetcode485最长连续1的个数](https://cdn.jsdelivr.net/gh/tan45du/test1@master/20210122/leetcode485最长连续1的个数.7avzcthkit80.gif)





下面我们直接看代码吧

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {

        int len = nums.length;
        int left = 0, right = 0;
        int maxcount = 0;

        while (right < len) {
            if (nums[right] == 1) {
                right++;
                continue;
            }
            //保存最大值
            maxcount = Math.max(maxcount, right - left);
            //跳过 0 的情况
            while (right < len && nums[right] == 0) {
                right++;
            }
            //同一起点继续遍历
            left = right;
        }
        return Math.max(maxcount, right-left);

    }
}
```



刚才的效率虽然相对高一些，但是代码不够优美，欢迎各位改进，下面我们说一下另外一种情况，一个特别容易理解的方法。

我们通过计数器计数 连续 1 的个数，当 nums[i] == 1 时，count++，nums[i] 为 0 时，则先保存最大 count，再将 count 清零，因为我们需要的是连续的 1 的个数，所以需要清零。

好啦，下面我们直接看代码吧。

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {

        int count = 0;
        int maxcount = 0;
        
        for (int i = 0; i < nums.length; ++i) {
            if (nums[i] == 1) {
                count++;
            //这里可以改成 while
            } else {
                 maxcount = Math.max(maxcount,count);
                 count = 0;
            }
        }
        return Math.max(count,maxcount);

    }
}
```


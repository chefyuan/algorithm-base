> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [485. 最大连�? 1 的个数](https://leetcode-cn.com/problems/max-consecutive-ones/)

给定一�?二进制数组， 计算其中最大连�? 1 的个数�?

示例 1:

> 输入: [1,1,0,1,1,1]
> 输出: 3
> 解释: 开头的两位和最后的三位都是连续 1，所以最大连�? 1 的个数是 3.

我的这个方法比较奇�?，但�?效率还可以，战胜�? 100% , 尽量减少�? Math.max()的使�?，我�?来看一下具体思路，利�? right 指针进�?�探�?，�?�果遇到 1 则继�?走，遇到零时则停下，求当�? 1 的个数�?

这时我们�?以通过 right - left 得到 1 �? �?数，因为此时我们�? right 指针指在 0 处，所以不需要和之前一样通过 right - left + 1 获得窗口长度�?

然后我们再使�? while �?�?，遍历完�? 0 的情况，跳到下一段为 1 的情况，然后移动 left 指针�? left = right，站在同一起点，继�?执�?�上诉过程�?

下面我们通过一�?视�?�模拟代码执行�?��?�大家一下就能搞懂了�?

![leetcode485最长连�?1的个数](https://cdn.jsdelivr.net/gh/tan45du/test1@master/20210122/leetcode485最长连�?1的个�?.7avzcthkit80.gif)

下面我们直接看代码吧

Java Code:

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
            //保存最大�?
            maxcount = Math.max(maxcount, right - left);
            //跳过 0 的情�?
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

Python3 Code:

```python
from typing import List
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int])->int:
        leng = len(nums)
        left = 0
        right = 0
        maxcount = 0
        while right < leng:
            if nums[right] == 1:
                right += 1
                continue
            # 保存最大�?
            maxcount = max(maxcount, right - left)
            # 跳过 0 的情�?
            while right < leng and nums[right] == 0:
                right += 1
            # 同一起点继续遍历
            left = right
        return max(maxcount, right - left)
```

Swift Code

```swift
class Solution {
    func findMaxConsecutiveOnes(_ nums: [Int]) -> Int {

        var left = 0, right = 0, res = 0
        let len = nums.count
        while right < len {
            if nums[right] == 1 {
                right += 1
                continue
            }
            // 保存最大�?
            res = max(res, right - left)
            // 跳过 0 的情�?
            while right < len && nums[right] == 0 {
                right += 1
            }
            // 同一起点继续遍历
            left = right
        }
        return max(res, right - left)
    }
}
```

刚才的效率虽然相对高一些，但是代码不�?�优美，欢迎各位改进，下面我�?说一下另外一种情况，一�?特别容易理解的方法�?

我们通过计数器�?�数 连续 1 的个数，�? nums[i] == 1 时，count++，nums[i] �? 0 时，则先保存最�? count，再�? count 清零，因为我�?需要的�?连续�? 1 的个数，所以需要清零�?

好啦，下面我�?直接看代码吧�?

Java Code:

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {

        int count = 0;
        int maxcount = 0;

        for (int i = 0; i < nums.length; ++i) {
            if (nums[i] == 1) {
                count++;
            //这里�?以改�? while
            } else {
                 maxcount = Math.max(maxcount,count);
                 count = 0;
            }
        }
        return Math.max(count,maxcount);

    }
}
```

Python3 Code:

```py
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        ans = i = t = 0
        for j in range(len(nums)):
            if nums[j] == 1:
                t += 1
                ans = max(ans, t)
            else:
                i = j + 1
                t = 0
        return ans
```

Swift Code

```swift
class Solution {
    func findMaxConsecutiveOnes(_ nums: [Int]) -> Int {
        let len = nums.count
        var maxCount = 0, count = 0
        for i in 0..<len {
            if nums[i] == 1 {
                count += 1
            } else { // 这里�?以改�? while
                maxCount = max(maxCount, count)
                count = 0
            }
        }
        return max(maxCount, count)
    }
}
```

C++ Code

```C++
class Solution
{
public:
    int findMaxConsecutiveOnes(vector<int> &nums)
    {
        int s = 0;
        int e = 0;
        int result = 0;
        int size = nums.size();

        while (s < size && e < size)
        {
            while (s < size && nums[s++] == 1)
            {
                e = s;
                while (e < size && nums[e] == 1)
                {
                    e++;
                };
                //注意需要加1, �?以使用极限条件测�?
                int r = e - s + 1;
                if (r > result)
                    result = r;
                s = e;
            }
        }

        return result;
    }
};
```

Go Code:

```go
func findMaxConsecutiveOnes(nums []int) int {
    cnt, maxCnt := 0, 0
    for i := 0; i < len(nums); i++ {
        if nums[i] == 1 {
            cnt++
        } else {
            maxCnt = max(maxCnt, cnt)
            cnt = 0
        }
    }
    return max(maxCnt, cnt)
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```


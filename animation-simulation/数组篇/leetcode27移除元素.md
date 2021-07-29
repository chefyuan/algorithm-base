> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [27. 移除元素](https://leetcode-cn.com/problems/remove-element/)

**题目描述**

> 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。
>
> 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。
>
> 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

**示例 1:**

> 给定 nums = [3,2,2,3], val = 3,
>
> 函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。
>
> 你不需要考虑数组中超出新长度后面的元素。

**示例 2:**

> 给定 nums = [0,1,2,2,3,0,4,2], val = 2,
>
> 函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。
>
> 注意这五个元素可为任意顺序。
>
> 你不需要考虑数组中超出新长度后面的元素。

**暴力法**

**解析**

该题目也算是简单题目，适合新手来做，然后大家也不要看不起暴力解法，我们可以先写出暴力解法，然后再思考其他方法，这对于我们的编码能力有很大的帮助。我们来解析一下这个题目的做题思路，他的含义就是让我们删除掉数组中的元素，然后将数组后面的元素跟上来。最后返回删除掉元素的数组长度即可。比如数组长度为 10，里面有 2 个目标值，我们最后返回的长度为 8，但是返回的 8 个元素，需要排在数组的最前面。那么暴力解法的话则就需要两个 for 循环，一个用来找到删除，另一个用来更新数组。

![移除数组元素暴力法](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/移除数组元素.lhuefelqd5o.png)

总体思路就是这样的，后面的会不断往前覆盖。暴力解法也是不超时的，实现也不算太简单主要需要注意两个地方。

（1）需要先定义变量 len 获取数组长度，因为后面我们的返回的数组长度是改变的，所以不可以用 nums.length 作为上界

（2）我们每找到一个需要删除的值的时候，需要 i--，防止出现多个需要删除的值在一起的情况，然后漏删。

**题目代码**

Java Code:

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        //获取数组长度
        int len = nums.length;
        if (len == 0) {
            return 0;
        }
        int i = 0;
        for (i = 0; i < len; ++i) {
            //发现符合条件的情况
            if (nums[i] == val) {
                //前移一位
                for (int j = i; j < len-1; ++j) {
                    nums[j] = nums[j+1];
                }
                i--;
                len--;
            }
        }
        return i;
    }
}
```

Python3 Code:

```python
from typing import List
class Solution:
    def removeElement(self, nums: List[int], val: int)->int:
        # 获取数组长度
        leng = len(nums)
        if 0 == leng:
            return 0
        i = 0
        while i < leng:
            # 发现符合条件的情况
            if nums[i] == val:
                # 前移一位
                for j in range(i, leng - 1):
                    nums[j] = nums[j + 1]
                i -= 1
                leng -= 1
            i += 1
        return i
```

**双指针**

快慢指针的做法比较有趣，只需要一个 for 循环即可解决，时间复杂度为 O(n) ,总体思路就是有两个指针，前面一个后面一个，前面的用于搜索需要删除的值，当遇到需要删除的值时，前指针直接跳过，后面的指针不动，当遇到正常值时，两个指针都进行移动，并修改慢指针的值。最后只需输出慢指针的索引即可。

**动图解析:**

![](https://img-blog.csdnimg.cn/20210317194638700.gif#pic_center)

**题目代码：**

Java Code:

```java
class Solution {
    public int removeElement(int[] nums, int val) {
          int len = nums.length;
          if (len == 0) {
              return 0;
          }
          int i = 0;
          for (int j = 0; j < len; ++j) {
                //如果等于目标值，则删除
                if (nums[j] == val) {
                    continue;
                }
                // 不等于目标值时，则赋值给nums[i],i++
                nums[i++] = nums[j];
          }
          return i;
    }
}
```

Python3 Code:

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i = 0
        for j in range(len(nums)):
            if nums[j] != val:
                nums[i] = nums[j]
                i += 1
        return i
```

C++ Code:

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int n = nums.size();
      	if(!n) return 0;
      	int i = 0;
      	for(int j = 0; j < n; ++j){
          if(nums[j] == val) continue;
          nums[i++] = nums[j];
        }
      	return i;
    }
};
```

Swift Code

```swift
class Solution {
    func removeElement(_ nums: inout [Int], _ val: Int) -> Int {
        if nums.count == 0 {
            return 0
        }
        var i = 0
        for j in 0..<nums.count {
            if nums[j] != val {
                nums[i] = nums[j]
                i += 1
            }

        }
        return i
    }
}
```

Go Code:

```go
func removeElement(nums []int, val int) int {
    length := len(nums)
    if length == 0 {
        return 0
    }
    i := 0
    for j := 0; j < length; j++ {
        if nums[j] == val {
            continue
        }
        nums[i] = nums[j]
        i++
    }
    return i
}
```

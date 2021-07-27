> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [27. 移除元素](https://leetcode-cn.com/problems/remove-element/)

**题目描述**

> 给你一�?数组 nums 和一�?�? val，你需�? 原地 移除所有数值等�? val 的元素，并返回移除后数组的新长度�?
>
> 不�?�使用�?��?�的数组空间，你必须仅使�? O(1) 额�?�空间并 原地 �?改输入数组�?
>
> 元素的顺序可以改变。你不需要考虑数组�?超出新长度后面的元素�?

**示例 1:**

> 给定 nums = [3,2,2,3], val = 3,
>
> 函数应�?�返回新的长�? 2, 并且 nums �?的前两个元素均为 2�?
>
> 你不需要考虑数组�?超出新长度后面的元素�?

**示例 2:**

> 给定 nums = [0,1,2,2,3,0,4,2], val = 2,
>
> 函数应�?�返回新的长�? 5, 并且 nums �?的前五个元素�? 0, 1, 3, 0, 4�?
>
> 注意这五�?元素�?为任意顺序�?
>
> 你不需要考虑数组�?超出新长度后面的元素�?

**暴力�?**

**解析**

该�?�目也算�?简单�?�目，适合新手来做，然后大家也不�?�看不起暴力解法，我�?�?以先写出暴力解法，然后再思考其他方法，这�?�于我们的编码能力有很大的帮助。我�?来解析一下这�?题目的做题思路，他的含义就�?让我�?删除掉数组中的元素，然后将数组后面的元素跟上来。最后返回删除掉元素的数组长度即�?。比如数组长度为 10，里面有 2 �?�?标值，我们最后返回的长度�? 8，但�?返回�? 8 �?元素，需要排在数组的最前面。那么暴力解法的话则就需要两�? for �?�?，一�?用来找到删除，另一�?用来更新数组�?

![移除数组元素暴力法](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/移除数组元素.lhuefelqd5o.png)

总体思路就是这样的，后面的会不断往前�?�盖。暴力解法也�?不超时的，实现也不算�?简单主要需要注意两�?地方�?

�?1）需要先定义变量 len 获取数组长度，因为后面我�?的返回的数组长度�?改变的，所以不�?以用 nums.length 作为上界

�?2）我�?每找到一�?需要删除的值的时候，需�? i--，防止出现�?�个需要删除的值在一起的情况，然后漏删�?

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
            //发现符合条件的情�?
            if (nums[i] == val) {
                //前移一�?
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
            # 发现符合条件的情�?
            if nums[i] == val:
                # 前移一�?
                for j in range(i, leng - 1):
                    nums[j] = nums[j + 1]
                i -= 1
                leng -= 1
            i += 1
        return i
```

**双指�?**

�?慢指针的做法比较有趣，只需要一�? for �?�?即可解决，时间�?�杂度为 O(n) ,总体思路就是有两�?指针，前�?一�?后面一�?，前面的用于搜索需要删除的值，当遇到需要删除的值时，前指针直接跳过，后面的指针不动，当遇到正常值时，两�?指针都进行移�?，并�?改慢指针的值。最后只需输出慢指针的索引即可�?

**动图解析:**

![](https://img-blog.csdnimg.cn/20210317194638700.gif#pic_center)

**题目代码�?**

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
                //如果等于�?标值，则删�?
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


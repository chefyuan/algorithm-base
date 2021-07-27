> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [剑指 Offer 03. 数组�?重�?�的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

**题目描述**

找出数组�?重�?�的数字�?

在一�?长度�? n 的数�? nums 里的所有数字都�? 0 �? n-1 的范围内。数组中某些数字�?重�?�的，但不知道有几个数字重�?�了，也不知道每�?数字重�?�了几�?�。�?�找出数组中任意一�?重�?�的数字�?

示例 1�?

输入�?
[2, 3, 1, 0, 2, 5, 3]
输出�?2 �? 3

#### **HashSet**

**解析**

这�?��?�目或�?�一下就让人想到 HashSet，�?�目描述很清楚就�?让我�?找到数组�?重�?�的元素，那我们�?一下想到的就是 HashSet，我�?遍历数组，�?�果发现 set �?有�?�元素则返回，不�?有则存入哈希�?，�?�目代码也很简�?

**题目代码**

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        // HashSet
        HashSet<Integer> set = new HashSet<Integer>();
        for (int x : nums) {
            //发现某元素存�?，返�?
            if (set.contains(x)) {
                return x;
            }
            //存入哈希�?
            set.add(x);
        }
        return -1;
    }
}
```

Python Code:

```python
from typing import List
class Solution:
    def findRepeatNumber(self, nums: List[int])->int:
        s = set()
        for x in nums:
            # 如果发现某元素存�?，则返回
            if x in s:
                return x
            # 存入集合
            s.add(x)
        return -1
```

Swift Code:

```swift
class Solution {
    func findRepeatNumber(_ nums: [Int]) -> Int {
        var set: Set<Int> = []
        for n in nums {
            if set.contains(n) { // 如果发现某元素存�?，则返回
                return n
            }
            set.insert(n) // 存入集合
        }

        return -1
    }
}
```

#### **原地�?�?**

**解析**

这一种方法也�?我们经常用到的，主�?�用于重复出现的数，缺失的数等�?�目�?，下面我�?看一下这�?原地�?换法，原地置换的大体思路就是将我�?**指针对应**的元素放到属于他的位�?（索引�?�应的地方）。我�?�?以这样理解，每个人都有自己的位置，我�?需要和�?人调换回到属于自己的位置，调�?之后，�?�果发现我们的位�?上有人了，则返回。大致意思了解了，下面看代码的执行过程。通过视�?�一下就�?以搞懂啦�?

![剑指offer3数组�?重�?�的数](https://cdn.jsdelivr.net/gh/tan45du/test1@master/20210122/剑指offer3数组�?重�?�的�?.2p6cd5os0em0.gif)

**题目代码**

Java Code:

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        if (nums.length == 0) {
            return -1;
        }
        for (int i = 0; i < nums.length; ++i) {
            while (nums[i] != i) {
                //发现重�?�元�?
                if (nums[i] == nums[nums[i]]) {
                    return nums[i];
                }
                //�?�?，将指针下的元素换到属于他的索引�?
                int temp = nums[i];
                nums[i] = nums[temp];
                nums[temp] = temp;
            }
        }
        return -1;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
	if(nums.empty()) return 0;
      	int n = nums.size();
      	for(int i = 0; i < n; ++i){
          while(nums[i] != i){
            if(nums[i] == nums[nums[i]]) return nums[i];
            swap(nums[i], nums[nums[i]]);
          }
        }
      return -1;
    }
};
```

Python3 Code:

```python
from typing import List
class Solution:
    def findRepeatNumber(self, nums: List[int])->int:
        if len(nums) == 0:
            return -1
        for i in range(0, len(nums)):
            while nums[i] != i:
                # 发现重�?�元�?
                if nums[i] == nums[nums[i]]:
                    return nums[i]
                # �?�?，将指针下的元素换到属于它的索引�?
                temp = nums[i]
                nums[i] = nums[temp]
                nums[temp] = temp
        return -1
```

Swift Code:

```swift
class Solution {
    func findRepeatNumber(_ nums: [Int]) -> Int {
        if nums.isEmpty {
            return -1
        }
        var nums = nums;
        for i in 0..<nums.count {
            while nums[i] != i {
                if nums[i] == nums[nums[i]] {
                    return nums[i]
                }
                nums.swapAt(i, nums[i])
            }
        }

        return -1
    }
}
```

Go Code:

```go
func findRepeatNumber(nums []int) int {
    l := len(nums)
    if l == 0 {
        return -1
    }
    for i := 0; i < l; i++ {
        // 将nums[i]换到i的位�?�?
        for nums[i] != i {
            if nums[i] == nums[nums[i]] {
                return nums[i]
            }
            nums[i], nums[nums[i]] = nums[nums[i]], nums[i]
        }
    }
    return -1
}
```


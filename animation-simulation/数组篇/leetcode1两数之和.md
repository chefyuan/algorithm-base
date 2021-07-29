> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

**题目描述：**

> 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

**示例:**

> 给定 nums = [2, 7, 11, 15], target = 9
>
> 因为 nums[0] + nums[1] = 2 + 7 = 9
> 所以返回 [0, 1]

题目很容易理解，即让查看数组中有没有两个数的和为目标数，如果有的话则返回两数下标，我们为大家提供两种解法双指针（暴力）法，和哈希表法

**双指针（暴力）法**

**解析**

双指针（L,R）法的思路很简单，L 指针用来指向第一个值，R 指针用来从第 L 指针的后面查找数组中是否含有和 L 指针指向值和为目标值的数。见下图

![图示](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/微信图片_20210104150003.3unncifeoe80.jpg)

例：绿指针指向的值为 3，蓝指针需要在绿指针的后面遍历查找是否含有 target - 3 = 2 的元素，若含有返回即可。

**题目代码**

Java Code:

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        if(nums.length < 2){
            return new int[0];
        }
        int[] rearr = new int[2];
        //查询元素
        for(int i = 0; i < nums.length; i++){
            for(int j = i+1; j < nums.length; j++ ){
                //发现符合条件情况
                if(nums[i] + nums[j] ==target){
                    rearr[0] = i;
                    rearr[1] = j;
                }
            }
        }
        return rearr;
    }
}
```

Python3 Code:

```python
from typing import List
class Solution:
    def twoSum(nums: List[int], target: int)->List[int]:
        if len(nums) < 2:
            return [0]
        rearr = [0] * 2
        # 查询元素
        for i in range(0, len(nums)):
            for j in range(i + 1, len(nums)):
                # 发现符合条件情况
                if nums[i] + nums[j] == target:
                    rearr[0] = i
                    rearr[1] = j
        return rearr
```

Swift Code:

```swift
class Solution {
    func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        let count = nums.count
        if count < 2 {
            return [0]
        }

        var rearr: [Int] = []
        // 查询元素
        for i in 0..<count {
            for j in i+1..<count {
                // 发现符合条件情况
                if nums[i] + nums[j] == target {
                    rearr.append(i)
                    rearr.append(j)
                }
            }
        }
        return rearr
    }
}
```

**哈希表**

**解析**

哈希表的做法很容易理解，我们只需通过一次循环即可，假如我们的 target 值为 9，当前指针指向的值为 2 ，我们只需从哈希表中查找是否含有 7，因为 9 - 2 =7 。如果含有 7 我们直接返回即可，如果不含有则将当前的 2 存入哈希表中，指针移动，指向下一元素。注： key 为元素值，value 为元素索引。

**动图解析：**

![两数之和](https://cdn.jsdelivr.net/gh/tan45du/tan45du.github.io.photo@master/photo/两数之和.7228lcxkqpw0.gif)

是不是很容易理解，下面我们来看一下题目代码。

**题目代码：**

Java Code:

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();
        for(int i = 0; i < nums.length; i++){
            //如果存在则返回
            if(map.containsKey(target-nums[i])){
                return new int[]{map.get(target-nums[i]),i};
            }
            //不存在则存入
            map.put(nums[i],i);

        }
        return new int[0];

    }
}
```

C++ Code:

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> m;
        for (int i = 0; i < nums.size(); ++i) {
            int t = target - nums[i];
            if (m.count(t)) return { m[t], i };
            m[nums[i]] = i;
        }
        return {};
    }
};
```

JS Code:

```js
const twoSum = function (nums, target) {
  const map = new Map();
  for (let i = 0; i < nums.length; i++) {
    const diff = target - nums[i];
    if (map.has(diff)) {
      return [map.get(diff), i];
    }
    map.set(nums[i], i);
  }
};
```

Python3 Code:

```python
from typing import List
class Solution:
    def twoSum(self, nums: List[int], target: int)->List[int]:
        m = {}
        for i in range(0, len(nums)):
            # 如果存在则返回
            if (target - nums[i]) in m.keys():
                return [m[target - nums[i]], i]
            # 不存在则存入
            m[nums[i]] = i
        return [0]
```

Swift Code:

```swift
class Solution {
    func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        var m:[Int:Int] = [:]
        for i in 0..<nums.count {
            let n = nums[i]
            if let k = m[target - n] { // 如果存在则返回
                return [k, i]
            }
            m[n] = i // 不存在则存入
        }
        return [0]
    }
}
```

Go Code:

```go
func twoSum(nums []int, target int) []int {
    m := make(map[int]int)
    for i, num := range nums {
        if v, ok := m[target - num]; ok {
            return []int{v, i}
        }
        m[num] = i
    }
    return []int{}
}
```

> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

### [219 数组�?重�?�元�? 2](https://leetcode-cn.com/problems/contains-duplicate-ii/)

**题目描述**

给定一�?整数数组和一�?整数 k，判�?数组�?�?否存在两�?不同的索�? i �? j，使�? nums [i] = nums [j]，并�? i �? j 的差�? 绝�?��? 至�?�为 k�?

示例 1:

> 输入: nums = [1,2,3,1], k = 3
> 输出: true

示例 2:

> 输入: nums = [1,0,1,1], k = 1
> 输出: true

示例 3:

> 输入: nums = [1,2,3,1,2,3], k = 2
> 输出: false

**Hashmap**

这个题目和我�?上面那个数组�?的重复数字几乎相同，�?不过�?增加了一�?判断相隔�?否小�? K 位的条件，我�?先用 HashMap 来做一哈，和刚才思路一致，我们直接看代码就能整�?

Java Code:

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        //特殊情况
        if (nums.length == 0) {
            return false;
        }
        // hashmap
        HashMap<Integer,Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            // 如果�?�?
            if (map.containsKey(nums[i])) {
                //判断�?否小于K，�?�果小于等于则直接返�?
                int abs = Math.abs(i - map.get(nums[i]));
                if (abs <= k)  return true;//小于等于则返�?
            }
            //更新索引，�?�时有两种情况，不存�?，或者存在时，将后出现的索引保存
            map.put(nums[i],i);
        }
        return false;
    }
}
```

Python3 Code:

```python
from typing import List
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int)->bool:
        # 特殊情况
        if len(nums) == 0:
            return False
        # 字典
        m = {}
        for i in range(0, len(nums)):
            # 如果�?�?
            if nums[i] in m.keys():
                # 判断�?否小于K，�?�果小于等于则直接返�?
                a = abs(i - m[nums[i]])
                if a <= k:
                    return True# 小于等于则返�?
            # 更新索引，�?�时有两种情况，不存�?，或者存在时，将后出现的索引保存
            m[nums[i]] = i
        return False
```

C++ Code:

```cpp
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_map <int, int> m;
        for(int i = 0; i < nums.size(); ++i){
            if(m.count(nums[i]) && i - m[nums[i]] <= k) return true;
            m[nums[i]] = i;
        }
        return false;
    }
};
```

Swift Code

```swift
class Solution {
    func containsNearbyDuplicate(_ nums: [Int], _ k: Int) -> Bool {
        if nums.count == 0 {
            return false
        }
        var dict:[Int:Int] = [:]
        for i in 0..<nums.count {
            // 如果�?�?
            if let v = dict[nums[i]] {
                // 判断�?否小于K，�?�果小于等于则直接返�?
                let abs = abs(i - v)
                if abs <= k {
                    return true
                }
            }
            // 更新索引，�?�时有两种情况，不存�?，或者存在时，将后出现的索引保存
            dict[nums[i]] = i
        }
        return false
    }
}
```

**HashSet**

**解析**

这个方法算是属于固定滑动窗口。我�?需要维护一�?长度�? K 的滑动窗口，如果窗口内含有�?�值，则直接返�? true，尾部进入新元素时，则将头部的元素去掉。继�?查看�?否含有�?�元素。下面我�?来看视�?�解析吧，保证以下就能搞懂了�?

![leetcode219数组�?重�?�元�?2](https://cdn.jsdelivr.net/gh/tan45du/test1@master/20210122/leetcode219数组�?重�?�元�?2.6m947ehfpb40.gif)

**题目代码**

Java Code

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        //特殊情况
        if (nums.length == 0) {
            return false;
        }
        // set
        HashSet<Integer> set = new HashSet<>();
        for (int i = 0; i < nums.length; ++i) {
            //�?有�?�元素，返回true
            if (set.contains(nums[i])) {
                return true;
            }
            // 添加新元�?
            set.add(nums[i]);
            //维护窗口长度
            if (set.size() > k) {
                set.remove(nums[i-k]);
            }
        }
        return false;
    }
}
```

Python3 Code:

```python
from typing import List
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int)->bool:
        # 特殊情况
        if len(nums) == 0:
            return False
        # 集合
        s = set()
        for i in range(0, len(nums)):
            # 如果�?有，返回True
            if nums[i] in s:
                return True
            # 添加新元�?
            s.add(nums[i])
            # 维护窗口长度
            if len(s) > k:
                s.remove(nums[i - k])
        return False
```

C++ Code:

```cpp
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        multiset <int> S;
        for(int i = 0; i < nums.size(); ++i){
            if(S.count(nums[i])) return true;
            S.insert(nums[i]);
            if(S.size() > k) S.erase(nums[i - k]);
        }
        return false;
    }
};
```

Swift Code

```swift
class Solution {
    func containsNearbyDuplicate(_ nums: [Int], _ k: Int) -> Bool {
        if nums.count == 0 {
            return false
        }
        var set:Set<Int> = []
        for i in 0..<nums.count {
            // �?有�?�元素，返回true
            if set.contains(nums[i]) {
                return true
            }
            // 添加新元�?
            set.insert(nums[i])
            if set.count > k {
                set.remove(nums[i - k])
            }
        }
        return false
    }
}
```

Go Code:

```go
func containsNearbyDuplicate(nums []int, k int) bool {
    length := len(nums)
    if length == 0 {
        return false
    }
    m := map[int]int{}
    for i := 0; i < length; i++ {
        if v, ok := m[nums[i]]; ok {
            if i - v <= k {
                return true
            }
        }
        m[nums[i]] = i
    }
    return false
}
```


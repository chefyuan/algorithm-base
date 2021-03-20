### leetcode 219 数组中重复元素2

**题目描述**

给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 nums [i] = nums [j]，并且 i 和 j 的差的 绝对值 至多为 k。

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

这个题目和我们上面那个数组中的重复数字几乎相同，只不过是增加了一个判断相隔是否小于K位的条件，我们先用 HashMap 来做一哈，和刚才思路一致，我们直接看代码就能整懂

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
            // 如果含有
            if (map.containsKey(nums[i])) {
                //判断是否小于K，如果小于则直接返回
                int abs = Math.abs(i - map.get(nums[i]));
                if (abs <= k)  return true;//小于则返回        
            }
            //更新索引，此时有两种情况，不存在，或者存在时，将后出现的索引保存
            map.put(nums[i],i);
        }
        return false;
    }
}
```

**HashSet**

**解析**

这个方法算是属于固定滑动窗口。我们需要维护一个长度为 K 的滑动窗口，如果窗口内含有该值，则直接返回 true，尾部进入新元素时，则将头部的元素去掉。继续查看是否含有该元素。下面我们来看视频解析吧，保证以下就能搞懂了。

![leetcode219数组中重复元素2](https://cdn.jsdelivr.net/gh/tan45du/test1@master/20210122/leetcode219数组中重复元素2.6m947ehfpb40.gif)



**题目代码**

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
            //含有该元素，返回true
            if (set.contains(nums[i])) {
                return true;
            }
            // 添加新元素
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


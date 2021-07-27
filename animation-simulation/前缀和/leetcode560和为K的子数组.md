> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [560. 和为 K 的子数组](https://leetcode-cn.com/problems/subarray-sum-equals-k/)

**题目描述**

> 给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

**示例 1 :**

> 输入:nums = [1,1,1], k = 2
> 输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。

**暴力法**

**解析**

这个题目的题意很容易理解，就是让我们返回和为 k 的子数组的个数，所以我们直接利用双重循环解决该题，这个是很容易想到的。我们直接看代码吧。

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
         int len = nums.length;
         int sum = 0;
         int count = 0;
         for (int i = 0; i < len; ++i) {
             for (int j = i; j < len; ++j) {
                 sum += nums[j];
                 if (sum == k) {
                     count++;
                 }
             }
             sum = 0;
         }
         return count;
    }
}
```

下面我们我们使用前缀和的方法来解决这个题目，那么我们先来了解一下前缀和是什么东西。其实这个思想我们很早就接触过了。见下图

![](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/微信截图_20210113193831.4wk2b9zc8vm0.png)

我们通过上图发现，我们的 presum 数组中保存的是 nums 元素的和，presum[1] = presum[0] + nums[0];

presum [2] = presum[1] + nums[1],presum[3] = presum[2] + nums[2] ... 所以我们通过前缀和数组可以轻松得到每个区间的和，

例如我们需要获取 nums[2] 到 nums[4] 这个区间的和，我们则完全根据 presum 数组得到，是不是有点和我们之前说的字符串匹配算法中 BM,KMP 中的 next 数组和 suffix 数组作用类似。

那么我们怎么根据 presum 数组获取 nums[2] 到 nums[4] 区间的和呢？见下图

![前缀和](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/前缀和.77twdj3gpkg0.png)

所以我们 nums[2] 到 nums[4] 区间的和则可以由 presum[5] - presum[2] 得到。

也就是前 5 项的和减去前 2 项的和，得到第 3 项到第 5 项的和。那么我们可以遍历 presum 就能得到和为 K 的子数组的个数啦。

直接上代码。

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        //前缀和数组
        int[] presum = new int[nums.length+1];
        for (int i = 0; i < nums.length; i++) {
            //这里需要注意，我们的前缀和是presum[1]开始填充的
            presum[i+1] = nums[i] + presum[i];
        }
        //统计个数
        int count = 0;
        for (int i = 0; i < nums.length; ++i) {
            for (int j = i; j < nums.length; ++j) {
                //注意偏移，因为我们的nums[2]到nums[4]等于presum[5]-presum[2]
                //所以这样就可以得到nums[i,j]区间内的和
                if (presum[j+1] - presum[i] == k) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

我们通过上面的例子我们简单了解了前缀和思想，那么我们如果继续将其优化呢？

**前缀和 + HashMap**

**解析**

其实我们在之前的两数之和中已经用到了这个方法，我们一起来回顾两数之和 HashMap 的代码.

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        HashMap<Integer,Integer> map  = new HashMap<>();
        //一次遍历
        for (int i = 0; i < nums.length; ++i) {
            //存在时，我们用数组得值为 key，索引为 value
            if (map.containsKey(target - nums[i])){
               return new int[]{i,map.get(target-nums[i])};
            }
            //存入值
            map.put(nums[i],i);
        }
        //返回
        return new int[]{};
    }
}
```

上面代码中，我们将数组的值和索引存入 map 中，当我们遍历到某一值 x 时，判断 map 中是否含有 target - x，即可。其实我们现在这个题目和两数之和原理是一致的，只不过我们是将**所有的前缀和**该**前缀和出现的次数**存到了 map 里。下面我们来看一下代码的执行过程。

**动图解析**

![](https://img-blog.csdnimg.cn/2021031809231883.gif#pic_center)

**题目代码**

Java Code：

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        if (nums.length == 0) {
            return 0;
        }
        HashMap<Integer,Integer> map = new HashMap<>();
        //细节，这里需要预存前缀和为 0 的情况，会漏掉前几位就满足的情况
        //例如输入[1,1,0]，k = 2 如果没有这行代码，则会返回0,漏掉了1+1=2，和1+1+0=2的情况
        //输入：[3,1,1,0] k = 2时则不会漏掉
        //因为presum[3] - presum[0]表示前面 3 位的和，所以需要map.put(0,1),垫下底
        map.put(0, 1);
        int count = 0;
        int presum = 0;
        for (int x : nums) {
            presum += x;
            //当前前缀和已知，判断是否含有 presum - k的前缀和，那么我们就知道某一区间的和为 k 了。
            if (map.containsKey(presum - k)) {
                count += map.get(presum - k);//获取presum-k前缀和出现次数
            }
            //更新
            map.put(presum,map.getOrDefault(presum,0) + 1);
        }
        return count;
    }
}
```

C++ Code：

```cpp
public:
    int subarraySum(vector<int>& nums, int k) {
         if (nums.size() == 0) {
            return 0;
        }
        map <int, int> m;
        //细节，这里需要预存前缀和为 0 的情况，会漏掉前几位就满足的情况
        //例如输入[1,1,0]，k = 2 如果没有这行代码，则会返回0,漏掉了1+1=2，和1+1+0=2的情况
        //输入：[3,1,1,0] k = 2时则不会漏掉
        //因为presum[3] - presum[0]表示前面 3 位的和，所以需要m.insert({0,1}),垫下底
        m.insert({0, 1});
        int count = 0;
        int presum = 0;
        for (int x : nums) {
            presum += x;
            //当前前缀和已知，判断是否含有 presum - k的前缀和，那么我们就知道某一区间的和为 k 了。
            if (m.find(presum - k) != m.end()) {
                count += m[presum - k];//获取presum-k前缀和出现次数
            }
            //更新
           if(m.find(presum) != m.end()) m[presum]++;
           else m[presum] = 1;
        }
        return count;
    }
};
```

Go Code:

```GO
func subarraySum(nums []int, k int) int {
    m := map[int]int{}
    // m存的是前缀和，没有元素的时候，和为0，且有1个子数组(空数组)满足条件，即m[0] = 1
    m[0] = 1
    sum := 0
    cnt := 0
    for _, num := range nums {
        sum += num
        if v, ok := m[sum - k]; ok {
            cnt += v
        }
        // 更新满足前缀和的子数组数量
        m[sum]++
    }
    return cnt
}
```

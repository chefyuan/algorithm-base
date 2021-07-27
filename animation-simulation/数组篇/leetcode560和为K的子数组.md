> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

### [leetcode560. 和为 K 的子数组](https://leetcode-cn.com/problems/subarray-sum-equals-k/)

**题目描述**

> 给定一�?整数数组和一�?整数 k，你需要找到�?�数组中和为 k 的连�?的子数组的个数�?

**示例 1 :**

> 输入:nums = [1,1,1], k = 2
> 输出: 2 , [1,1] �? [1,1] 为两种不同的情况�?

**暴力�?**

**解析**

这个题目的�?�意很�?�易理解，就�?让我�?返回和为 k 的子数组的个数，所以我�?直接利用双重�?�?解决该�?�，这个�?很�?�易想到的。我�?直接看代码吧�?

Java Code:

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

Python3 版本的代码会超时

Swift 版本的代码会超时

下面我们我们使用前缀和的方法来解决这�?题目，那么我�?先来了解一下前缀和是什么东西。其实这�?思想我们很早就接触过了。�?�下�?

![](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/�?信截图_20210113193831.4wk2b9zc8vm0.png)

我们通过上图发现，我�?�? presum 数组�?保存的是 nums 元素的和，presum[1] = presum[0] + nums[0];

presum [2] = presum[1] + nums[1],presum[3] = presum[2] + nums[2] ... 所以我�?通过前缀和数组可以轻松得到每�?区间的和�?

例�?�我�?需要获�? nums[2] �? nums[4] 这个区间的和，我�?则完全根�? presum 数组得到，是不是有点和我�?之前说的字�?�串匹配算法�? BM,KMP �?�? next 数组�? suffix 数组作用类似�?

那么我们怎么根据 presum 数组获取 nums[2] �? nums[4] 区间的和�?？�?�下�?

![前缀和](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/前缀�?.77twdj3gpkg0.png)

所以我�? nums[2] �? nums[4] 区间的和则可以由 presum[5] - presum[2] 得到�?

也就�?�? 5 项的和减去前 2 项的和，得到�? 3 项到�? 5 项的和。那么我�?�?以遍�? presum 就能得到和为 K 的子数组的个数啦�?

直接上代码�?

Java Code:

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        //前缀和数�?
        int[] presum = new int[nums.length+1];
        for (int i = 0; i < nums.length; i++) {
            //这里需要注意，我们的前缀和是presum[1]开始填充的
            presum[i+1] = nums[i] + presum[i];
        }
        //统�?�个�?
        int count = 0;
        for (int i = 0; i < nums.length; ++i) {
            for (int j = i; j < nums.length; ++j) {
                //注意偏移，因为我�?的nums[2]到nums[4]等于presum[5]-presum[2]
                //所以这样就�?以得到nums[i,j]区间内的�?
                if (presum[j+1] - presum[i] == k) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

Python3 版本的代码也会超�?

我们通过上面的例子我�?简单了解了前缀和思想，那么我�?如果继续将其优化�?�?

**前缀�? + HashMap**

**解析**

其实我们在之前的两数之和�?已经用到了这�?方法，我�?一起来回顾两数之和 HashMap 的代�?.

Java Code:

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        HashMap<Integer,Integer> map  = new HashMap<>();
        //一次遍�?
        for (int i = 0; i < nums.length; ++i) {
            //存在时，我们用数组得值为 key，索引为 value
            if (map.containsKey(target - nums[i])){
               return new int[]{i,map.get(target-nums[i])};
            }
            //存入�?
            map.put(nums[i],i);
        }
        //返回
        return new int[]{};
    }
}
```

上面代码�?，我�?将数组的值和索引存入 map �?，当我们遍历到某一�? x 时，判断 map �?�?否含�? target - x，即�?。其实我�?现在这个题目和两数之和原理是一致的，只不过我们�?�?**所有的前缀�?**�?**前缀和出现的次数**存到�? map 里。下面我�?来看一下代码的执�?�过程�?

**动图解析**

![](https://img-blog.csdnimg.cn/2021031809231883.gif#pic_center)

**题目代码**

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        if (nums.length == 0) {
            return 0;
        }
        HashMap<Integer,Integer> map = new HashMap<>();
        //细节，这里需要�?�存前缀和为 0 的情况，会漏掉前几位就满足的情况
        //例�?�输�?[1,1,0]，k = 2 如果没有这�?�代码，则会返回0,漏掉�?1+1=2，和1+1+0=2的情�?
        //输入：[3,1,1,0] k = 2时则不会漏掉
        //因为presum[3] - presum[0]表示前面 3 位的和，所以需要map.put(0,1),�?下底
        map.put(0, 1);
        int count = 0;
        int presum = 0;
        for (int x : nums) {
            presum += x;
            //当前前缀和已知，判断�?否含�? presum - k的前缀和，那么我们就知道某一区间的和�? k 了�?
            if (map.containsKey(presum - k)) {
                count += map.get(presum - k);//获取presum-k前缀和出现�?�数
            }
            //更新
            map.put(presum,map.getOrDefault(presum,0) + 1);
        }
        return count;
    }
}
```

Swift Code

```swift
class Solution {
    func subarraySum(_ nums: [Int], _ k: Int) -> Int {
        if nums.count == 0 {
            return 0
        }
        var map: [Int: Int] = [:]
        map[0] = 1 // 需要添加入一�?元素�?底，已支持前几位就满足的情况
        var presum = 0, count = 0

        for x in nums {
            presum += x
            //当前前缀和已知，判断�?否含�? presum - k的前缀和，那么我们就知道某一区间的和�? k 了�?
            if let v = map[presum - k] {
                count += v //获取presum-k前缀和出现�?�数
            }
            map[presum] = (map[presum] ?? 0) + 1
        }
        return count
    }
}
```

C++ Code

```C++
class Solution
{
public:
    int subarraySum(vector<int> &nums, int k)
    {
        unordered_map<int, int> smp;
        int sum = 0;
        //初�?�化"最外面"�?0
        smp[0] = 1;
        int result = 0;
        for(int i = 0; i < nums.size(); i++)
        {
            sum += nums[i];
            auto mp = smp.find(sum - k);
            if (mp != smp.end())
            {
                //map里面存的一定是在前面的元素
                //�?以尝试将map的value�?为数�?
                result += mp->second;
            }
            smp[sum]++;
        }

        return result;
    }
};
```

Go Code:

```go
func subarraySum(nums []int, k int) int {
    m := map[int]int{}
    m[0] = 1
    sum := 0
    cnt := 0
    for _, num := range nums {
        sum += num
        if v, ok := m[sum - k]; ok {
            cnt += v
        }
        m[sum]++
    }
    return cnt
}
```


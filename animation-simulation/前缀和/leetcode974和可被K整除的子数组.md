> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [974. 和可�? K 整除的子数组](https://leetcode-cn.com/problems/subarray-sums-divisible-by-k/)

**题目描述**

> 给定一�?整数数组 A，返回其�?元素之和�?�? K 整除的（连续、非空）子数组的数目�?

**示例�?**

> 输入：A = [4,5,0,-2,-3,1], K = 5
> 输出�?7

**解释�?**

> �? 7 �?子数组满足其元素之和�?�? K = 5 整除�?
> [4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]

**前缀�?+HashMap**

**解析**

我们在�?�文的�??一�? **和为 K 的子数组 **�?，我�?需要求出满足条件的区间，�?�下�?

![�?信截图_20210115194113](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/�?信截图_20210115194113.5e56re9qdic0.png)

我们需要找到满足，和为 K 的区间。我�?此时 presum �?已知的，k 也是已知的，我们�?需要找�? presum - k 区间的个数，就能得到 k 的区间个数。但�?我们在当前�?�目�?应�?�怎么做呢？�?�下图�?

![�?信截图_20210115150520](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/�?信截图_20210115150520.3kh5yiwwmlm0.png)

我们在之前的例子�?说到，presum[j+1] - presum[i] �?以得�? nums[i] + nums[i+1]+.... nums[j]，也就是[i,j]区间的和�?

那么我们想�?�判�?区间 [i,j] 的和�?否能整除 K，也就是上图�?�?色那一段是否能整除 K，那么我�?�?需判断

(presum[j+1] - presum[i] ) % k �?否等�? 0 即可�?

我们假�?? (presum[j+1] - presum[i] ) % k == 0；则

presum[j+1] % k - presum[i] % k == 0;

presum[j +1] % k = presum[i] % k ;

我们 presum[j +1] % k 的�? key �?已知的，则是当前�? presum �? k 的关系，我们�?需要知道之前的前缀区间里含有相同余�? （key）的�?数。则能�?�知道当前能够整�? K 的区间个数。�?�下�?

![�?信截图_20210115152113](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/�?信截图_20210115152113.606bcpexpww0.png)

**题目代码**

```java
class Solution {
    public int subarraysDivByK(int[] A, int K) {
        HashMap<Integer,Integer> map = new HashMap<>();
        map.put(0,1);
        int presum = 0;
        int count = 0;
        for (int x : A) {
             presum += x;
             //当前 presum �? K的关系，余数�?几，当�??除数为负数时取模结果为负数，需要纠�?
             int key = (presum % K + K) % K;
             //查�?�哈希表获取之前key也就�?余数的�?�数
             if (map.containsKey(key)) {
                 count += map.get(key);
             }
             //存入哈希表当前key，也就是余数
             map.put(key,map.getOrDefault(key,0)+1);
        }
        return count;
    }
}
```

我们看到上面代码�?有一段代码是这样�?

```java
int key = (presum % K + K) % K;
```

这是为什么呢？不能直接用 presum % k 吗？

这是因为当我�? presum 为负数时，需要�?�其纠�?�。纠正前(-1) %2 = (-1)，纠正之�? ( (-1) % 2 + 2) % 2=1 保存在哈希表�?的则�? 1.则不会漏掉部分情况，例�?�输入为 [-1,2,9],K = 2 如果不�?�其纠�?�则会漏掉区�? [2] 此时 2 % 2 = 0，�?�合条件，但�?不会�?计数�?

那么这个题目我们�?不可以用数组，代�? map �?？当然也�?�?以的，因为�?�时我们的哈希表存的�?余数，余数最大也�?不过�? K-1 所以我�?�?以用固定长度 K 的数组来模拟哈希表�?

Java Code:

```java
class Solution {
    public int subarraysDivByK(int[] A, int K) {
        int[] map = new int[K];
        map[0] = 1;
        int len = A.length;
        int presum = 0;
        int count = 0;
        for (int i = 0; i < len; ++i) {
            presum += A[i];
            //求key
            int key = (presum % K + K) % K;
            //count添加次数，并将当前的map[key]++;
            count += map[key]++;
        }
        return count;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    int subarraysDivByK(vector<int>& A, int K) {
        vector <int> map (K, 0);
      	int len = A.size();
        int count = 0;
        int presum = 0;
        map[0] = 1;
         for (int i = 0; i < len; ++i) {
            presum += A[i];
            //求key
            int key = (presum % K + K) % K;
            //count添加次数，并将当前的map[key]++;
            count += (map[key]++);
        }
        return count;
    }
};
```

Go Code:

```go
func subarraysDivByK(nums []int, k int) int {
    m := make(map[int]int)
    cnt := 0
    sum := 0
    m[0] = 1
    for _, num := range nums {
        sum += num
        key := (sum % k + k) % k
        cnt += m[key]
        m[key]++
    }
    return cnt
}
```


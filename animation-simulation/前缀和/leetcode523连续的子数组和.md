> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [523. 连续的子数组和](https://leetcode-cn.com/problems/continuous-subarray-sum/)

**题目描述**

> 给定一�?包含 非负�? 的数组和一�?�?�? 整数 k，编写一�?函数来判�?该数组是否含有连�?的子数组，其大小至少�? 2，且总和�? k 的倍数，即总和�? n\*k，其�? n 也是一�?整数�?

**示例 1�?**

> 输入：[23,2,4,6,7], k = 6
> 输出：True

解释：[2,4] �?一�?大小�? 2 的子数组，并且和�? 6�?

**示例 2�?**

> 输入：[23,2,6,4,7], k = 6
> 输出：True

解释：[23,2,6,4,7]�?大小�? 5 的子数组，并且和�? 42�?

**前缀�? + HashMap**

这个题目算是对刚才那�?题目的升级，前半部分�?一样的，都�?为了让你找到能�?? K 整除的子数组，但�?这里加了一�?限制，那就是子数组的大小至少�? 2，那么我�?应�?�怎么判断子数组的长度�?？我�?�?以根�?索引来进行判�?，�?�下图�?

![�?信截图_20210115174825](https://img-blog.csdnimg.cn/img_convert/953d09fbfffab9298152e143a39c85c0.png)

此时我们 K = 6, presum % 6 = 4 也找到了相同余数的前缀子数�? [0,1] 但是我们此时指针指向�? 2，我�?的前缀子区�? [0,1]的下界为 1，所�? 2 - 1 = 1，但我们的中间区间的长度小于 2，所以不能返�? true，需要继�?遍历，那我们有两�?区间[0,1],[0,2]都满�? presum % 6 = 4，那我们哈希表中保存的下标应该是 1 还是 2 �?？我�?保存的是 1，�?�果我们保存的是较大的那�?索引，则会出现下列情况，见下图�?

![�?信截图_20210115175122](https://img-blog.csdnimg.cn/img_convert/7bbd04ac578074d5fbccae7ab384f061.png)

此时，仍会显示不满足子区间长度至少为 2 的情况，仍会继续遍历，但�?我们此时�? [2,3]区间已经满足该情况，返回 true，所以我�?往哈希表存值时，只存一次，即最小的索引即可。下面我�?看一下�?��?�的两个细节

细节 1：我�?�? k 如果�? 0 时怎么办，因为 0 不可以做除数。所以当我们 k �? 0 时可以直接存到数组里，例如输入为 [0,0] , K = 0 的情�?

细节 2：另外一�?就是之前我们都是统�?�个数，value 里保存的�?次数，但�?此时我们加了一�?条件就是长度至少�? 2，保存的�?索引，所以我�?不能继续 map.put(0,1)，应该赋初值为 map.put(0,-1)。这样才不会漏掉一些情况，例�?�我�?的数组为[2,3,4],k = 1,当我�? map.put(0,-1) 时，当我�?遍历�? nums[1] �? 3 时，则可以返�? true，因�? 1-�?-1�?= 2�?5 % 1=0 , 同时满足�?

**视�?�解�?**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210318094237943.gif#pic_center)

**题目代码**

Java Code:

```java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        HashMap<Integer,Integer> map = new HashMap<>();
        //细节2
        map.put(0,-1);
        int presum = 0;
        for (int i = 0; i < nums.length; ++i) {
            presum += nums[i];
            //细节1，防�? k �? 0 的情�?
            int key = k == 0 ? presum : presum % k;
            if (map.containsKey(key)) {
                if (i - map.get(key) >= 2) {
                     return true;
                }
                //因为我们需要保存最小索引，当已经存在时则不用再次存入，不然会更新索引�?
                continue;
            }
            map.put(key,i);
        }
        return false;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        map <int, int> m;
        //细节2
        m.insert({0,-1});
        int presum = 0;
        for (int i = 0; i < nums.size(); ++i) {
            presum += nums[i];
            //细节1，防�? k �? 0 的情�?
            int key = k == 0 ? presum : presum % k;
            if (m.find(key) != m.end()) {
                if (i - m[key] >= 2) {
                     return true;
                }
                //因为我们需要保存最小索引，当已经存在时则不用再次存入，不然会更新索引�?
                continue;
            }
            m.insert({key, i});
        }
        return false;
    }
};
```

Go Code:

```go
func checkSubarraySum(nums []int, k int) bool {
    m := map[int]int{}
    // 由于前缀�?%k�?能为0，所以需要给出没有元素的时候，索引位置，即-1
    m[0] = -1
    sum := 0
    for i, num := range nums {
        sum += num
        key := sum % k
        /*
        // 题目�?告诉k >= 1
        key := sum
        if k != 0 {
            key = sum % k
        }
        */
        if v, ok := m[key]; ok {
            if i - v >= 2 {
                return true
            }
            // 避免更新最小索�?
            continue
        }
        // 保存的是最小的索引
        m[key] = i
    }
    return false
}
```


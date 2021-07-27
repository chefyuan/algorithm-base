> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [66. 加一](https://leetcode-cn.com/problems/plus-one/)

**题目描述**

> 给定一�?�? 整数 组成�? 非空 数组所表示的非负整数，在�?�数的基础上加一�?
>
> 最高位数字存放在数组的首位�? 数组�?每个元素�?存储单个数字�?
>
> 你可以假设除了整�? 0 之�?�，这个整数不会以零开头�?

**示例 1�?**

> 输入：digits = [1,2,3]
> 输出：[1,2,4]
> 解释：输入数组表示数�? 123�?

**示例 2�?**

> 输入：digits = [4,3,2,1]
> 输出：[4,3,2,2]
> 解释：输入数组表示数�? 4321�?

**示例 3�?**

输入：digits = [0]
输出：[1]

**数组遍历**

**题目解析**

我们思考一下，加一的情况一共有几�?�情况呢？是不是有以下三种情�?

![加一](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/加一.3lp9zidw61s0.png)

则我�?根据什么来判断属于�?几�?�情况呢�?

我们�?以根�?当前�? �? 10 来判�?，这样我�?就可以区分属于�??几�?�情况了，大家直接看代码吧，很�?�易理解的�?

Java Code:

```java
class Solution {
    public int[] plusOne(int[] digits) {
        //获取长度
        int len = digits.length;
        for (int i = len-1; i >= 0; i--) {
            digits[i] = (digits[i] + 1) % 10;
            //�?一种和�?二�?�情况，如果此时某一位不�? 0 ，则直接返回即可�?
            if (digits[i] != 0) {
                return digits;
            }

        }
        //�?三�?�情况，因为数组初�?�化每一位都�?0，我�?�?需将�?�位设为1即可
        int[] arr = new int[len+1];
        arr[0] = 1;
        return arr;
    }
}
```

Python Code:

```python
from typing import List
class Solution:
    def plusOne(self, digits: List[int])->List[int]:
        # 获取长度
        leng = len(digits)
        for i in range(leng - 1, -1, -1):
            digits[i] = (digits[i] + 1) % 10
            # �?一种和�?二�?�情况，如果此时某一位不�? 0 ，则直接返回即可�?
            if digits[i] != 0:
                return digits
        # �?三�?�情况，因为数组初�?�化每一位都�?0，我�?�?需将�?�位设为1即可
        arr = [0] * (leng + 1)
        arr[0] = 1
        return arr
```

C++ Code:

```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        for(int i = digits.size() - 1; i >= 0; --i){
            digits[i] = (digits[i] + 1)%10;
            if(digits[i]) return digits;
        }
        for(int & x: digits) x = 0;
        digits.emplace_back(1);
        reverse(digits.begin(), digits.end());
        return digits;
    }
};
```

Swift Code:

```swift
class Solution {
    func plusOne(_ digits: [Int]) -> [Int] {
        let count = digits.count
        var digits = digits
        for i in stride(from: count - 1, through: 0, by: -1) {
            digits[i] = (digits[i] + 1) % 10
            if digits[i] != 0 {
                return digits
            }
        }
        var arr: [Int] = Array.init(repeating: 0, count: count + 1)
        arr[0] = 1
        return arr
    }
}
```

Go Code:

```go
func plusOne(digits []int) []int {
    l := len(digits)
    for i := l - 1; i >= 0; i-- {
        digits[i] = (digits[i] + 1) % 10
        if digits[i] != 0 {
            return digits
        }
    }
    digits = append([]int{1}, digits...)
    return digits
}
```


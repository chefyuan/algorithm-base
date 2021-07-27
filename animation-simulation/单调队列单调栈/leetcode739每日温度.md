> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [739. 每日温度](https://leetcode-cn.com/problems/daily-temperatures/)

题目描述�?

> 请根�?每日 气温 列表，重新生成一�?列表。�?�应位置的输出为：�?�想观测到更高的气温，至少需要等待的天数。�?�果气温在这之后都不会升高，请在该位�?�? 0 来代替�?

示例 1�?

> 输入�? temperatures = [73, 74, 75, 71, 69, 72, 76, 73]
>
> 输出：arr = [1, 1, 4, 2, 1, 1, 0, 0]

示例 2�?

> 输入：temperatures = [30,30,31,45,31,34,56]
>
> 输出：arr = [2,1,1,3,1,1,0]

#### 题目解析

其实我们�?以换种方式理解这�?题目，比如我�? temperatures[0] = 30,则我�?需要找到后面�??一�?�? 30 大的数，也就�? 31�?31 的下标为 2�?30 的下标为 0 ，则我们的返回数�? arr[0] = 2�?

理解了�?�目之后我们来�?�一下解题思路�?

遍历数组，数组中的值为待入栈元素，待入栈元素入栈时会先跟栈顶元素进行�?�比，�?�果小于该值则入栈，�?�果大于则将栈顶元素出栈，新的元素入栈�?

例�?�栈顶为 69，新的元素为 72，则 69 出栈�?72 入栈。并赋值给 arr�?69 的索引为 4�?72 的索引为 5，则 arr[4] = 5 - 4 = 1，这�?题目用到的是单调栈的思想，下面我�?来看一下�?��?�解析�?

![](https://img-blog.csdnimg.cn/20210319163137996.gif)

�?：栈�?的括号内的值，代表索引对应的元素，我们的入栈的为索引值，为了便于理解将其对应的值写在了�?号中

```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        int len = T.length;
        if (len == 0) {
            return T;
        }
        Stack<Integer> stack = new Stack<>();
        int[] arr = new int[len];
        int t = 0;
        for (int i = 0; i < len; i++) {
            //单调�?
            while (!stack.isEmpty() && T[i] > T[stack.peek()]){
                  arr[stack.peek()] = i - stack.pop();
            }
            stack.push(i);
        }
        return arr;

    }
}
```

**GO�?言版本�?**

```go
func dailyTemperatures(temperatures []int) []int {
    l := len(temperatures)
    if l == 0 {
        return temperatures
    }
    stack := []int{}
    arr   := make([]int, l)
    for i := 0; i < l; i++ {
        for len(stack) != 0 && temperatures[i] > temperatures[stack[len(stack) - 1]] {
            idx := stack[len(stack) - 1]
            arr[idx] = i - idx
            stack = stack[: len(stack) - 1]
        }
        // 栈保存的�?索引
        stack = append(stack, i)
    }
    return arr
}
```


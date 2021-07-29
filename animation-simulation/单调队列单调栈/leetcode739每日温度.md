> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [739. 每日温度](https://leetcode-cn.com/problems/daily-temperatures/)

题目描述：

> 请根据每日 气温 列表，重新生成一个列表。对应位置的输出为：要想观测到更高的气温，至少需要等待的天数。如果气温在这之后都不会升高，请在该位置用 0 来代替。

示例 1：

> 输入： temperatures = [73, 74, 75, 71, 69, 72, 76, 73]
>
> 输出：arr = [1, 1, 4, 2, 1, 1, 0, 0]

示例 2：

> 输入：temperatures = [30,30,31,45,31,34,56]
>
> 输出：arr = [2,1,1,3,1,1,0]

#### 题目解析

其实我们可以换种方式理解这个题目，比如我们 temperatures[0] = 30,则我们需要找到后面第一个比 30 大的数，也就是 31，31 的下标为 2，30 的下标为 0 ，则我们的返回数组 arr[0] = 2。

理解了题目之后我们来说一下解题思路。

遍历数组，数组中的值为待入栈元素，待入栈元素入栈时会先跟栈顶元素进行对比，如果小于该值则入栈，如果大于则将栈顶元素出栈，新的元素入栈。

例如栈顶为 69，新的元素为 72，则 69 出栈，72 入栈。并赋值给 arr，69 的索引为 4，72 的索引为 5，则 arr[4] = 5 - 4 = 1，这个题目用到的是单调栈的思想，下面我们来看一下视频解析。

![](https://img-blog.csdnimg.cn/20210319163137996.gif)

注：栈中的括号内的值，代表索引对应的元素，我们的入栈的为索引值，为了便于理解将其对应的值写在了括号中

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
            //单调栈
            while (!stack.isEmpty() && T[i] > T[stack.peek()]){
                  arr[stack.peek()] = i - stack.pop();
            }
            stack.push(i);
        }
        return arr;

    }
}
```

GO Code:

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
        // 栈保存的是索引
        stack = append(stack, i)
    }
    return arr
}
```

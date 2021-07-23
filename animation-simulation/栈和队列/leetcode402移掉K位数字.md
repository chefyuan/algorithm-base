> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [402. 移掉 K 位数字](https://leetcode-cn.com/problems/remove-k-digits/)

今天给大家带来一个栈的中等题目，移掉 K 位数字，题目很简单，但是很有趣。另外明天继续给大家带来一道栈和队列题目（困难），那么咱们的栈和队列模块就结束啦，下周开始整字符串的题目啦！

### 题目描述

给定一个以字符串表示的非负整数 num，移除这个数中的 k 位数字，使得剩下的数字最小。

注意:

> num 的长度小于 10002 且 ≥ k。
> num 不会包含任何前导零。

示例 1 :

> 输入: num = "1432219", k = 3
> 输出: "1219"
> 解释: 移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219。

示例 2 :

> 输入: num = "10200", k = 1
> 输出: "200"
> 解释: 移掉首位的 1 剩下的数字为 200. 注意输出不能有任何前导零。

示例 3 :

> 输入: num = "10", k = 2
> 输出: "0"
> 解释: 从原数字移除所有的数字，剩余为空就是 0

题目很容易理解，而且也很容易实现，因为在示例中几乎把所有特殊情况都进行了举例，我们直接代码实现就好啦。

### 栈（贪心）

下面我们来看一下用栈的解题思路，因为我们需要删除掉 K 位数字得到最小值，那么我们需要注意的是，删除的数字应该尽量在高位，则当前位小于前一位时，对前一位出栈，当前位入栈。大家思考一下思路是不是这样呢？

另外我们需要注意的是，仅删除 K 位数字，得到最小值，比如 54321，我们删除 3 位，得到 21。但是刚才我们说当前位小于前一位时，则前一位出栈，当前位入栈，所以我们需要加上删除 K 位的规则。

废话不多说我们直接上动图，把该题吃透！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210320141440557.gif)

PPT 中的文字

> 这里需要注意的是，我们不需要将 0 入栈，因为 0 如果处于栈底，没有比它更小的值所以它不会被移除，我们只有在最后才有机会处理它。因为我们的 010 = 10 ，首位 0 是需要在最后去掉的。所以我们这里可以直接不让其入栈，continue 掉这次循环，也不改变 K 值，这样我们最后出栈处理时就不用考虑啦。这样逻辑就比官方题解好理解一些，也简洁一些。

> 这里需要注意的是，我们的 K 值还为 2，我们目前仅删除 2 位数字，但是我们需要删除 4 位，但是后面的几位都是当前位大于前一位。所以我们需要在遍历结束后再移除后面最大的两位数字

```java
class Solution {
    public String removeKdigits(String num, int k) {
        //特殊情况全部删除
        if (num.length() == k) {
            return "0";
        }
        char[] s = num.toCharArray();
        Stack<Character> stack = new Stack<>();
        //遍历数组
        for (Character i : s) {
          //移除元素的情况，k--
            while (!stack.isEmpty() && i < stack.peek() && k > 0) {
                   stack.pop();
                   k--;
            }
            //栈为空，且当前位为0时，我们不需要将其入栈
            if (stack.isEmpty() && i == '0') {
                continue;
            }
            stack.push(i);
        }
        while (k > 0) {
            stack.pop();
            k--;
        }
         if (stack.isEmpty()) {
             return "0";
         }
         //反转并返回字符串
         StringBuilder str = new StringBuilder();
         while (!stack.isEmpty()) {
             str.append(stack.pop());
         }
         return str.reverse().toString();
    }
}
```

这个题目也是很不错的，题目是精心挑选的，然后动图里面的例子也是精心构思过的。所以大家记得打卡呀！

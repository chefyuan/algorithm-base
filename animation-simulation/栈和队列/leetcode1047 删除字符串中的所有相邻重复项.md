> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [1047. 删除字符串中的所有相邻重复项](https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/)

今天给大家带来一个栈的经典题目，删除字符串中的相邻重复项，下面我们先来看一下题目描述。

给出由小写字母组成的字符串 S，重复项操作会选择**两个相邻且相同**的字母，并删除他们。

在 S 上反复执行重复项删除操作，直到无法继续删除。在完成所有重复项删除操作后返回最终字符串。答案保证唯一

示例 1：

> 输入：“abbaca”
> 输出：”ca“

​ 我们在之前的文章中介绍过删除重复项的思想，当时我们介绍的重复项可能是两个或更多，今天的题目更加简单是两字母相邻且相同。这个题目我们可以使用双指针思想解决，用来判断两个字符是否相同，但是我们这个板块的主题是栈和队列，那么我们就详细介绍一下如何用栈解答这个题目。

## 解题思路：

我们将字符入栈，然后新的字符入栈之前先于栈顶元素对比，判断是否和栈顶元素一致，如果一致则栈顶元素出栈，指针移到下一位，则就实现了去除重复元素。如果和栈顶元素不同或栈为空则将当前元素入栈。直至字符串遍历结束，另外我们需要注意的是栈是先进后出，最后我们元素出栈的时候，我们需要对字符串反转一下才为我们的答案。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210320141506967.gif)

**题目代码**

Java Code:

```java
class Solution {
    public String removeDuplicates(String S) {
         Stack<Character> stack = new Stack<>();
         char[] s = S.toCharArray();//先将字符串变成字符数组
         //特殊情况
         if (S.length() == 0 || S.length() == 1) {
             return S;
         }
         //遍历数组
         for (int i= 0; i<S.length(); i++) {
         //为空或者和栈顶元素不同时入栈
             if(stack.isEmpty() || s[i] != stack.peek()) {
                 stack.push(s[i]);
             }
         //相同出栈
             else {
                 stack.pop();
             }
         }

         StringBuilder str = new StringBuilder();
         //字符出栈
         while (!stack.isEmpty()) {
             str.append(stack.pop());
         }
         //翻转字符并返回
         return str.reverse().toString();

    }
}
```

当然这个题目也可以用 set 来做，大家可以随意发挥

C++ Code:

```cpp
class Solution {
public:
string removeDuplicates(string S) {
         string str;
         if (S.empty() || S.size() == 1) {
             return S;
         }
         for (int i = 0; i<S.size(); i++) {
             if(str.empty() || S[i] != str.back()) {
                 str.push_back(S[i]);
             }
             else {
                 str.pop_back();
             }
         }
         return str;
    }
};
```

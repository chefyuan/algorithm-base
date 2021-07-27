> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

今天我们开始了一个新的模块，栈和队列，另外昨天肝了一篇栈和队列的文章，大家可以先去了解以下，今天我们先来一道经典简单题热热身。大家一定要记得打卡，这个题目是真不错。

> 文章里的所有题目都是经过认真挑选的并且所有代码都经过测试大家可以放心食用。

题目描述

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:

> 输入: "()"
> 输出: true

示例 2:

> 输入: "(]"
> 输出: false

示例 3:

> 输入: "()]"
> 输出: false

示例 4：

> 输入:"()["
>
> 输出:false

我这里用了两种方法进行解决，第一种是利用 ArrayList，第二种是利用栈，今天主要讲 一下用栈的方法。思路很简单，我们遇到左括号就将其入栈，遇到右括号就和栈顶元素进行比较，如果是对应的则 pop 栈顶元素，不对应直接返回 false 即可。另外我们还需要考虑的就是示例 3 和示例 4 这两种情况，需要我们好好思考一下。

下面我们直接上动图。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210320141414239.gif)

题目代码：

```java
class Solution {
    public boolean isValid(String s) {
       Stack<Character> stack = new Stack<Character>();
        //循环遍历字符串
        for(char ch : s.toCharArray()){
            //入栈的三种情况
            if (ch == '(' || ch == '[' || ch == '{') {
                stack.push(ch);
            }
            //右括号对比，其中注意为空的情况
            if (ch == ')') {
                if( stack.isEmpty() || stack.pop() != '(') {
                    return false;
                }
            }
            if (ch == ']') {
                 if (stack.isEmpty() || stack.pop() != '[') {
                    return false;
                 }
            }
             if (ch == '}') {
                 if (stack.isEmpty() || stack.pop() != '{') {
                    return false;
                }
            }
        }
        //遍历结束的情况
        if (!stack.isEmpty()) {
            return false;
        }
        return true;
    }
}
```

另外我们看下另一种方法,这个方法很有趣，，我们遇到 ‘ [ ’ 时，则入栈 ' ] ' ，这样当我们遇到 ‘]’ 时只需判断栈顶元素是否和其一致即可，一致则出，继续遍历下一个，否则返回 false 。

这个方法有些巧妙，大家第一次看时可能不是那么容易理解，所以大家可以自己打一下，动脑子想一下代码逻辑。

```java
class Solution {
    public boolean isValid(String s) {
        LinkedList<Character> stack = new LinkedList<>();
        //遍历字符串
        for (char ch : s.toCharArray()) {
            //遍历到左括号时右括号入栈，右括号来对比时，只需要对比是否相同。
            if (ch == '[') stack.push(']');
            else if (ch == '(') stack.push(')');
            else if (ch == '{') stack.push('}');
            //当ch为右括号时，如果为空，或不对应，则返回false;
            else if (stack.isEmpty() || ch != stack.pop()) return false;
        }
        return stack.isEmpty();//最后判断是否为空。
    }
}
```

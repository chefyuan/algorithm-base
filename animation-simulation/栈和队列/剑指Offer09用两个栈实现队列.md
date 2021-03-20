

#### [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

今天给大家带来一个有意思的题目，思路很easy，但是刚刷题的小伙伴，示例理解起来可能会有点费劲，花里胡哨一大堆是啥意思啊。在之前的文章《不知道这篇文章合不合你的胃口》中写了栈是先进后出，队列是先进先出。本题让我们用两个先进后出的栈，完成一个先进先出的队列。我们应该怎么实现呢？

废话不多说，大家看图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210320141325908.gif)

这就是具体思路，然后我们来看一下题目示例及官方提供的函数都是什么意思。

```java
class CQueue {
    //创建队列
    public CQueue() {

    }
    //入队
    public void appendTail(int value) {

    }
    //出队
    public int deleteHead() {

    }
}
```

示例 1：

```java
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```


示例 2：

```java
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

其实也很容易理解，输入有两行第一行，为执行的函数，Cqueue代表创建队列(代表我们初始化两个栈)，appendTail代表入队操作（代表stackA入栈），deleteHead代表出队操作（代表我们stackB出栈）

第二行输入代表值，分别给每个函数传入的参数，我们发现只有appendTail函数下有对应值，因为只有该函数传入参数。

大家可以点击该链接[剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)去实现一下，下面我们看代码。

```java
class CQueue {
     //初始化两个栈
    Stack<Integer> stack1,stack2;
    public CQueue() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
 
    }
    //入队，我们往第一个栈压入值
    public void appendTail (int value) {
        stack1.push(value);
    }
    //出队
    public int deleteHead() {
        //大家可以自己思考一下为什么if条件为stack2.isEmpty(),细节所在
        if (stack2.isEmpty()) {
           //如果此时A栈没有值，则直接-1，我们可以看示例
           if (stack1.isEmpty()) {
               return -1;
           }
           //将A栈的值，压入B栈中
           while (!stack1.isEmpty()) {
               stack2.push(stack1.pop());
           }
        }
        return stack2.pop();
    }
}
```


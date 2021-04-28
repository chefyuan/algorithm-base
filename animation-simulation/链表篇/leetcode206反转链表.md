今天咱们说一道非常简单但是很经典的面试题，思路很容易，但是里面细节挺多，所以我们还是需要注意。

我们先来看一下题目描述

#### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

反转一个单链表。

**示例:**

> 输入: 1->2->3->4->5->NULL
> 输出: 5->4->3->2->1->NULL

该题目我们刚开始刷题的同学可能会想到先保存到数组中，然后从后往前遍历数组，重新组成链表，这样做是可以 AC 的，但是我们机试时往往不允许我们修改节点的值，仅仅是修改节点的指向。所以我们应该用什么方法来解决呢？

我们先来看动图，看看我们能不能理解。然后再对动图进行解析。

![](https://img-blog.csdnimg.cn/20210323191331552.gif)

原理很容易理解，我们首先将 low 指针指向空节点， pro 节点指向 head 节点，

然后我们定义一个临时节点指向 pro 节点，

此时我们就记住了 pro 节点的位置，然后 pro = pro.next.这样我们三个指针指向三个不同的节点。

则我们将 temp 指针指向 low 节点，此时则完成了反转。

反转之后我们继续反转下一节点，则

low = temp 即可。然后重复执行上诉操作直至最后，这样则完成了反转链表。

我们下面看代码吧

我会对每个关键点进行注释，大家可以参考动图理解。



**题目代码**

Java Code:
```java
class Solution {
    public ListNode reverseList(ListNode head) {
         //特殊情况
        if (head == null || head.next == null) {
            return head;
        }
        //反转
        return reverse(head);
    }
    public ListNode reverse (ListNode head) {
        
        ListNode low = null;
        ListNode pro = head;
        while (pro != null) {
            //代表橙色指针
            ListNode temp = pro;
            //移动绿色指针
            pro = pro.next;
            //反转节点
            temp.next = low;
            //移动黄色指针
            low = temp;
        }     
        return low;
    }

}
```
JS Code:
```javascript
var reverseList = function(head) {
    if(!head || !head.next) {
        return head;
    }
    let low = null;
    let pro = head;
    while (pro) {
        let temp = pro;
        pro = pro.next;
        temp.next = low;
        low = temp;
    }
    return low;
};
```

C++代码

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
         //特殊情况
        if (head == nullptr || head->next == nullptr) {
            return head;
        }
        //反转
        return reverse(head);
    }
    ListNode * reverse (ListNode * head) {
        
        ListNode * low = nullptr;
        ListNode * pro = head;
        while (pro != nullptr) {
            //代表橙色指针
            ListNode * temp = pro;
            //移动绿色指针
            pro = pro->next;
            //反转节点
            temp->next = low;
            //移动黄色指针
            low = temp;
        }     
        return low;
    }
};
```

上面的迭代写法是不是搞懂啦，现在还有一种递归写法，不是特别容易理解，刚开始刷题的同学，可以只看迭代解法。



**题目代码**

Java Code:
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        //结束条件
        if (head == null || head.next == null) {
            return head;
        }
        //保存最后一个节点
        ListNode pro = reverseList(head.next);
        //将节点进行反转。我们可以这样理解 4.next.next = 4;
        //4.next = 5；
        //则 5.next = 4 则实现了反转
        head.next.next = head;
        //防止循环
        head.next = null;
        return pro;
    }
}

```

JS Code:
```javascript
var reverseList = function(head) {
    if (!head || !head.next) {
        return head;
    }
    let pro = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return pro;
};
```

C++代码:

```cpp
class Solution {
public:
    ListNode * reverseList(ListNode * head) {
        //结束条件
        if (head == nullptr || head->next == nullptr) {
            return head;
        }
        //保存最后一个节点
        ListNode * pro = reverseList(head->next);
        //将节点进行反转。我们可以这样理解 4->next->next = 4;
        //4->next = 5；
        //则 5->next = 4 则实现了反转
        head->next->next = head;
        //防止循环
        head->next = nullptr;
        return pro;
    }
};
```


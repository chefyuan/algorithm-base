> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [剑指 Offer 22. 链表中倒数第 k 个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

题目：

输入一个链表，输出该链表中倒数第 k 个节点。为了符合大多数人的习惯，本题从 1 开始计数，即链表的尾节点是倒数第 1 个节点。例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

题目分析：

自己思考一下：

我们遇到这个题目，可能会有什么答题思路呢？

你看我说的对不对，是不是会想到先遍历一遍链表知道 链表节点的个数，然后再计算出倒数第 n 个节点。

比如链表长度为 10，倒数第 3 个节点，不就是正数第 8 个节点呀，这种方法当然可以啦，是可以实现的，那么我们再思考一下有没有其他方法呢？哦，对，我们可以将链表元素保存到数组里面，然后直接就可以知道倒数第 k 个节点了。这个方法确实比刚才那个方法省时间了，但是所耗的空间更多了，那我们还有什么方法吗？

我们可以继续利用我们的双指针呀，但是我们应该怎么做呢？

双指针法：

首先一个指针移动 K-1 位（这里可以根据你的初始化指针决定），然后另一个指针开始启动，他俩移动速度一样，所以他俩始终相差 K-1 位，当第一个指针到达链表尾部时，第二个指针的指向则为倒数第 K 个节点。

![](https://img-blog.csdnimg.cn/img_convert/506c4d70f4c50c66994711c8506462a8.gif)

感觉这个方法既巧妙又简单，大家可以自己动手打一下，这个题目是经典题目。

**题目代码**

Java Code:

```java
class Solution {
    public ListNode getKthFromEnd (ListNode head, int k) {
        //特殊情况
        if (head == null) {
            return head;
        }
        //初始化两个指针
        ListNode pro = new ListNode(-1);
        ListNode after = new ListNode(-1);
        //定义指针指向
        pro = head;
        after = head;
        //先移动绿指针到指定位置
        for (int i = 0; i < k-1; i++) {
            pro = pro.next;
        }
        //两个指针同时移动
        while (pro.next != null) {
            pro = pro.next;
            after = after.next;
        }
        //返回倒数第k个节点
        return after;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    ListNode * getKthFromEnd(ListNode * head, int k) {
         //特殊情况
        if (head == nullptr) {
            return head;
        }
        //初始化两个指针
        ListNode * pro = new ListNode(-1);
        ListNode * after = new ListNode(-1);
        //定义指针指向
        pro = head;
        after = head;
        //先移动绿指针到指定位置
        for (int i = 0; i < k-1; i++) {
            pro = pro->next;
        }
        //两个指针同时移动
        while (pro->next != nullptr) {
            pro = pro->next;
            after = after->next;
        }
        //返回倒数第k个节点
        return after;
    }
};
```

JS Code:

```javascript
var getKthFromEnd = function (head, k) {
  //特殊情况
  if (!head) return head;
  //初始化两个指针, 定义指针指向
  let pro = head,
    after = head;
  //先移动绿指针到指定位置
  for (let i = 0; i < k - 1; i++) {
    pro = pro.next;
  }
  //两个指针同时移动
  while (pro.next) {
    pro = pro.next;
    after = after.next;
  }
  //返回倒数第k个节点
  return after;
};
```

Python Code:

```python
class Solution:
    def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
        # 特殊情况
        if head is None:
            return head
        # 初始化两个指针, 定义指针指向
        pro = head
        after = head
        # 先移动绿指针到指定位置
        for _ in range(k - 1):
            pro = pro.next
        # 两个指针同时移动
        while pro.next is not None:
            pro = pro.next
            after = after.next
        # 返回倒数第k个节点
        return after
```

Swift Code：

```swift
class Solution {
    func getKthFromEnd(_ head: ListNode?, _ k: Int) -> ListNode? {
        //特殊情况
        if head == nil {
            return head
        }
        //初始化两个指针
        var pro = head, after = head
        //先移动绿指针到指定位置
        for i in 0..<k-1 {
            pro = pro?.next
        }
        //两个指针同时移动
        while pro?.next != nil {
            pro = pro?.next
            after = after?.next
        }
        //返回倒数第k个节点
        return after
    }
}
```

Go Code:

```go
func getKthFromEnd(head *ListNode, k int) *ListNode {
    if head == nil { return head }
    pro, after := head, head
    //先移动绿指针到指定位置
    for i := 0; i < k - 1; i++ {
        pro = pro.Next
    }
    for pro.Next != nil {
        pro = pro.Next
        after = after.Next
    }
    return after
}
```

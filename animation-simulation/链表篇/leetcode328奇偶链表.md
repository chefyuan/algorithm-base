> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

### [328. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)

下面我们再来看一种双指针，我称之为交替领先双指针，起名鬼才哈哈。下面我们一起来看看吧。

#### 题目描述

> 给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。
>
> 请尝试使用原地算法完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes 为节点总数。

示例 1:

> 输入: 1->2->3->4->5->NULL
> 输出: 1->3->5->2->4->NULL

示例 2:

> 输入: 2->1->3->5->6->4->7->NULL
> 输出: 2->3->6->7->1->5->4->NULL

#### 题目解析

题目也很容易理解就是让我们将原来奇数位的结点放一起，偶数位的结点放一起。这里需要注意，题目和结点值无关，是奇数位和偶数位结点。

我们可以先将奇数位和在一起，再将偶数位和在一起，最后再将两个链表合并很简单，我们直接看动画模拟吧。

#### **动画模拟**

![](https://img-blog.csdnimg.cn/20210321120150255.gif)

#### 题目代码

Java Code:

```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
         if (head == null || head.next == null) {
             return head;
         }
         ListNode odd = head;
         ListNode even = head.next;
         ListNode evenHead = even;

         while (odd.next != null && even.next != null) {
             //将偶数位合在一起，奇数位合在一起
             odd.next = even.next;
             odd = odd.next;
             even.next = odd.next;
             even = even.next;
         }
         //链接
         odd.next = evenHead;
         return head;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
         if (head == nullptr || head->next == nullptr) {
             return head;
         }
         ListNode * odd = head;
         ListNode * even = head->next;
         ListNode * evenHead = even;

         while (odd->next != nullptr && even->next != nullptr) {
             //将偶数位合在一起，奇数位合在一起
             odd->next = even->next;
             odd = odd->next;
             even->next = odd->next;
             even = even->next;
         }
         //链接
         odd->next = evenHead;
         return head;
    }
};
```

JS Code:

```javascript
var oddEvenList = function (head) {
  if (!head || !head.next) return head;
  let odd = head,
    even = head.next,
    evenHead = even;
  while (odd.next && even.next) {
    //将偶数位合在一起，奇数位合在一起
    odd.next = even.next;
    odd = odd.next;
    even.next = odd.next;
    even = even.next;
  }
  //链接
  odd.next = evenHead;
  return head;
};
```

Python Code:

```python
class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        if head is None or head.next is None:
            return head
        odd = head
        even = head.next
        evenHead = even
        while odd.next is not None and even.next is not None:
            # 将偶数位合在一起，奇数位合在一起
            odd.next = even.next
            odd = odd.next
            even.next = odd.next
            even = even.next
        # 链接
        odd.next = evenHead
        return head
```

Swift Code：

```swift
class Solution {
    func oddEvenList(_ head: ListNode?) -> ListNode? {
        if head == nil || head?.next == nil {
            return head
        }
        var odd = head
        var even = head?.next
        var evenHead = even
        while odd?.next != nil && even?.next != nil {
            //将偶数位合在一起，奇数位合在一起
            odd?.next = even?.next
            odd = odd?.next
            even?.next = odd?.next
            even = even?.next
        }
        //链接
        odd?.next = evenHead
        return head
    }
}
```

Go Code:

```go
func oddEvenList(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }
    odd, even := head, head.Next
    evenHead := even
    for odd.Next != nil && even.Next != nil {
        odd.Next = even.Next
        odd = odd.Next
        even.Next = odd.Next
        even = even.Next
    }
    odd.Next = evenHead
    return head
}
```

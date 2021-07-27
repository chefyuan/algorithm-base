> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

### [328. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)

下面我们再来看一种双指针，我称之为交替�?�先双指针，起名鬼才哈哈。下面我�?一起来看看吧�?

#### 题目描述

> 给定一�?单链�?，把所有的奇数节点和偶数节点分�?排在一起。�?�注意，这里的�?�数节点和偶数节点指的是节点编号的�?�偶性，而不�?节点的值的奇偶性�?
>
> 请尝试使用原地算法完成。你的算法的空间复杂度应�? O(1)，时间�?�杂度应�? O(nodes)，nodes 为节点总数�?

示例 1:

> 输入: 1->2->3->4->5->NULL
> 输出: 1->3->5->2->4->NULL

示例 2:

> 输入: 2->1->3->5->6->4->7->NULL
> 输出: 2->3->6->7->1->5->4->NULL

#### 题目解析

题目也很容易理解就是让我�?将原来�?�数位的结点放一起，偶数位的结点放一起。这里需要注意，题目和结点值无关，�?奇数位和偶数位结点�?

我们�?以先将�?�数位和在一起，再将偶数位和在一起，最后再将两�?链表合并很简单，我们直接看动画模拟吧�?

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
             //将偶数位合在一起，奇数位合在一�?
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
             //将偶数位合在一起，奇数位合在一�?
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
    //将偶数位合在一起，奇数位合在一�?
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
            # 将偶数位合在一起，奇数位合在一�?
            odd.next = even.next
            odd = odd.next
            even.next = odd.next
            even = even.next
        # 链接
        odd.next = evenHead
        return head
```

Swift Code�?

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
            //将偶数位合在一起，奇数位合在一�?
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


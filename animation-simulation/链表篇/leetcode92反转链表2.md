> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

今天我们来说一下反转链表 2，其实这个和 1 的思路差不多，今天先说一个比较好理解的方法，完全按照反转链表 1 的方法来解决，大家看这个题目之前要先看一下[【动画模拟】leetcode 206 反转链表](https://github.com/chefyuan/algorithm-base/blob/main/animation-simulation/%E9%93%BE%E8%A1%A8%E7%AF%87/leetcode206%E5%8F%8D%E8%BD%AC%E9%93%BE%E8%A1%A8.md)。

下面我们先来看一下题目。

#### [92. 反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

给你单链表的头指针 `head` 和两个整数 `left` 和 `right` ，其中 `left <= right` 。请你反转从位置 `left` 到位置 `right` 的链表节点，返回 **反转后的链表** 。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

> 输入：head = [1,2,3,4,5], left = 2, right = 4
> 输出：[1,4,3,2,5]

**示例 2：**

> 输入：head = [5], left = 1, right = 1
> 输出：[5]

含义就是让我们反转部分链表。也就是上面蓝色的部分，那我们怎么借助 1 的方法来解决呢？

我们主要通过两部分来解决，先截取需要翻转的部分，然后再头尾交换即可。下面我们通过一个动画来看看具体步骤。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210327163804112.gif)

是不是很容易理解，下面我们来看代码吧。

**题目代码**

Java Code:

```java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        //虚拟头节点
        ListNode temp = new ListNode(-1);
        temp.next = head;
        ListNode pro = temp;
        //来到 left 节点前的一个节点
        int i = 0;
        for (; i < left-1; ++i) {
            pro = pro.next;
        }
        //保存 left 节点前的一个节点
        ListNode leftNode = pro;
        //来到 right 节点
        for (; i < right; ++i) {
            pro = pro.next;
        }
        //保存 right 节点后的一个节点
        ListNode rightNode = pro.next;
        //切断链表
        pro.next = null;//切断 right 后的部分
        ListNode newhead = leftNode.next;//保存 left 节点
        leftNode.next = null;//切断 left 前的部分
        //反转
        leftNode.next = reverse(newhead);
        //重新接头
        newhead.next = rightNode;
        return temp.next;

    }
    //和反转链表1代码一致
    public ListNode reverse (ListNode head) {
        ListNode low = null;
        ListNode pro = head;
        while (pro != null) {
            ListNode temp = pro;
            pro = pro.next;
            temp.next = low;
            low = temp;
        }
        return low;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        //虚拟头节点
        ListNode * temp = new ListNode(-1);
        temp->next = head;
        ListNode * pro = temp;
        //来到 left 节点前的一个节点
        int i = 0;
        for (; i < left-1; ++i) {
            pro = pro->next;
        }
        //保存 left 节点前的一个节点
        ListNode * leftNode = pro;
        //来到 right 节点
        for (; i < right; ++i) {
            pro = pro->next;
        }
        //保存 right 节点后的一个节点
        ListNode * rightNode = pro->next;
        //切断链表
        pro->next = nullptr;//切断 right 后的部分
        ListNode * newhead = leftNode->next;//保存 left 节点
        leftNode->next = nullptr;//切断 left 前的部分
        //反转
        leftNode->next = reverse(newhead);
        //重新接头
        newhead->next = rightNode;
        return temp->next;
    }
    //和反转链表1代码一致
    ListNode * reverse (ListNode * head) {
        ListNode * low = nullptr;
        ListNode * pro = head;
        while (pro != nullptr) {
            ListNode * temp = pro;
            pro = pro->next;
            temp->next = low;
            low = temp;
        }
        return low;
    }
};
```

JS Code:

```js
var reverseBetween = function (head, left, right) {
  //虚拟头节点
  let temp = new ListNode(-1);
  temp.next = head;
  let pro = temp;
  //来到 left 节点前的一个节点
  let i = 0;
  for (; i < left - 1; ++i) {
    pro = pro.next;
  }
  //保存 left 节点前的一个节点
  let leftNode = pro;
  //来到 right 节点
  for (; i < right; ++i) {
    pro = pro.next;
  }
  //保存 right 节点后的一个节点
  let rightNode = pro.next;
  //切断链表
  pro.next = null; //切断 right 后的部分
  let newhead = leftNode.next; //保存 left 节点
  leftNode.next = null; //切断 left 前的部分
  //反转
  leftNode.next = reverse(newhead);
  //重新接头
  newhead.next = rightNode;
  return temp.next;
};

//和反转链表1代码一致
var reverse = function (head) {
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

Python Code:

```python
class Solution:
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
        # 虚拟头节点
        temp = ListNode(-1)
        temp.next = head
        pro = temp
        # 来到 left 节点前的一个节点
        for _ in range(left - 1):
            pro = pro.next
        # 保存 left 节点前的第一个节点
        leftNode = pro
        for _ in range(right - left + 1):
            pro = pro.next
        # 保存 right 节点后的节点
        rightNode = pro.next
        # 切断链表
        pro.next = None  # 切断 right 后的部分
        newhead = leftNode.next  # 保存 left 节点
        leftNode.next = None  # 切断 left 前的部分
        # 反转
        leftNode.next = self.reverse(newhead)
        # 重新接头
        newhead.next = rightNode
        return temp.next

    # 和反转链表1代码一致
    def reverse(self, head):
        low = None
        pro = head
        while pro is not None:
            temp = pro
            pro = pro.next
            temp.next = low
            low = temp
        return low
```

Swift Code：

```swift
class Solution {
    func reverseBetween(_ head: ListNode?, _ left: Int, _ right: Int) -> ListNode? {
        // 虚拟头结点
        var temp = ListNode(-1)
        temp.next = head
        var pro:ListNode? = temp
        // 来到 left 节点前的一个节点
        var i = 0
        for n in i..<left - 1 {
            pro = pro?.next
            i += 1
        }
        // 保存 left 节点前的一个节点
        var leftNode = pro
        // 来到 right 节点
        for n in i..<right {
            pro = pro?.next
        }
        // 保存 right 节点后的一个节点
        var rightNode:ListNode? = pro?.next
        // 切断链表
        pro?.next = nil // 切断 right 后的部分
        var newHead:ListNode? = leftNode?.next // 保存 left 节点
        leftNode?.next = nil // 切断 left 前的部分
        // 反转
        leftNode?.next = reverse(newHead)
        // 重新接头
        newHead?.next = rightNode
        return temp.next
    }
    // 和反转链表1代码一致
    func reverse(_ head: ListNode?) -> ListNode? {
        var low:ListNode?
        var pro = head
        while pro != nil {
            var temp = pro
            pro = pro?.next
            temp?.next = low
            low = temp
        }
        return low
    }
}
```

GoCode:

```go
func reverseBetween(head *ListNode, left int, right int) *ListNode {
    root := &ListNode{
        Next: head,
    }
    temp := root
    i := 0
    // left的前一个节点
    for ; i < left - 1; i++ {
        temp = temp.Next
    }
    leftNode := temp
    // right的后一个节点
    for ; i < right; i++ {
        temp = temp.Next
    }
    rightNode := temp.Next
    // 切断链表
    temp.Next = nil
    newhead := leftNode.Next
    leftNode.Next = nil

    // 反转后将3段链表接上。
    leftNode.Next = reverse(newhead)
    newhead.Next = rightNode
    return root.Next
}

func reverse(head *ListNode) *ListNode {
    var pre *ListNode
    cur := head
    for cur != nil {
        temp := cur
        cur = cur.Next
        temp.Next = pre
        pre = temp
    }
    return pre
}
```

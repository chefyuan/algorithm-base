> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

今天我们来�?�一下反�?链表 2，其实这�?�? 1 的思路�?不�?�，今天先�?�一�?比较好理解的方法，完全按照反�?链表 1 的方法来解决，大家看这个题目之前要先看一下[【动画模拟】leetcode 206 反转链表](https://github.com/chefyuan/algorithm-base/blob/main/animation-simulation/%E9%93%BE%E8%A1%A8%E7%AF%87/leetcode206%E5%8F%8D%E8%BD%AC%E9%93%BE%E8%A1%A8.md)�?

下面我们先来看一下�?�目�?

#### [92. 反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

给你单链表的头指�? `head` 和两�?整数 `left` �? `right` ，其�? `left <= right` 。�?�你反转从位�? `left` 到位�? `right` 的链表节点，返回 **反转后的链表** �?

**示例 1�?**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

> 输入：head = [1,2,3,4,5], left = 2, right = 4
> 输出：[1,4,3,2,5]

**示例 2�?**

> 输入：head = [5], left = 1, right = 1
> 输出：[5]

�?义就�?让我�?反转部分链表。也就是上面蓝色的部分，那我�?怎么借助 1 的方法来解决�?�?

我们主�?�通过两部分来解决，先�?取需要翻�?的部分，然后再头尾交换即�?。下面我�?通过一�?动画来看看具体�?��?��?

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210327163804112.gif)

�?不是很�?�易理解，下面我�?来看代码吧�?

**题目代码**

Java Code:

```java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        //虚拟头节�?
        ListNode temp = new ListNode(-1);
        temp.next = head;
        ListNode pro = temp;
        //来到 left 节点前的一�?节点
        int i = 0;
        for (; i < left-1; ++i) {
            pro = pro.next;
        }
        //保存 left 节点前的一�?节点
        ListNode leftNode = pro;
        //来到 right 节点
        for (; i < right; ++i) {
            pro = pro.next;
        }
        //保存 right 节点后的一�?节点
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
    //和反�?链表1代码一�?
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
        //虚拟头节�?
        ListNode * temp = new ListNode(-1);
        temp->next = head;
        ListNode * pro = temp;
        //来到 left 节点前的一�?节点
        int i = 0;
        for (; i < left-1; ++i) {
            pro = pro->next;
        }
        //保存 left 节点前的一�?节点
        ListNode * leftNode = pro;
        //来到 right 节点
        for (; i < right; ++i) {
            pro = pro->next;
        }
        //保存 right 节点后的一�?节点
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
    //和反�?链表1代码一�?
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
  //虚拟头节�?
  let temp = new ListNode(-1);
  temp.next = head;
  let pro = temp;
  //来到 left 节点前的一�?节点
  let i = 0;
  for (; i < left - 1; ++i) {
    pro = pro.next;
  }
  //保存 left 节点前的一�?节点
  let leftNode = pro;
  //来到 right 节点
  for (; i < right; ++i) {
    pro = pro.next;
  }
  //保存 right 节点后的一�?节点
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

//和反�?链表1代码一�?
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
        # 虚拟头节�?
        temp = ListNode(-1)
        temp.next = head
        pro = temp
        # 来到 left 节点前的一�?节点
        for _ in range(left - 1):
            pro = pro.next
        # 保存 left 节点前的�?一�?节点
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

    # 和反�?链表1代码一�?
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

Swift Code�?

```swift
class Solution {
    func reverseBetween(_ head: ListNode?, _ left: Int, _ right: Int) -> ListNode? {
        // 虚拟头结�?
        var temp = ListNode(-1)
        temp.next = head
        var pro:ListNode? = temp
        // 来到 left 节点前的一�?节点
        var i = 0
        for n in i..<left - 1 {
            pro = pro?.next
            i += 1
        }
        // 保存 left 节点前的一�?节点
        var leftNode = pro
        // 来到 right 节点
        for n in i..<right {
            pro = pro?.next
        }
        // 保存 right 节点后的一�?节点
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
    // 和反�?链表1代码一�?
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
    // left的前一�?节点
    for ; i < left - 1; i++ {
        temp = temp.Next
    }
    leftNode := temp
    // right的后一�?节点
    for ; i < right; i++ {
        temp = temp.Next
    }
    rightNode := temp.Next
    // 切断链表
    temp.Next = nil
    newhead := leftNode.Next
    leftNode.Next = nil

    // 反转后将3段链表接上�?
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


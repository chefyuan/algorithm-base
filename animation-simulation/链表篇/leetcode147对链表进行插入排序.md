> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

有的老哥说链表的排序搞不明白，让我写一下，一不小心给忘记了，今天咱们就安排上。没有学过数据结构的同学可以先看下这个文章：

[【绘图解析】链表详解](https://github.com/chefyuan/algorithm-base/blob/main/animation-simulation/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E5%92%8C%E7%AE%97%E6%B3%95/%E5%85%B3%E4%BA%8E%E9%93%BE%E8%A1%A8%E7%9A%84%E9%82%A3%E4%BA%9B%E4%BA%8B.md)

另外大家如果忘记了[【动画模拟】插入排序](https://github.com/chefyuan/algorithm-base/blob/main/animation-simulation/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E5%92%8C%E7%AE%97%E6%B3%95/%E7%9B%B4%E6%8E%A5%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F.md)和[【动画模拟】归并排序](https://github.com/chefyuan/algorithm-base/blob/main/animation-simulation/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E5%92%8C%E7%AE%97%E6%B3%95/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F.md)思想的话，可以先复习一下，不然这两道题目会看得云里雾里。

#### [147. 对链表进行插入排序](https://leetcode-cn.com/problems/insertion-sort-list/)

**示例 1：**

> 输入: 4->2->1->3
> 输出: 1->2->3->4

**示例 2：**

> 输入: -1->5->3->4->0
> 输出: -1->0->3->4->5

下面咱们先来看个动画回忆一下插入排序的具体执行步骤，然后我们再来说下面的题目。

![直接插入排序](https://cdn.jsdelivr.net/gh/tan45du/test1@master/20210122/直接插入排序.2marc4epuzy0.gif)

我们的指针在数组时，可以随意的前后移动，将指针指向值和新元素的值比较后，将新元素插入到合适的位置。

我们知道链表查询元素的时间复杂度为 O(n)，我们只能够通过遍历链表查询元素。

那么我们怎么才能将新元素放到合适的位置呢？见下图。

![](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/微信截图_20210325113449.75knzw7zmyg0.png)

此时我们不能通过移动绿色指针来寻找 5 的合适位置，那么我们应该怎么做呢？见下图。

![](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/微信截图_20210325131349.14mi2ap89uxs.png)

当我们发现绿色指针的值大于新元素时（7 > 5），我们则可以定义一个新指针，让其从哑节点开始遍历，直到找到新元素（5）的位置，（4 和 7 之间），然后再将新元素插入即可。

我们是通过下面这行代码来找到插入位置的, temphead 则代表我们的紫色指针。

```java
 while (temphead.next.val <= pre.val) {
      temphead = temphead.next;
 }
```

下面我们再来看动画模拟具体过程。

**注：为了更好的表达算法思想，让过程更流畅，特省略了指针的移动细节，直接插入到合适位置，后面会详细说明插入操作的具体步骤。**

![](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/链表的插入排序.4hnc4shp5le0.gif)

我们通过上面的动画知道了大致过程，那么我们的是如何将新元素插入到指定位置的呢？

见下图。

![插入排序](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/微信截图_20210325132359.1hc2axzks3k0.png)

我们想要将 3 插入到 2 和 4 的中间，此时我们三个指针分别指向 2，4，3。

我们共分 4 步，来完成这个操作，见下图。

![](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/44444444.29mvcvs4yrms.png)

我们来把上图中的最后结果来捋一下看看最后结果是不是完成了插入操作。

![](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/微信截图_20210325134022.w5nnr1spyps.png)

这样我们就完成了链表的插入排序。下面我们来看下题目代码吧。

**题目代码**

Java Code:

```java
class Solution {
    public ListNode insertionSortList(ListNode head) {
        if (head == null && head.next == null) {
            return head;
        }
        //哑节点
        ListNode dummyNode = new ListNode(-1);
        dummyNode.next = head;
        //pre负责指向新元素，last 负责指向新元素的前一元素
        //判断是否需要执行插入操作
        ListNode pre = head.next;
        ListNode last = head;
        while (pre != null) {
            //不需要插入到合适位置，则继续往下移动
            if (last.val <= pre.val) {
                pre = pre.next;
                last = last.next;
                continue;
            }
            //开始出发，查找新元素的合适位置
            ListNode temphead = dummyNode;
            while (temphead.next.val <= pre.val) {
                temphead = temphead.next;
            }
            //此时我们已经找到了合适位置，我们需要进行插入，大家可以画一画
            last.next = pre.next;
            pre.next = temphead.next;
            temphead.next = pre;
            //继续往下移动
            pre = last.next;
        }
        return dummyNode.next;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    ListNode* insertionSortList(ListNode* head) {
        if (head == nullptr && head->next == nullptr) {
            return head;
        }
        //哑节点
        ListNode * dummyNode = new ListNode(-1);
        dummyNode->next = head;
        //pre负责指向新元素，last 负责指向新元素的前一元素
        //判断是否需要执行插入操作
        ListNode * pre = head->next;
        ListNode * last = head;
        while (pre != nullptr) {
            //不需要插入到合适位置，则继续往下移动
            if (last->val <= pre->val) {
                pre = pre->next;
                last = last->next;
                continue;
            }
            //开始出发，查找新元素的合适位置
            ListNode * temphead = dummyNode;
            while (temphead->next->val <= pre->val) {
                temphead = temphead->next;
            }
            //此时我们已经找到了合适位置，我们需要进行插入，大家可以画一画
            last->next = pre->next;
            pre->next = temphead->next;
            temphead->next = pre;
            //继续往下移动
            pre = last->next;
        }
        return dummyNode->next;
    }
};
```

JS Code:

```javascript
var insertionSortList = function (head) {
  if (head === null || head.next === null) return head;
  //哑节点
  let dummyNode = new ListNode(-1, head);
  let pre = head.next;
  //pre负责指向新元素，last 负责指向新元素的前一元素
  //判断是否需要执行插入操作
  let last = head;
  while (pre) {
    //不需要插入到合适位置，则继续往下移动
    if (last.val <= pre.val) {
      last = last.next;
      pre = pre.next;
      continue;
    }
    //开始出发，查找新元素的合适位置
    let tempHead = dummyNode;
    while (tempHead.next.val <= pre.val) {
      tempHead = tempHead.next;
    }
    //此时我们已经找到了合适位置，我们需要进行插入，大家可以画一画
    last.next = pre.next;
    pre.next = tempHead.next;
    tempHead.next = pre;
    //继续往下移动
    pre = last.next;
  }
  return dummyNode.next;
};
```

Python Code:

```python
class Solution:
    def insertionSortList(self, head: ListNode) -> ListNode:
        if head is None or head.next is None:
            return head
        # 哑节点
        dummyNode = ListNode(-1, head)
        # pre负责指向新元素，last 负责指向新元素的前一元素
        # 判断是否需要执行插入操作
        pre = head.next
        last = head
        while pre is not None:
            # 不需要插入到合适位置，则继续往下移动
            if last.val <= pre.val:
                pre = pre.next
                last = last.next
                continue
            # 开始出发，查找新元素的合适位置
            temphead = dummyNode
            while temphead.next.val <= pre.val:
                temphead = temphead.next
            # 此时我们已经找到了合适位置，我们需要进行插入，大家可以画一画
            last.next = pre.next
            pre.next = temphead.next
            temphead.next = pre
            # 继续往下移动
            pre = last.next
        return dummyNode.next
```

Swift Code：

```swift
class Solution {
    func insertionSortList(_ head: ListNode?) -> ListNode? {
        if head == nil && head?.next == nil {
            return head
        }
        //哑节点
        var dummyNode = ListNode(-1)
        dummyNode.next = head
        //pre负责指向新元素，last 负责指向新元素的前一元素
        //判断是否需要执行插入操作
        var pre = head?.next
        var last = head
        while pre != nil {
            //不需要插入到合适位置，则继续往下移动
            if last!.val <= pre!.val {
                pre = pre?.next
                last = last?.next
                continue
            }
            //开始出发，查找新元素的合适位置
            var temphead = dummyNode
            while temphead.next!.val <= pre!.val {
                temphead = temphead.next!
            }
            //此时我们已经找到了合适位置，我们需要进行插入，大家可以画一画
            last?.next = pre?.next
            pre?.next = temphead.next
            temphead.next = pre
            //继续往下移动
            pre = last?.next
        }
        return dummyNode.next
    }
}
```

Go Code:

```go
func insertionSortList(head *ListNode) *ListNode {
    if head == nil || head.Next == nil { return head }
    root := &ListNode{
        Next: head,
    }
    cur, nxt := head, head.Next
    for nxt != nil {
        // 有序的不需要换位置
        if cur.Val <= nxt.Val {
            cur = cur.Next
            nxt = nxt.Next
            continue
        }
        temp := root
        for temp.Next.Val <= nxt.Val {
            temp = temp.Next
        }
        // 此时找到合适的位置
        cur.Next = nxt.Next
        nxt.Next = temp.Next
        temp.Next = nxt
        // 继续向下
        nxt = cur.Next
    }
    return root.Next
}
```

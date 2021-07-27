> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

#### [剑指 Offer 52. 两个链表的第一个公共节点](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/) & [160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

### 前言

今天给大家带来一个不是那么难的题目，这个题目的解答方法很多，只要能 AC 的就是好方法，虽然题目不是特别难但是也是剑指 offer 上的经典题目所以大家要记得打卡呀。

然后今天我们的链表板块就算结束啦。周末的时候我会对链表的题目做一个总结，俗话说温故而知新嘛。好啦废话不多说，我们一起来看一下今天的题目吧！

题目描述：

输入两个链表，找出它们的第一个公共节点。如下图，返回黄色结点即可。

![image-20201029215837844](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/image-20201029215837844.7ezoerpghyk0.png)

题目表达是不是也很简单，这个题目我的方法一共有两个，一种就是用 HashSet 进行存储，一种就是利用双指针，大家有更好的可以在下面讨论呀。

### HashSet

这个方法是比较简单的，主要思路就是，先遍历一个链表将链表的所有值都存到 Hashset 中，然后再遍历另一个链表，如果发现某个结点在 Hashset 中已经存在那我们直接返回该节点即可，代码也很简单。

**题目代码**

Java Code:

```java
public class Solution {
    public ListNode getIntersectionNode (ListNode headA, ListNode headB) {
        ListNode tempa = headA;
        ListNode tempb = headB;
        //定义Hashset
        HashSet<ListNode> arr = new HashSet<ListNode>();
        //遍历链表A，将所有值都存到arr中
        while (tempa != null) {
            arr.add(tempa);
            tempa = tempa.next;
        }
        //遍历列表B，如果发现某个结点已在arr中则直接返回该节点
        while (tempb != null) {
            if (arr.contains(tempb)) {
                return tempb;
            }
            tempb = tempb.next;
        }
        //若上方没有返回，此刻tempb为null
        return tempb;

    }
}
```

C++ Code:

```cpp
class Solution {
public:
    ListNode * getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode * tempa = headA;
        ListNode * tempb = headB;
        //定义Hashset
        set <ListNode *> arr;
        //遍历链表A，将所有值都存到arr中
        while (tempa != nullptr) {
            arr.insert(tempa);
            tempa = tempa->next;
        }
        //遍历列表B，如果发现某个结点已在arr中则直接返回该节点
        while (tempb != nullptr) {
            if (arr.find(tempb) != arr.end()) {
                return tempb;
            }
            tempb = tempb->next;
        }
        //若上方没有返回，此刻tempb为null
        return tempb;
    }
};
```

JS Code:

```js
var getIntersectionNode = function (headA, headB) {
  let tempa = headA;
  let tempb = headB;
  //定义Hashset
  let arr = new Set();
  //遍历链表A，将所有值都存到arr中
  while (tempa) {
    arr.add(tempa);
    tempa = tempa.next;
  }
  //遍历列表B，如果发现某个结点已在arr中则直接返回该节点
  while (tempb) {
    if (arr.has(tempb)) {
      return tempb;
    }
    tempb = tempb.next;
  }
  //若上方没有返回，此刻tempb为null
  return tempb;
};
```

Python Code:

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        tempa = headA
        tempb = headB
        # 定义Hashset
        arr = set()
        # 遍历链表A，将所有值都存到arr中
        while tempa is not None:
            arr.add(tempa)
            tempa = tempa.next
        # 遍历列表B，如果发现某个结点已在arr中则直接返回该节点
        while tempb is not None:
            if tempb in arr:
                return tempb
            tempb = tempb.next
        # 若上方没有返回，此刻tempb为null
        return tempb
```

Swift Code：

```swift
class Solution {
    func getIntersectionNode(_ headA: ListNode?, _ headB: ListNode?) -> ListNode? {
        var tempa = headA
        var tempb = headB
        var arr:Set<ListNode> = []
        //遍历链表A，将所有值都存到arr中
        while tempa != nil {
            arr.insert(tempa!)
            tempa = tempa?.next
        }
        //遍历列表B，如果发现某个结点已在arr中则直接返回该节点
        while tempb != nil {
            if arr.contains(tempb!) {
                return tempb
            }
            tempb = tempb?.next
        }
        //若上方没有返回，此刻tempb为null
        return tempb
    }
}
extension ListNode: Hashable, Equatable {
    public func hash(into hasher: inout Hasher) {
        hasher.combine(val)
        hasher.combine(ObjectIdentifier(self))
    }
    public static func ==(lhs: ListNode, rhs: ListNode) -> Bool {
        return lhs === rhs
    }
}
```

下面这个方法比较巧妙，不是特别容易想到，大家可以自己实现一下，这个方法也是利用我们的双指针思想。

下面我们直接看动图吧，特别直观，一下就可以搞懂。

![第一次相交的点](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/第一次相交的点.5nbxf5t3hgk0.gif)

是不是一下就懂了呀，我们利用双指针，当某一指针遍历完链表之后，然后掉头去另一个链表的头部，继续遍历。因为速度相同所以他们第二次遍历的时候肯定会相遇，是不是很浪漫啊！

**题目代码**

Java Code:

```java
public class Solution {
    public ListNode getIntersectionNode (ListNode headA, ListNode headB) {
        //定义两个节点
        ListNode tempa = headA;
        ListNode tempb = headB;
        //循环
        while (tempa != tempb) {
          //如果不为空就指针下移，为空就跳到另一链表的头部
           tempa = tempa != null ? tempa.next: headB;
           tempb = tempb != null ? tempb.next: headA;
        }
        return tempa;//返回tempb也行
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    ListNode * getIntersectionNode(ListNode *headA, ListNode *headB) {
        //定义两个节点
        ListNode * tempa = headA;
        ListNode * tempb = headB;
        //循环
        while (tempa != tempb) {
           //如果不为空就指针下移，为空就跳到另一链表的头部
           tempa = tempa != nullptr ? tempa->next: headB;
           tempb = tempb != nullptr ? tempb->next: headA;
        }
        return tempa;//返回tempb也行
    }
};
```

JS Code:

```js
var getIntersectionNode = function (headA, headB) {
  //定义两个节点
  let tempa = headA;
  let tempb = headB;
  //循环
  while (tempa != tempb) {
    //如果不为空就指针下移，为空就跳到另一链表的头部
    tempa = tempa != null ? tempa.next : headB;
    tempb = tempb != null ? tempb.next : headA;
  }
  return tempa; //返回tempb也行
};
```

Python Code:

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        # 定义两个节点
        tempa = headA
        tempb = headB
        # 循环
        while tempa is not tempb:
            # 如果不为空就指针下移，为空就跳到另一链表的头部
            tempa = tempa.next if tempa is not None else headB
            tempb = tempb.next if tempb is not None else headA
        return tempa  # 返回tempb也行
```

Swift Code：

```swift
class Solution {
    func getIntersectionNode(_ headA: ListNode?, _ headB: ListNode?) -> ListNode? {
        //定义两个节点
        var tempa = headA
        var tempb = headB
        //循环
        while tempa != tempb {
            // 如果不为空就指针下移，为空就跳到另一链表的头部
            tempa = tempa != nil ? tempa?.next : headB
            tempb = tempb != nil ? tempb?.next : headA
        }
        return tempa //返回tempb也行
    }
}
```

Go Code:

```go
func getIntersectionNode(headA, headB *ListNode) *ListNode {
    tempA, tempB := headA, headB
    for tempA != tempB {
        // 如果不为空就指针下移，为空就跳到另一链表的头部
        if tempA == nil {
            tempA = headB
        } else {
            tempA = tempA.Next
        }
        if tempB == nil {
            tempB = headA
        } else {
            tempB = tempB.Next
        }
    }
    return tempA
}
```

好啦，链表的题目就结束啦，希望大家能有所收获，下周就要更新新的题型啦，继续坚持，肯定会有收获的。

<br/>

> 贡献者[@jaredliw](https://github.com/jaredliw)注：
>
> 在这里带大家来看看一些其他的解题方法，虽然没有双指针有效，但还是值得一试。
>
> 1. 两个链表各遍历一次，找出长度。根据长度差 k，让较长的那个链表先走 k 步。之后再两个指针一起走，由于起点一样，两个指针必将一起到达公共节点。
> 2. 将其中一条链表的头和尾相连，公共节点就是环的入口，直接套用之前学过的算法就可以啦。（这解法看得我拍腿叫好）

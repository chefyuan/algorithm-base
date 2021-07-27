> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [142. �?形链�? II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

题目描述�?

今天给大家介绍比较有特点的�?�目，也�?一�?特别经典的�?�目，判�?链表�?有没有环，并返回�?的入口�?

我们�?以先做一下这�?题目，就�?如何判断链表�?�?否有�?�?？下图则为链表存在环的情况�?

![image-20201027175552961](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/image-20201027175552961.63sz69rbes00.png)

判断链表�?否有�?�?很简单的一�?�?题，我们�?需利用之前的快慢指针即�?，大家想一下，指针�?要进入环内就�?能在�?�?�?�?，那么我�?�?以利用快慢指针，虽然慢指针的速度小于�?指针但是，总会进入�?�?，当两个指针都�?�于�?�?时，因为移动速度不同，两�?指针必会相遇�?

我们�?以这样假设，两个孩子在操场顺时针跑�?�，一�?跑的�?，一�?跑的�?，跑的快的那�?孩子总会追上跑的慢的孩子�?

代码请参考[【动画模拟】leetcode 141 �?形链表](https://github.com/chefyuan/algorithm-base/blob/main/animation-simulation/%E9%93%BE%E8%A1%A8%E7%AF%87/leetcode141%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8.md)�?

判断链表�?不是�?有环很简单，但是我们想找到环的入口可能就没有那么容易了。（入口则为下图绿色节点�?

然后我们返回的则为绿色节点的索引，则返回 2�?

![image-20201027180921770](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/image-20201027180921770.21fh8pt3cuv4.png)

### HashSet

我们�?以利�? HashSet 来做，之前的文章说过 HashSet �?一�?不允许有重�?�元素的集合。所以我�?通过 HashSet 来保存链表节点，对链表进行遍历，如果链表不存在环则每�?节点都会�?存入�?�?，但�?当链表中存在�?时，则会发重复存储链表节点的情况，所以当我们发现 HashSet �?�?有某节点时�?�明该节点为�?的入口，返回即可�?

下图�?，存储顺序为 0�?1�?2�?3�?4�?5�?6�?**2 **因为 2 已经存在，则返回�?

![image-20201027182649669](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/image-20201027182649669.2g8gq4ik6xs0.png)

Java Code:

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
         if (head == null) {
             return head;
         }
         if (head.next == null) {
             return head.next;
         }
         //创建新的HashSet，用于保存节�?
         HashSet<ListNode> hash = new HashSet<ListNode>();
         //遍历链表
         while (head != null) {
             //判断哈希表中�?否含有某节点，没有则保存，含有则返回该节�?
             if (hash.contains(head)) {
                 return head;
             }
             //不含有，则进行保存，并移动指�?
             hash.add(head);
             head = head.next;
         }
        return head;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if (head == nullptr) return head;
        if (head->next == nullptr) return head->next;
        //创建新的HashSet，用于保存节�?
        set<ListNode *> hash;
        //遍历链表
        while (head != nullptr) {
            //判断哈希表中�?否含有某节点，没有则保存，含有则返回该节�?
            if (hash.count(head)) {
                return head;
            }
            //不含有，则进行保存，并移动指�?
            hash.insert(head);
            head = head->next;
        }
        return head;
    }
};
```

JS Code:

```javascript
var detectCycle = function (head) {
  if (head === null) return head;
  if (head.next === null) return head.next;
  //创建新的HashSet，用于保存节�?
  let hash = new Set();
  //遍历链表
  while (head !== null) {
    //判断哈希表中�?否含有某节点，没有则保存，含有则返回该节�?
    if (hash.has(head)) {
      return head;
    }
    //不含有，则进行保存，并移动指�?
    hash.add(head);
    head = head.next;
  }
  return head;
};
```

Python Code:

```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        if head is None:
            return head
        if head.next is None:
            return head.next
        # 创建新的HashSet，用于保存节�?
        hash = set()
        while head is not None:
            # 判断哈希表中�?否含有某节点，没有则保存，含有则返回该节�?
            if head in hash:
                return head
            # 不含有，则进行保存，并移动指�?
            hash.add(head)
            head = head.next
        return head
```

### �?慢指�?

这个方法�?比较巧�?�的方法，但�?不�?�易想到，也不太容易理解，利用快慢指针判�?�?否有�?很�?�易，但�?判断�?的入口就没有那么容易，之前�?�过�?慢指针肯定会在环内相遇，见下图�?

![image-20201027184755943](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/image-20201027184755943.3edot8s2xi60.png)

上图黄色节点为快慢指针相遇的节点，�?�时

�?指针走的距�?�：**a+(b+c)n+b**，n 代表圈数�?

很�?�易理解 b+c 为环的长度，a 为直线距离，b 为绕�? n 圈之后又走了一段距离才相遇，所以相遇时走的总路程为 a+(b+c)n+b，合并同类项�? a+(n+1)b+nc�?

慢指针走的距离：**a+(b+c)m+b**，m 代表圈数�?

然后我们设快指针得速度�?慢指针的 2 倍，�?义为相同时间内，�?指针走过的距离是慢指针的 2 倍�?

**a+(n+1)b+nc=2[a+(m+1)b+mc]**整理�?**a+b=(n-2m)(b+c)�?**那么我们�?以从这个等式上面发现什么呢�?

**b+c**为一圈的长度。也就是�? a+b 等于 n-2m �?�?的长度。为了便于理解我�?看一种特殊情况，�? n-2m 等于 1，那�? a+b=b+c 整理得，a=c。�?�时我们�?需重新释放两个指针，一�?�? head 释放，一�?从相遇点释放，速度相同，因�? a=c 所以他俩必会在�?入口处相遇，则求得入口节点索引�?

算法流程�?

1.设置�?慢指针，�?指针速度为慢指针�? 2 倍�?

2.找出相遇点�?

3.�? head 处和相遇点同时释放相同速度且速度�? 1 的指针，两指针必会在�?入口处相遇�?

![�?形链�?2](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/�?形链�?2.elwu1pw2lw0.gif)

**题目代码**

Java Code:

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
       //�?慢指�?
        ListNode fast = head;
        ListNode slow = head;
        //设置�?�?条件
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            //相遇
            if (fast == slow) {
                //设置一�?新的指针，从头节点出发，慢指针速度�?1，所以可以使用慢指针从相遇点出发
                ListNode newptr = head;
                while (newptr != slow) {
                    slow = slow.next;
                    newptr = newptr.next;
                }
                //在环入口相遇
                return slow;
            }
        }
        return null;
    }
}
```

C++ Code:

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        //�?慢指�?
        ListNode * fast = head;
        ListNode * slow = head;
        //设置�?�?条件
        while (fast != nullptr && fast->next != nullptr) {
            fast = fast->next->next;
            slow = slow->next;
            //相遇
            if (fast == slow) {
                //设置一�?新的指针，从头节点出发，慢指针速度�?1，所以可以使用慢指针从相遇点出发
                ListNode * newnode = head;
                while (newnode != slow) {
                    slow = slow->next;
                    newnode = newnode->next;
                }
                //在环入口相遇
                return slow;
            }
        }
        return nullptr;
    }
};
```

JS Code:

```js
var detectCycle = function (head) {
  //�?慢指�?
  let fast = head;
  let slow = head;
  //设置�?�?条件
  while (fast && fast.next) {
    fast = fast.next.next;
    slow = slow.next;
    //相遇
    if (fast == slow) {
      let newptr = head;
      //设置一�?新的指针，从头节点出发，慢指针速度�?1，所以可以使用慢指针从相遇点出发
      while (newptr != slow) {
        slow = slow.next;
        newptr = newptr.next;
      }
      //在环入口相遇
      return slow;
    }
  }
  return null;
};
```

Python Code:

```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        # �?慢指�?
        fast = head
        slow = head
        # 设置�?�?条件
        while fast is not None and fast.next is not None:
            fast = fast.next.next
            slow = slow.next
            # 相遇
            if fast is slow:
                # 设置一�?新的指针，从头节点出发，慢指针速度�?1，所以可以使用慢指针从相遇点出发
                newptr = head
                while newptr is not slow:
                    slow = slow.next
                    newptr = newptr.next
                # 在环入口相遇
                return slow
```

Swift Code�?

```swift
class Solution {
    func detectCycle(_ head: ListNode?) -> ListNode? {
        // �?慢指�?
        var fast = head, slow = head
        while fast != nil && fast?.next != nil {
            fast = fast?.next?.next
            slow = slow?.next
            // 相遇
            if fast === slow {
                // 设置一�?新的指针，从头节点出发，慢指针速度�?1，所以可以使用慢指针从相遇点出发
                // 此�?�也�?以不创新结点，直接将 fast = head
                var newNode = head
                while newNode !== slow {
                    slow = slow?.next
                    newNode = newNode?.next
                }
                return slow
            }
        }
        return nil
    }
}
```

Go Code:

```go
func detectCycle(head *ListNode) *ListNode {
    if head == nil { return nil }
    s, f := head, head
    for f != nil && f.Next != nil {
        s = s.Next
        f = f.Next.Next
        // �?慢指针相�?
        if f == s {
            // �?指针从头开始一步一步走，也�?以用一�?新的指针
            f = head
            for f != s {
                f = f.Next
                s = s.Next
            }
            return f
        }
    }
    return nil
}
```


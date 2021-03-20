#### 剑指 Offer 52. 两个链表的第一个公共节点

### 前言

今天给大家带来一个不是那么难的题目，这个题目的解答方法很多，只要能AC的就是好方法，虽然题目不是特别难但是也是剑指offer上的经典题目所以大家要记得打卡呀。

然后今天我们的链表板块就算结束啦。周末的时候我会对链表的题目做一个总结，俗话说温故而知新嘛。好啦废话不多说，我们一起来看一下今天的题目吧

题目描述：

输入两个链表，找出它们的第一个公共节点。如下图，返回黄色结点即可。



![image-20201029215837844](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/image-20201029215837844.7ezoerpghyk0.png)



题目表达是不是也很简单，这个题目我的方法一共有两个，一种就是用HashSet进行存储，一种就是利用双指针，大家有更好的可以在下面讨论呀。

### HashSet

这个方法是比较简单的，主要思路就是，先遍历一个链表将链表的所有值都存到哈希表中，然后再遍历另一个链表，如果发现某个结点在哈希表中已经存在那我们直接返回该节点即可，代码也很简单。

```java
public class Solution {
    public ListNode getIntersectionNode (ListNode headA, ListNode headB) {
        ListNode tempa = headA;
        ListNode tempb = headB;
        //定义hash表
        HashSet<ListNode> arr = new HashSet<ListNode>();
        while (tempa != null) {
            arr.add(tempa);
            tempa = tempa.next;
        }
        while (tempb != null) {
            if (arr.contains(tempb)) {
                return tempb;
            }
            tempb = tempb.next;
        }
        return tempb;
        
    }
}
```

下面这个方法比较巧妙，不是特别容易想到，大家可以自己实现一下，这个方法也是利用我们的双指针思想。

下面我们直接看动图吧，特别直观，一下就可以搞懂。

![第一次相交的点](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/第一次相交的点.5nbxf5t3hgk0.gif)

是不是一下就懂了呀，我们利用双指针，当某一指针遍历完链表之后，然后掉头去另一个链表的头部，继续遍历。因为速度相同所以他们第二次遍历的时候肯定会相遇，是不是很浪漫啊！

```java
public class Solution {
    public ListNode getIntersectionNode (ListNode headA, ListNode headB) {
        //定义两个节点
        ListNode tempa = headA;
        ListNode tempb = headB;
        //循环
        while (tempa != tempb) {
          //如果不为空就指针下移，为空就跳到另一链表的头部
           tempa = tempa!=null ? tempa.next:headB;
           tempb = tempb!=null ? tempb.next:headA;
        }
        return tempa;        
    }
}
```



好啦，链表的题目就结束啦，希望大家能有所收获，下周就要更新新的题型啦，继续坚持，肯定会有收获的。












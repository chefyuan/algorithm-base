给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。

你应当 保留 两个分区中每个节点的初始相对位置。

![](https://img-blog.csdnimg.cn/20210319190335143.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzODg1OTI0,size_16,color_FFFFFF,t_70) 

示例 1：


输入：head = [1,4,3,2,5,2], x = 3
输出：[1,2,2,4,3,5]
示例 2：

输入：head = [2,1], x = 2
输出：[1,2]

来源：力扣（LeetCode）

这个题目我的做题思路是这样的，我们先创建一个侦察兵，侦察兵负责比较链表值和 x 值，如果  >=  的话则接在 big 链表上，小于则接到 small 链表上，最后一个细节就是我们的 big 链表尾部要加上 null，不然会形成环。这是这个题目的一个小细节，很重要。

中心思想就是，将链表先分后合。

下面我们来看模拟视频吧。希望能给各位带来一丢丢帮助。

![](https://img-blog.csdnimg.cn/20210319190417499.gif)

**题目代码**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode partition(ListNode head, int x) {
        if (head == null) {
            return head;
        }
        ListNode pro = head;
        ListNode big = new ListNode(-1);
        ListNode small = new ListNode(-1); 
        ListNode headbig = big; 
        ListNode headsmall =small;  
        //分     
        while (pro != null) {           
            //大于时，放到 big 链表上
            if (pro.val >= x) {
                big.next = pro;
                big = big.next;
            // 小于放到 small 链表上
            }else {
                small.next = pro;
                small = small.next;
            }
            pro = pro.next;
        }
        //细节
        big.next = null;
        //合
        small.next = headbig.next;
        return headsmall.next;
    }
}
```






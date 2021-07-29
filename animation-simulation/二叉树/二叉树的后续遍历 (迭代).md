之前给大家介绍了二叉树的[前序遍历]()，[中序遍历]()的迭代法和 Morris 方法，今天咱们来说一下二叉后序遍历的迭代法及 Morris 方法。

注：阅读该文章前，建议各位先阅读之前的三篇文章，对该文章的理解有很大帮助。

## 迭代

后序遍历的相比前两种方法，难理解了一些，所以这里我们需要认真思考一下，每一行的代码的作用。

我们先来复习一下，二叉树的后序遍历

![](https://cdn.jsdelivr.net/gh/tan45du/test@master/photo/后序遍历.2bx6qccr1q1w.gif)

我们知道后序遍历的顺序是,` 对于树中的某节点, 先遍历该节点的左子树, 再遍历其右子树, 最后遍历该节点`。

那么我们如何利用栈来解决呢？

我们直接来看动画，看动画之前，但是我们`需要带着问题看动画`，问题搞懂之后也就搞定了后序遍历。

1.动画中的橙色指针发挥了什么作用

2.为什么动画中的某节点，为什么出栈后又入栈呢?

好啦，下面我们看动画吧！

![后序遍历迭代](https://img-blog.csdnimg.cn/20210622160754912.gif)

相信大家看完动画之后，也能够发现其中规律。

我们来对其中之前提出的问题进行解答

1.动画中的橙色箭头的作用？

> 用来定位住上一个访问节点，这样我们就知道 cur 节点的 right 节点是否被访问，如果被访问，我们则需要遍历 cur 节点。

2.为什么有的节点出栈后又入栈了呢？

> 出栈又入栈的原因是，我们发现 cur 节点的 right 不为 null ，并且 cur.right 也没有被访问过。因为 `cur.right != preNode `，所以当前我们还不能够遍历该节点，应该先遍历其右子树中的节点。
>
> 所以我们将其入栈后，然后`cur = cur.right`

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> list = new ArrayList<>();
        TreeNode cur = root;
        //这个用来记录前一个访问的节点，也就是橙色箭头
        TreeNode preNode = null;
        while (cur != null || !stack.isEmpty()) {
            //和之前写的中序一致
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            //1.出栈，可以想一下，这一步的原因。
            cur = stack.pop();
            //2.if 里的判断语句有什么含义？
            if (cur.right == null || cur.right == preNode) {
                list.add(cur.val);
                //更新下 preNode，也就是定位住上一个访问节点。
                preNode = cur;
                cur = null;
            } else {
                //3.再次压入栈，和上面那条 1 的关系？
                stack.push(cur);
                cur = cur.right;
            }
        }
        return list;
    }
}
```

Swift Code：

```swift
class Solution {
    func postorderTraversal(_ root: TreeNode?) -> [Int] {
        var list:[Int] = []
        var stack:[TreeNode] = []
        var cur = root, preNode: TreeNode?
        while !stack.isEmpty || cur != nil {
            //和之前写的中序一致
            while cur != nil {
                stack.append(cur!)
                cur = cur!.left
            }
            //1.出栈，可以想一下，这一步的原因。
            cur = stack.popLast()
            //2.if 里的判断语句有什么含义？
            if cur!.right === nil || cur!.right === preNode  {
                list.append(cur!.val)
                //更新下 preNode，也就是定位住上一个访问节点。
                preNode = cur
                cur = nil
            } else {
                //3.再次压入栈，和上面那条 1 的关系？
                stack.append(cur!)
                cur = cur!.right
            }
        }
        return list
    }
}
```

Go Code:

```go
func postorderTraversal(root *TreeNode) []int {
    res := []int{}
    if root == nil {
        return res
    }
    stk := []*TreeNode{}
    cur := root
    var pre *TreeNode
    for len(stk) != 0 || cur != nil {
        for cur != nil {
            stk = append(stk, cur)
            cur = cur.Left
        }
        // 这里符合本文最后的说法，使用先获取栈顶元素但是不弹出，根据栈顶元素的情况进行响应的处理。
        temp := stk[len(stk) - 1]
        if temp.Right == nil || temp.Right == pre {
            stk = stk[: len(stk) - 1]
            res = append(res, temp.Val)
            pre = temp
        } else {
            cur = temp.Right
        }
    }
    return res
}
```

当然也可以修改下代码逻辑将 `cur = stack.pop()` 改成 `cur = stack.peek()`，下面再修改一两行代码也可以实现，这里这样写是方便动画模拟，大家可以随意发挥。

时间复杂度 O（n）, 空间复杂度 O（n）

这里二叉树的三种迭代方式到这里就结束啦，大家可以进行归纳总结，三种遍历方式大同小异，建议各位，掌握之后，自己手撕一下，从搭建二叉树开始。

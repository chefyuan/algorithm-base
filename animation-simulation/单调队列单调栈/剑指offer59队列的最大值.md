> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

今天我们好好说�?�单调栈和单调队列。其实很容易理解，单调栈就是单调递�?�或单调递减的栈，栈内元素是有序的，单调队列同样也是�?

下面我们通过几个题目由浅入深，一点一点挖透他�?吧！

## 单调队列

#### [剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

#### 题目描述

请定义一�?队列并实现函�? max_value 得到队列里的最大�?

若队列为空，pop_front �? max_value 需要返�? -1

**示例 1�?**

> 输入: ["MaxQueue","push_back","push_back","max_value","pop_front","max_value"] > [[],[1],[2],[],[],[]]
> 输出: [null,null,null,2,1,2]

**示例 2�?**

> 输入:
> ["MaxQueue","pop_front","max_value"] > [[],[],[]]
> 输出: [null,-1,-1]

#### 题目解析�?

我们先来拆解下上面的示例 1

![队列的最大值](https://cdn.jsdelivr.net/gh/tan45du/github.io.phonto2@master/myphoto/队列的最大�?.6bfapy4zf1g0.png)

其实我�?�得这个题目的重点在理解题意上面，可能刚开始刷题的同�?�，对�?�意理解不�?�透彻，做起来没有那么得心应手，通过上面的图片我�?简单了解了一下�?�意，那我们应�?�怎么做才能实现上述�?�求�?�?

下面我们来�?�一下双�?队列。我�?之前说过的队列，遵守先进先出的�?�则，双�?队列则可以从队头出队，也�?以从队尾出队。我�?先通过一�?视�?�来简单了解下双�??队列�?

![](https://img-blog.csdnimg.cn/20210319154950406.gif)

我们�?以用双�??队列做辅助队列，用辅助队列来保存当前队列的最大值。我�?同时定义一�?�?通队列和一�?双�??单调队列。普通队列就正常执�?�入队，出队操作。max_value 操作则返回咱�?的双�?队列的队头即�?。下面我�?来看一下代码的具体执�?�过程吧�?

![](https://img-blog.csdnimg.cn/20210319154716931.gif)

我们来�?��?��?�进行解�?

1.我们需要维护一�?单调双�??队列，上面的队列则执行�?�常操作，下面的队列队头元素则为上面队列的最大�?

2.出队时，我们需要进行�?�比两个队列的队头元素是否相等，如果相等则同时出队，则出队后的双�?队列的头部仍�?上面队列�?的最大值�?

3.入队时，我们需要维持一�?单调递减的双�?队列，因为我�?需要确保队头元素为最大值嘛�?

```java
class MaxQueue {
    //�?通队�?
    Queue<Integer> que;
    //双�??队列
    Deque<Integer> deq;
    public MaxQueue() {
        que = new LinkedList<>();
        deq = new LinkedList<>();
    }
    //获取最大值值，返回我们双�??队列的�?�头即可，因为我�?双�??队列�?单调递减的嘛
    public int max_value() {
        return deq.isEmpty() ? -1 : deq.peekFirst();
    }
    //入队操作
    public void push_back(int value) {
        que.offer(value);
        //维护单调递减
        while (!deq.isEmpty() && value > deq.peekLast()){
            deq. pollLast();
        }
        deq.offerLast(value);

    }
    //返回队头元素，�?�时有个细节，我�?需要用equals
    //这里需要使�? equals() 代替 == 因为队列�?存储的是 int 的包装类 Integer
    public int pop_front() {
        if(que.isEmpty()) return -1;
        if (que.peek().equals(deq.peekFirst())) {
            deq.pollFirst();
        }
        return que.poll();
    }
}
```

**GO�?言版本�?**

```go
type MaxQueue struct {
    que []int	// �?通队�?
    deq []int	// 双�??队列
    size int	// que的队列长�?
}


func Constructor() MaxQueue {
    return MaxQueue{
        que: []int{},
        deq: []int{},
    }
}

// Is_empty 表示队列�?否为�?
func (mq *MaxQueue) Is_empty() bool {
    return mq.size == 0
}

// Max_value 取最大值值，返回我们双�??队列的�?�头即可，因为我�?双�??队列�?单调递减的嘛 
func (mq *MaxQueue) Max_value() int {
    if mq.Is_empty() { return -1 }
    return mq.deq[0]
}

// Push_back 入队
func (mq *MaxQueue) Push_back(value int)  {
    mq.que = append(mq.que, value)
    // 维护单调递减队列
    for len(mq.deq) != 0 && mq.deq[len(mq.deq) - 1] < value {
        mq.deq = mq.deq[:len(mq.deq) - 1]
    }
    mq.deq = append(mq.deq, value)
    mq.size++
}

// Pop_front 弹出队列头元素，并且返回其值�?
func (mq *MaxQueue) Pop_front() int {
    if mq.Is_empty() { return -1 }
    ans := mq.que[0]
    mq.que = mq.que[1:]
    if mq.deq[0] == ans {
        mq.deq = mq.deq[1:]
    }
    mq.size--
    return ans
}
```

### 

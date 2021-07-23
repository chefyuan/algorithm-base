> 如果阅读时，发现错误，或者动画不可以显示的问题可以添加我微信好友 **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/个人微信.15egrcgqd94w.jpg)** ，备注 github + 题目 + 问题 向我反馈
>
> 感谢支持，该仓库会一直维护，希望对各位有一丢丢帮助。
>
> 另外希望手机阅读的同学可以来我的 <u>[**公众号：袁厨的算法小屋**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同步，想要和题友一起刷题，互相监督的同学，可以在我的小屋点击<u>[**刷题小队**](https://raw.githubusercontent.com/tan45du/test/master/微信图片_20210320152235.2pthdebvh1c0.png)</u>进入。

> 为保证代码严谨性，文中所有代码均在 leetcode 刷题网站 AC ，大家可以放心食用。

皇上生辰之际，举国同庆，袁记菜馆作为天下第一饭店，所以被选为这次庆典的菜品供应方，这次庆典对于袁记菜馆是一项前所未有的挑战，毕竟是第一次给皇上庆祝生辰，稍有不慎就是掉脑袋的大罪，整个袁记菜馆内都在紧张的布置着。此时突然有一个店小二慌慌张张跑到袁厨面前汇报，到底发生了什么事，让店小二如此慌张呢？

袁记菜馆内

店小二：不好了不好了，掌柜的，出大事了。

袁厨：发生什么事了，慢慢说，如此慌张，成何体统。（开店开久了，架子出来了哈）

店小二：皇上按照咱们菜单点了 666 道菜，但是咱们做西湖醋鱼的师傅请假回家结婚了，不知道皇上有没有点这道菜，如果点了这道菜，咱们做不出来，那咱们店可就完了啊。

（袁厨听了之后，吓得一屁股坐地上了，缓了半天说道）

袁厨：别说那么多了，快给我找找皇上点的菜里面，有没有这道菜！

找了很久，并且核对了很多遍，最后确认皇上没有点这道菜。菜馆内的人都松了一口气

通过上面的一个例子，让我们简单了解了字符串匹配。

字符串匹配：设 S 和 T 是给定的两个串，在主串 S 中找到模式串 T 的过程称为字符串匹配，如果在主串 S 中找到 模式串 T ，则称匹配成功，函数返回 T 在 S 中首次出现的位置，否则匹配不成功，返回 -1。

例：

![字符串匹配](https://cdn.jsdelivr.net/gh/tan45du/photobed@master/photo/字符串匹配.3q9wqbh8ws40.png)

在上图中，我们试图找到模式 T = baab,在主串 S = abcabaabcabac 中第一次出现的位置，即为红色阴影部分， T 第一次在 S 中出现的位置下标为 4 （ 字符串的首位下标是 0 ），所以返回 4。如果模式串 T 没有在主串 S 中出现，则返回 -1。

解决上面问题的算法我们称之为字符串匹配算法，今天我们来介绍三种字符串匹配算法，大家记得打卡呀，说不准面试的时候就问到啦。

## BF 算法（Brute Force）

这个算法很容易理解，就是我们将模式串和主串进行比较，一致时则继续比较下一字符，直到比较完整个模式串。不一致时则将模式串后移一位，重新从模式串的首位开始对比，重复刚才的步骤下面我们看下这个方法的动图解析，看完肯定一下就能搞懂啦。

![请添加图片描述](https://img-blog.csdnimg.cn/20210319193924425.gif)

通过上面的代码是不是一下就将这个算法搞懂啦，下面我们用这个算法来解决下面这个经典题目吧。

### leetcdoe 28. 实现 strStr()

#### 题目描述

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从 0 开始)。如果不存在，则返回 -1。

示例 1:

> 输入: haystack = "hello", needle = "ll"
> 输出: 2

示例 2:

> 输入: haystack = "aaaaa", needle = "bba"
> 输出: -1

#### 题目解析

其实这个题目很容易理解，但是我们需要注意的是一下几点，比如我们的模式串为 0 时，应该返回什么，我们的模式串长度大于主串长度时，应该返回什么，也是我们需要注意的地方。下面我们来看一下题目代码吧。

#### 题目代码

Java Code:

```java
class Solution {
    public int strStr(String haystack, String needle) {
        int haylen = haystack.length();
        int needlen = needle.length();
        //特殊情况
        if (haylen < needlen) {
            return -1;
        }
        if (needlen == 0) {
            return 0;
        }
        //主串
        for (int i = 0; i < haylen - needlen + 1; ++i) {
            int j;
            //模式串
            for (j = 0; j < needlen; j++) {
                //不符合的情况，直接跳出，主串指针后移一位
                if (haystack.charAt(i+j) != needle.charAt(j)) {
                    break;
                }
            }
            //匹配成功
            if (j == needlen) {
                return i;
            }

        }
        return -1;
    }
}
```

Python Code:

```python
from typing import List
class Solution:
    def strStr(self, haystack: str, needle: str)->int:
        haylen = len(haystack)
        needlen = len(needle)
        # 特殊情况
        if haylen < needlen:
            return -1
        if needlen == 0:
            return 0
        # 主串
        for i in range(0, haylen - needlen + 1):
            # 模式串
            j = 0
            while j < needlen:
                if haystack[i + j] != needle[j]:
                    break
                j += 1
            # 匹配成功
            if j == needlen:
                return i
        return -1
```

我们看一下 BF 算法的另一种算法（显示回退），其实原理一样，就是对代码进行了一下修改，只要是看完咱们的动图，这个也能够一下就能看懂，大家可以结合下面代码中的注释和动图进行理解。

Java Code:

```java
class Solution {
    public int strStr(String haystack, String needle) {
        //i代表主串指针，j模式串
        int i,j;
        //主串长度和模式串长度
        int halen = haystack.length();
        int nelen = needle.length();
        //循环条件，这里只有 i 增长
        for (i = 0 , j = 0; i < halen && j < nelen; ++i) {
            //相同时，则移动 j 指针
            if (haystack.charAt(i) == needle.charAt(j)) {
                ++j;
            } else {
                //不匹配时，将 j 重新指向模式串的头部，将 i 本次匹配的开始位置的下一字符
                i -= j;
                j = 0;
            }
        }
        //查询成功时返回索引，查询失败时返回 -1；
        int renum = j == nelen ? i - nelen : -1;
        return renum;

    }
}
```

Python Code:

```python
from typing import List
class Solution:
    def strStr(self, haystack: str, needle: str)->int:
        # i代表主串指针，j模式串
        i = 0
        j = 0
        # 主串长度和模式串长度
        halen = len(haystack)
        nelen = len(needle)
        # 循环条件，这里只有 i 增长
        while i < halen and j < nelen:
            # 相同时，则移动 j 指针
            if haystack[i] == needle[j]:
                j += 1
            else:
                # 不匹配时，将 j 重新只想模式串的头部，将 i 本次匹配的开始位置的下一字符
                i -= j
                j = 0
            i += 1
            # 查询成功时返回索引，查询失败时返回 -1
            renum = i - nelen if j == nelen else -1
        return renum
```

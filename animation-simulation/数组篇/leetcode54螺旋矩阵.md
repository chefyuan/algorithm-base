> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

#### [54. 螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/)

题目描述

_给定一�?包含 m_ x n �?元素的矩阵（m �?, n 列），�?�按照顺时针螺旋顺序，返回矩阵中的所有元素�?

示例一

> 输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
> 输出：[1,2,3,6,9,8,7,4,5]

示例�?

> 输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
> 输出：[1,2,3,4,8,12,11,10,9,5,6,7]

这个题目很细非常细，思路很�?�易想到，但�?要是完全实现也不�?特别容易，我�?一起分析下这个题目，我�?�?以这样理解，我们像剥洋葱似的一步�?�的剥掉外皮，直到遍历结束，见下图�?

![](https://img-blog.csdnimg.cn/img_convert/cfa0192601dcc185e77125adc35e1cc5.png)\*

题目很�?�易理解，但�?要想完全执�?�出来，也是不�?�易的，因为这里面的细节�?多了，我�?需要�?�真仔细的考虑边界�?

我们也�?�考虑重�?�遍历的情况即什么时候跳出循�?。刚才我�?通过�?头知道了我们元素的遍历顺序，这个题目也就完成了一大半了，下面我们来�?��?�一下什么时候跳出循�?，�?�下图�?

�?：这里需要注意的�?，�?��?�代表的�?每个边界�?

![](https://img-blog.csdnimg.cn/20210318095839543.gif)

题目代码�?

Java Code:

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {

        List<Integer> arr = new ArrayList<>();
        int left = 0, right = matrix[0].length-1;
        int top = 0, down = matrix.length-1;

        while (true) {
             for (int i = left; i <= right; ++i) {
                 arr.add(matrix[top][i]);
             }
             top++;
             if (top > down) break;
             for (int i = top; i <= down; ++i) {
                 arr.add(matrix[i][right]);
             }
             right--;
             if (left > right) break;
             for (int i = right; i >= left; --i) {
                 arr.add(matrix[down][i]);
             }
             down--;
             if (top > down) break;
             for (int i = down; i >= top; --i) {
                 arr.add(matrix[i][left]);
             }
             left++;
             if (left > right) break;

        }
        return arr;
    }
}

```

C++ Code:

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector <int> arr;
        int left = 0, right = matrix[0].size()-1;
        int top = 0, down = matrix.size()-1;
        while (true) {
             for (int i = left; i <= right; ++i) {
                 arr.emplace_back(matrix[top][i]);
             }
             top++;
             if (top > down) break;
             for (int i = top; i <= down; ++i) {
                 arr.emplace_back(matrix[i][right]);
             }
             right--;
             if (left > right) break;
             for (int i = right; i >= left; --i) {
                 arr.emplace_back(matrix[down][i]);
             }
             down--;
             if (top > down) break;
             for (int i = down; i >= top; --i) {
                 arr.emplace_back(matrix[i][left]);
             }
             left++;
             if (left > right) break;
        }
        return arr;
    }
};
```

Python3 Code:

```python
from typing import List
class Solution:
    def spiralOrder(self, matrix: List[List[int]])->List[int]:
        arr = []
        left = 0
        right = len(matrix[0]) - 1
        top = 0
        down = len(matrix) - 1
        while True:
            for i in range(left, right + 1):
                arr.append(matrix[top][i])
            top += 1
            if top > down:
                break
            for i in range(top, down + 1):
                arr.append(matrix[i][right])
            right -= 1
            if left > right:
                break
            for i in range(right, left - 1, -1):
                arr.append(matrix[down][i])
            down -= 1
            if top > down:
                break
            for i in range(down, top - 1, -1):
                arr.append(matrix[i][left])
            left += 1
            if left > right:
                break
        return arr
```

Swift Code

```swift
class Solution {
    func spiralOrder(_ matrix: [[Int]]) -> [Int] {
        var arr:[Int] = []
        var left = 0, right = matrix[0].count - 1
        var top = 0, down = matrix.count - 1

        while (true) {
            for i in left...right {
                arr.append(matrix[top][i])
            }
            top += 1
            if top > down { break }
            for i in top...down {
                arr.append(matrix[i][right])
            }
            right -= 1
            if left > right { break}
            for i in stride(from: right, through: left, by: -1) {
                arr.append(matrix[down][i])
            }
            down -= 1
            if top > down { break}
            for i in stride(from: down, through: top, by: -1) {
                arr.append(matrix[i][left])
            }
            left += 1
            if left > right { break}
        }

        return arr
    }
}
```

Go Code:

```go
func spiralOrder(matrix [][]int) []int {
    res := []int{}
    left, right := 0, len(matrix[0]) - 1
    top, down   := 0, len(matrix) - 1

    for {
        for i := left; i <= right; i++ {
            res = append(res, matrix[top][i])
        }
        top++
        if top > down { break }

        for i := top; i <= down; i++ {
            res = append(res, matrix[i][right])
        }
        right--
        if left > right { break }

        for i := right; i >= left; i-- {
            res = append(res, matrix[down][i])
        }
        down--
        if top > down { break }
        
        for i := down; i >= top; i-- {
            res = append(res, matrix[i][left])
        }
        left++
        if left > right { break }
    }
    return res
}
```


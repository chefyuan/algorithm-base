> 如果阅�?�时，发现错�?，或者动画不�?以显示的�?题可以添加我�?信好�? **[tan45du_one](https://raw.githubusercontent.com/tan45du/tan45du.github.io/master/�?人微�?.15egrcgqd94w.jpg)** ，�?�注 github + 题目 + �?�? 向我反�??
>
> 感谢�?持，该仓库会一直维护，希望对各位有一�?丢帮助�?
>
> 另�?�希望手机阅读的同�?�可以来我的 <u>[**�?众号：�?�厨的算法小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u> 两个平台同�?�，想�?�和题友一起刷题，互相监督的同学，�?以在我的小屋点击<u>[**刷�?�小�?**](https://raw.githubusercontent.com/tan45du/test/master/�?信图片_20210320152235.2pthdebvh1c0.png)</u>进入�?

### [75 颜色分类](https://leetcode-cn.com/problems/sort-colors/)

题目描述�?

给定一�?包含红色、白色和蓝色，一�? n �?元素的数组，原地对它�?进�?�排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列�?

此�?�中，我�?使用整数 0�? 1 �? 2 分别表示红色、白色和蓝色�?

示例 1�?

> 输入：nums = [2,0,2,1,1,0]
> 输出：[0,0,1,1,2,2]

示例 2�?

> 输入：nums = [2,0,1]
> 输出：[0,1,2]

示例 3�?

> 输入：nums = [0]
> 输出：[0]

示例 4�?

> 输入：nums = [1]
> 输出：[1]

**做�?�思路**

这个题目我们使用 Arrays.sort() 解决，哈哈，但是那样�?无聊啦，题目�?义就�?让我�?将所有的 0 放在前面�?2 放在后面�?1 放在�?间，�?不是和我�?上面说的荷兰国旗�?题一样。我�?仅仅�? 1 做为 pivot 值�?

下面我们直接看代码吧，和三向切分基本一致�?

Java Code:

```java
class Solution {
    public void sortColors(int[] nums) {
        int len = nums.length;
        int left = 0;
        //这里和三向切分不完全一�?
        int i = left;
        int right = len-1;

        while (i <= right) {
             if (nums[i] == 2) {
                 swap(nums,i,right--);
             } else if (nums[i] == 0) {
                 swap(nums,i++,left++);
             } else {
                 i++;
             }
        }
    }
    public void swap (int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

Python3 Code:

```python
from typing import List
class Solution:
    def sortColors(self, nums: List[int]):
        leng = len(nums)
        left = 0
        # 这里和三向切分不完全一�?
        i = left
        right = leng - 1
        while i <= right:
            if nums[i] == 2:
                self.swap(nums, i, right)
                right -= 1
            elif nums[i] == 0:
                self.swap(nums, i, left)
                i += 1
                left += 1
            else:
                i += 1
        return nums

    def swap(self, nums: List[int], i: int, j: int):
        temp = nums[i]
        nums[i] = nums[j]
        nums[j] = temp
```

C++ Code:

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int len = nums.size(), left = 0;
        int i = left, right = len-1;
        while (i <= right) {
             if (nums[i] == 2) {
                 swap(nums[i],nums[right--]);
             } else if (nums[i] == 0) {
                 swap(nums[i++],nums[left++]);
             } else {
                 i++;
             }
        }
    }
};
```

Swift Code:

```swift
class Solution {
    func sortColors(_ nums: inout [Int]) {

        let count = nums.count
        var left = 0, i = left, right = count - 1
        while i <= right {
            if nums[i] == 2 {
                //nums.swapAt(i, right) 直接调用系统方法
                self.swap(&nums, i, right) // 保持风格统一走自定义交换
                right -= 1
            } else if nums[i] == 0 {
                //nums.swapAt(i, left) 直接调用系统方法
                self.swap(&nums, i, left) // 保持风格统一走自定义交换
                i += 1
                left += 1
            } else {
                i += 1
            }
        }
    }

    func swap(_ nums: inout [Int], _ i: Int, _ j: Int) {
        let temp = nums[i]
        nums[i] = nums[j]
        nums[j] = temp
    }
}
```

Go Code:

```go
func sortColors(nums []int)  {
    length := len(nums)
    left, right := 0, length - 1
    i := left
    for i <= right {
        if nums[i] == 2 {
            // �?2换到最�?
            nums[i], nums[right] = nums[right], nums[i]
            right--
        } else if nums[i] == 0 {
            // �?0换到最前面
            nums[i], nums[left] = nums[left], nums[i]
            i++
            left++
        } else {
            i++
        }
    }
}
```



另�?�我�?看这段代码，有什么问题呢？那就是我们即使完全符合时，仍会交换元素，这样会大大降低我们的效率�?

例�?�：[0,0,0,1,1,1,2,2,2]

此时我们完全符合情况，不需要交换元素，但是按照我们上面的代码，0,2 的每�?元素会和�?己进行交�?，所以这里我�?�?以根�? i �? left 的值是否相等来决定�?否需要交�?，大家可以自己写一下�?

下面我们看一下另外一种写�?

这个题目的关�?点就�?，当我们 nums[i] �? nums[right] 交换后，我们�? nums[right] 此时指向的元素是符合要求的，但是我们 nums[i] 指向的元素不一定�?�合要求，所以我�?需要继�?判断�?

![细节地方](https://cdn.jsdelivr.net/gh/tan45du/test@master/photo/�?信截图_20210305153911.28capmzljy80.png)

我们 2 �? 0 交换后，此时 i 指向 0 �?0 应放在头�?，所以不符合情况，所�? 0 �? 1 仍需要交�?。下面我�?来看一下动画来加深理解吧�?

![](https://img-blog.csdnimg.cn/20210318093047325.gif#pic_center)

另一种代码表�?

Java Code:

```java
class Solution {
    public void sortColors(int[] nums) {

        int left = 0;
        int len = nums.length;
        int right = len - 1;
        for (int i = 0; i <= right; ++i) {
            if (nums[i] == 0) {
                swap(nums,i,left);
                left++;
            }
            if (nums[i] == 2) {
                swap(nums,i,right);
                right--;
                //如果不等�? 1 则需要继�?判断，所以不移动 i 指针，i--
                if (nums[i] != 1) {
                    i--;
                }
            }
        }

    }
    public void swap (int[] nums,int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

Python3 Code:

```python
from typing import List
class Solution:
    def sortColors(self, nums: List[int]):
        left = 0
        leng = len(nums)
        right = leng - 1
        i = 0
        while i <= right:
            if nums[i] == 0:
                self.swap(nums, i, left)
                left += 1
            if nums[i] == 2:
                self.swap(nums, i, right)
                right -= 1
                # 如果不等�? 1 则需要继�?判断，所以不移动 i 指针，i--
                if nums[i] != 1:
                    i -= 1
            i += 1
        return nums

    def swap(self, nums: List[int], i: int, j: int):
        temp = nums[i]
        nums[i] = nums[j]
        nums[j] = temp
```

C++ Code:

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int left = 0, len = nums.size();
        int right = len - 1;
        for (int i = 0; i <= right; ++i) {
            if (nums[i] == 0) {
                swap(nums[i],nums[left++]);
            }
            if (nums[i] == 2) {
                swap(nums[i],nums[right--]);
                if (nums[i] != 1) {
                        i--;
                    }
                }
            }
        }
};
```

Swift Code:

```swift
class Solution {
    func sortColors(_ nums: inout [Int]) {

        let count = nums.count
        var left = 0, i = left, right = count - 1
        while i <= right {
            if nums[i] == 0 {
                //nums.swapAt(i, left) 直接调用系统方法
                self.swap(&nums, i, left) // 保持风格统一走自定义交换
                left += 1
            }
            if nums[i] == 2 {
                //nums.swapAt(i, right) 直接调用系统方法
                self.swap(&nums, i, right) // 保持风格统一走自定义交换
                right -= 1
                //如果不等�? 1 则需要继�?判断，所以不移动 i 指针，i--
                if nums[i] != 1 {
                    i -= 1
                }
            }
            i += 1
        }
    }

    func swap(_ nums: inout [Int], _ i: Int, _ j: Int) {
        let temp = nums[i]
        nums[i] = nums[j]
        nums[j] = temp
    }
}
```

Go Code:

```go
func sortColors(nums []int)  {
    length := len(nums)
    left, right := 0, length - 1
    for i := 0; i <= right; i++ {
        if nums[i] == 0 {
            // �?0时，和头交换
            nums[i], nums[left] = nums[left], nums[i]
            left++
        } else if nums[i] == 2 {
            // �?2时，和尾交换
            nums[i], nums[right] = nums[right], nums[i]
            right--
            // 不为1时，需要把i减回�?
            if nums[i] != 1 {
                i--
            }
        }
    }
}
```


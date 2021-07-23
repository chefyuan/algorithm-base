# Leetcode 常用函数

## 链表篇

一些节点，除了最后一个节点以外的每一个节点都存储着下一个节点的地址，依据这种方法依次连接， 构成一个链式结构。

### ListNode

```java
ListNode list=new ListNode(0)
```

初始化一个值为 0 的空节点，提倡的写法

### HashSet

HashSet 基于 HashMap 来实现的，是一个不允许有重复元素的集合但是允许有 null 值，HashSet 是无序的，即不会记录插入的顺序。HashSet 不是线程安全的， 如果多个线程尝试同时修改 HashSet，则最终结果是不确定的。 您必须在多线程访问时显式同步对 HashSet 的并发访问。

```java
HashSet<String> sites = new HashSet<String>();
```

#### add()

往 HashSet 里添加元素

```
sites.add("我是袁厨，大家快快关注我吧");
```

#### size()

#### remove()

remover()size()也是会用到的函数，具体用法和 ArrayList 一样

#### contains()

判断元素是否存在

```
System.out.println(sites.contains("我是袁厨，大家快快关注我吧"));
```

> 输出：true；

## 数组篇

### length

该函数是用来得到数组长度的函数，这里需要注意的是 length 后面没有括号

### sort()

该函数用于给数组进行排序，这两个函数用的比较多

### Arrays.fill()

用于填充数组

一共有四个参数，分别是数组，开始索引，结束索引，填充数值。

```
Arrays.fill(nums, 0, 2, 0);
for(int x:nums){
  System.out.println(x);
}
```

> 输出：0,0

### Arrays.sort()

给数组排序,也可以做到部分排序 ，在括号中添加索引即可

```
int[] array = {1,6,3,4};
Arrays.sort(array);
return array;
```

> array : 1,3,4,6;

### Arrays.copyOfRange()

将一个原始的数组，从下标 0 开始复制，复制到上标 2，生成一个新的数组

```
int[] array = {1,2,3,4};
int[] ar= Arrays.copyOfRange(intersection, 0, 2);
return ar;

```

> array2: 1 , 2 ;

### System.arraycopy();

```java
System.arraycopy(targetnums,beganindex, newnums, newindex, length);
```

targetnums:目标数组，想要复制的数组

beganindex:目标数组开始索引

newsnums:复制到的新数组

newindex:开始索引

length：想要复制的长度

```java
 int[] array = {1,2,3,4};
 int[] newarray  =  new int[2];
 System.arraycopy(array,0,newarray,0,2);
 for(int x : newarray){
     System.out.println(x)
 }
```

> 输出：1，2

### 逻辑运算符

#### x | 0

得到的仍然是他本身，

例：1001|0000=1001；或运算代表的是如果两位其中有一个 1 则返回 1，否则为 0；

```java
public static void main(String[] args) {
        int x =10 ;
        System.out.println(x|0);
    }
```

> 输出：10

#### x & 0

无论任何数都会输出 0，这个也很好理解。

例：1001&0000=0000;两位都为 1 才能返回 1

```
public static void main(String[] args) {
        int x =10 ;
        System.out.println(x&0);
    }
```

> 输出：0

#### x ^ 0

得到的还是他本身，这个也很好理解，异或的含义就是如果相同输出 0，如果不同输出 1

例：0111^0000=0111 第一位相同，其余位不同

```java
public static void main(String[] args) {
    int x =-10 ;
    System.out.println(x^0);
}
```

> 输出：-10

#### x | 1

如果是奇数的话，还是它本身，偶数的话则加 1；

```java
int x =-9 ;
int y = -10;
System.out.println(x|1);
System.out.println(y|1);
```

> 输出：-9，-9

#### x ^ 1

如果是偶数则加 1，如果是奇数则减 1；

```java
int x =-9 ;
int y = -10;
System.out.println(x^1);
System.out.println(y^1);
```

> 输出：-10，-9

#### x & 1

得出最后一位是 0 还是 1，通常会用来判断奇偶

```java
int x =-9 ;
int y = -10;
System.out.println(x&1);
System.out.println(y&1);
```

> 输出：1，0

#### 1<<3

代表的含义是将 1 左移 3 位，即 0001 ---->1000 则为 2^3 为 8

```java
System.out.println(1<<3);
```

> 输出：8

#### HashMap

创建一个 HashMap,两种数据类型

```
HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();
```

往 hashmap 里面插入数据

```java
for (int num : arr){
     map.put(num, map.getOrDefault(num, 0) + 1);//如果没有则添加，如果有则加1
 }
```

遍历 Hashmap,查询值为 k 的元素

```
for (int k : hashmap.keySet())
      if (hashmap.get(k) == 1) return k;

```

遍历 HashSet

```
set.iterator().next();//迭代器
```

## 树篇

### ArrayList<List<对象类型>>

```java
List<List<Integer>> arr = new  ArrayList<List<Integer>>();
```

用来创建二维的动态数组，层次遍历用到这个。

### ArrayList

```java
List<Integer> array = new ArrayList<>();
```

ArrayList 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素。<>代表的数组类型

#### add()元素,括号内为需要添加的元素

```java
public class Test {
    public static void main(String[] args) {
        List<String> array = new ArrayList<>();
        array.add("大家好我是袁厨");
        System.out.println(array);
    }
}
```

> 输出：大家好我是袁厨

#### get()

get()函数用于获取动态数组的元素，括号内为索引值

```java
public class Test {
    public static void main(String[] args) {
        List<String> array = new ArrayList<>();
        array.add("大家好我是袁厨");
        System.out.println(array.get(0));//获取第一个元素
    }
}

```

> 输出：大家好我是袁厨

#### set()

set()用于修改元素，括号内为索引值

```
public class Test {
    public static void main(String[] args) {
        List<String> array = new ArrayList<>();
        array.add("大家好我是袁厨");
        array.set(0,"祝大家天天开心")
        System.out.println(array.get(0));//获取第一个元素
    }
}
```

> 输出：祝大家天天开心

#### remove()

用来删除数组内的元素

```
public class Test {
    public static void main(String[] args) {
        List<String> array = new ArrayList<>();
        array.add("大家好我是袁厨");
        array.add("祝大家天天开心");
        array.remove(0);
        System.out.println(array);//获取第一个元素
    }
}
```

> 输出：祝大家天天开心

#### isEmpty()

isEmpty()函数判断是否为空，这个函数用到的地方很多，队列和栈的时候总会用。总是会在 while 循环中使用

while(!queue.isEmpty()){

//用来判断队列是否为空的情况

}

```
public class Test {
    public static void main(String[] args) {
        List<String> array = new ArrayList<>();
        array.add("大家好我是袁厨");
        array.add("祝大家天天开心");
        array.remove(0);
        System.out.println(array.isEmpty());//获取第一个元素
    }
}
```

输出：false

#### clear()

该函数用来清空动态数组

```
ArrayList<String> sites = new ArrayList<>();
        sites.add("袁厨不帅");
        sites.add("袁厨不帅");
        sites.add("袁厨不帅");
        System.out.println(sites);
        // 删除所有元素
        sites.clear();
        System.out.println(sites);
```

> ```
> 删除前：[袁厨不帅，袁厨不帅，袁厨不帅]删除后：[]
> ```

#### sort()

该函数用来给动态数组排序，这个有时也会用到。

```
public class leetcode {
    public static void main(String[] args) {
         int[] arr = {4,5,1,3,6};
         Arrays.sort(arr);
         for(int x : arr){
             System.out.println(x);
         }

    }
}
```

> 输出：1，3，4，5，6

## 字符串篇

### StringBuffer

StringBuilder 类在 Java 5 中被提出，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。

```Java
public class Test{
  public static void main(String args[]){
    StringBuffer sBuffer = new StringBuffer("我的");
    sBuffer.append("名字");
    sBuffer.append("是");
    sBuffer.append("袁厨");
    sBuffer.append("大家点个关注吧");
    System.out.println(sBuffer);
  }
}
```

> 输出：我的名字是袁厨大家点个关注吧

String 中的字符串是不允许修改的，这个 StringBuffer 可以进行修改，做字符串的题目时会经常用到，树的题目中也偶尔会遇到

### charAt(i)

charAt() 方法用于返回指定索引处的字符。索引范围为从 0 到 length() - 1。

```java
public class Test {
    public static void main(String[] args) {
        String s = "大家好我是袁厨，点个关注哦";
        char result = s.charAt(6);
        System.out.println(result);
    }
}
```

> 输出：厨

这个函数的用法，就跟我们根据数组的索引输出值一样。在字符串题目中也比较常用。

### s.charAt(index)-'0'

这个函数的用途是将字符串索引值变成 int 型。知道这个可以大大提高刷题效率。大家可以掌握一下。

```java
public class Test {
    public static String getType(Object test) {
        return test.getClass().getName();
    }
    public static void main(String[] args) {

        String s = "祝大家永不脱发，点个关注哦";
        System.out.println(getType(s.charAt(6)-'0'));
    }
}
```

> 输出：java.lang.Integer

### Integer.toString()

该函数用于将 int 型变为 string 型，比如这个**第 9 题求回文数**的题目，我们就是先将 x 变为字符串，然后再遍历字符串

```java
class Solution {
    public boolean isPalindrome(int x) {
       if(x<0){
           return false;
       }
       //将int型变成string型，然后遍历字符串，不再需要使用额外数组进行存储
       String t = Integer.toString(x);
       int i = 0;
       int j = t.length()-1;
        //双指针遍历
       while(i<j){
           if(t.charAt(i)!=t.charAt(j)){
               return false;
           }
           else{
               i++;
               j--;
           }
       }
       return true;
    }
}
```

### substring()

substring() 方法返回字符串的子字符串

```java
public String substring(int beginIndex);
public String substring(int beginIndex, int endIndex);
```

表示两种情况，一种是从 beginIndex 到结尾，一种是从 beginIndex ->endIndex;

```
   String Str = new String("程序员爱做饭");
   System.out.println(Str.substring(3) );
   System.out.println(Str.substring(4, 5) );
```

> 输出：爱做饭，做

### equals()

equals() 方法用于判断 Number 对象与方法的参数和类型是否相等。

```
public static void main(String args[]){
        Integer x = 5;
        Integer y = 10;
        Integer z =5;
        Short a = 5;
        System.out.println(x.equals(y));
        System.out.println(x.equals(z));
        System.out.println(x.equals(a));
    }
```

> 输出：false,true,false

### toCharArray()

```java
String num = "12345";
char[] s = num.toCharArray();//将字符串变为char数组
System.out.println(s);
```

> 输出：12345

### char 数组变为 String

```java
String newstr = new String (arr2,start,end);
```

### indexOf

- **int indexOf(String str):** 返回指定字符在字符串中第一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1。
- **int indexOf(String str, int fromIndex):** 返回从 fromIndex 位置开始查找指定字符在字符串中第一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1

```
String s = "LkLLAAAOOO";
return s.indexOf("LLL");
```

> 返回-1

## 栈（Stack）

#### 创建栈

```
Stack<TreeNode> stack = new Stack<TreeNode>();//创建栈
```

上面的是创建新栈，栈的变量类型为 TreeNode,我们用深度优先遍历树来举例

#### push()

把项压入栈顶部

```
 stack.push(root);//将根节点入栈
```

#### pop()

移除堆栈顶部的对象，并作为此函数的值返回该对象。

```java
TreeNode temp = stack.pop();//将栈顶元素出栈，赋值TreeNode变量temp
```

peek()

查看栈顶元素但是不移除它

```java
 stack.push(root);
 TreeNode temp2 = stack.peek();
 System.out.println(temp2.val);
```

#### 出栈操作

```
StringBuilder str = new StringBuilder();
//遍历栈
while(!stack.isEmpty()){
    str.append(stack.pop());
 }
 //反转并变为字符串
return str.reverse().toString();
```

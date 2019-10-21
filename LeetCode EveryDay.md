# LeetCode EveryDay

[TOC]



## 基础排序算法

### 1，快速排序-分治

> 思路
>
> - 确定分界点：q[left],q[right],q[(left+right)/2]
> - 调整区间 小于x的在左边，大于x的在右边（<font color=red>重点</font>）
> - 递归处理左右两边排序



## Day 1

认识时间复杂度

### 时间复杂度

##### 两数之和

> 1.两数之和（2019.09）
>
> 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。
>
> 示例:
>
> 给定 nums = [2, 7, 11, 15], target = 9
>
> 因为 nums[0] + nums[1] = 2 + 7 = 9
> 所以返回 [0, 1]

```java 
class Solution {
  /**
  *1,利用hashmap实现
  *2，如果数组中不能包含重复元素
  *3，时间复杂度O（n）
  */
    public int[] twoSum(int[] nums, int target) {
        // use HashMap
        Map<Integer,Integer> arraysMap = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            int temp = target - nums[i];
            if(arraysMap.containsKey(temp)){
                return new int[]{i, arraysMap.get(temp)};
            }
            arraysMap.put(nums[i], i);
        }
        throw new IllegalArgumentException("No two sum solution!");
    }
}
```



## Day 2

### 国庆旅行

>2.国庆旅行
>
>小明国庆节来北京玩，北京有N个景点，第 i 个景点的评分用a[i]表示，两个景点i, j之间的距离为j - i(j > i)。
>
>小明一天只能游玩两个景点，我们认为总评分是两个景点的评分之和减去两个景点之间的距离，即为a[i]+a[j]+i-j。
>
>那么小明选择哪两个景点才会总评分最大呢？
>
>#### 输入格式
>
>第一行包含整数N。
>
>第二行分别输入N个景点的评分。
>
>#### 输出格式
>
>输出最大评分
>
>#### 数据范围
>
>2≤N≤10^5
>1≤a[i]≤1000
>
>#### 输入样例：
>
>```
>5
>11 6 5 18 12
>```
>
>#### 输出样例：
>
>```
>29
>```

```java
/**
     * 思路：维护最大值
     * a[i]+a[j]+i-j = a[i]+i + a[j]-j
     * O(n)
     * @param fieldNum 景点数目
     * @param fieldList 景点分值列表
     */
    public static int travel(int fieldNum, int[] fieldList){
        //O(n)时间复杂度方式
        int res = 0,aiScore = fieldList[0];
        for(int j = 1;j<fieldList.length;j++){
            //因为j是从第1个开始
            res = Math.max(res, (aiScore+fieldList[j]-j));
            //算出1时的Max的a[i] （a[j]+j） == a[i]+i
            aiScore = Math.max(aiScore, (fieldList[j]+j));

        }
        return res;
    }
```

### 整数反转

>3.整数反转
>
>给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。
>
>示例 1:
>
>输入: 123
>输出: 321
> 示例 2:
>
>输入: -123
>输出: -321
>示例 3:
>
>输入: 120
>输出: 21
>注意:
>
>假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−2^31,  2^31 − 1]。请根据这个假设，**如果反转后整数溢出那么就返回 0**。

```java
class Solution {
    public int reverse(int x) {
        /**
        思路： 逆序只需要从右往左计算
        注意点：int类型逆序可能会溢出，溢出为0
        时间复杂度分析：int型整数在十进制表示下最多有10位，对于每一位的计算量是常数级的，所以总时间复杂度是 O(1)
        **/
        Long res = 0L;
        /**
        正数：x = 123 
        0*10+(123%10)  x = 12 res = 3
        3*10 + (12%10)  x = 1 res = 32
        32*10 + (1%10)  x= 0 res = 321
        
        负数: x = -321
        
        **/
        while(x != 0){
            res = res*10 + x%10; 
            x = x/10;
        }
        if(res>Integer.MAX_VALUE || res < Integer.MIN_VALUE){
            return 0;
        }
        return res.intValue();
    }
}
```

## Day 3

### 回文数

> 4.回文数
>
> 判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。
>
> **示例 :**
>
> ```
> 输入: 121
> 输出: true
> 
> 输入: -121
> 输出: false
> 解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
> 示例 3:
> 
> 输入: 10
> 输出: false
> 解释: 从右向左读, 为 01 。因此它不是一个回文数。
> 
> ```

```java
class Solution {
    public boolean isPalindrome(int x) {
        //负数肯定不是回文数
        if(x < 0){
            return false;
        }
        //如果正数逆序和原来的相等则返回true
        int res = 0;
        int result = x;
        while(x != 0){
            res = res*10 + x%10;
            x=x/10;
        }
        return res == result;
    }
}
```

### 罗马数字转整数

>5.罗马数字转整数
>
>罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。
>
>字符          数值
>I             1
>V             5
>X             10
>L             50
>C             100
>D             500
>M             1000
>
>例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。
>
>通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：
>
>I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
>X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
>C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。
>给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。
>
>示例 1:
>
>输入: "III"
>输出: 3
>示例 2:
>
>输入: "IV"
>输出: 4
>示例 3:
>
>输入: "IX"
>输出: 9
>示例 4:
>
>输入: "LVIII"
>输出: 58
>解释: L = 50, V= 5, III = 3.
>示例 5:
>
>输入: "MCMXCIV"
>输出: 1994
>解释: M = 1000, CM = 900, XC = 90, IV = 4

```java
/**
     * 罗马数转int（1-3999）
     * 1,哈希表实现,罗列所有复杂的情况。
       2,遍历字符串，如果两个字符存在优先两个字符
     * 时间复杂度O(n)
     * @param roman
     * @return
     */
class Solution {
    public int romanToInt(String s) {
         //枚举所有异常情况
        Map<String,Integer> map = new HashMap<>(16);
        map.put("I",1);
        map.put("IV",4);
        map.put("V",5);
        map.put("IX",9);
        map.put("X",10);
        map.put("XL",40);
        map.put("L",50);
        map.put("XC",90);
        map.put("C",100);
        map.put("CD",400);
        map.put("D",500);
        map.put("CM",900);
        map.put("M",1000);
        int romanLength = s.length();
        int res = 0;
        //i的增量分情况实现
        for (int i = 0; i < romanLength;) {
            if(i+1<romanLength && map.containsKey(s.substring(i,i+2))){
                res+=map.get(s.substring(i,i+2));
                i+=2;
            }else{
                res+=map.get(s.substring(i,i+1));
                i++;
            }
        }
        return res;
    }
}
```

### 最长公共前缀

>6.最长公共前缀
>
>编写一个函数来查找字符串数组中的最长公共前缀。
>
>如果不存在公共前缀，返回空字符串 ""。
>
>示例 1:
>
>输入: ["flower","flow","flight"]
>输出: "fl"
>示例 2:
>
>输入: ["dog","racecar","car"]
>输出: ""
>解释: 输入不存在公共前缀。
>说明:
>
>所有输入只包含小写字母 a-z 。
>

```java
/**
     * 
       利用栈(先进后出的特性)来实现，每次遇到左边元素则压栈，遇到右边元素则从栈顶出
     * 需要一个Hash表来存储括号KV，K是右括号，V是左括号
     * 注意：""也是符合要求的。。。
     * 时间复杂度：O(m)
     * 空间复杂度：O(m)
     * @param s
     * @return
     */
    public static boolean isValidUseStack(String s) {
        Stack<Character> stack = new Stack<>();
        if(s.length() == 0){
            return true;
        }
        if(s.length()%2!=0){
            return false;
        }
        Map<Character,Character> map = new HashMap<>(16);
        map.put(']','[');
        map.put(')','(');
        map.put('}','{');
        for(int i = 0;i<s.length();i++){
            Character key = s.charAt(i);
            if(map.containsKey(key)){
                //pop栈顶元素
                char topEle = stack.empty() ? '#' : stack.pop();
                if(topEle != map.get(key)){
                    return false;
                }
            }else{
                stack.push(key);
            }
        }
        return stack.isEmpty();

    }
```

## Day 4

### 删除排序数组中的重复项

>7.删除排序数组中的重复项
>
>给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。
>
>不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。
>
>示例 1:
>
>给定数组 nums = [1,1,2], 
>
>函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 
>
>你不需要考虑数组中超出新长度后面的元素。
>示例 2:
>
>给定 nums = [0,0,1,1,1,2,2,3,3,4],
>
>函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。
>
>你不需要考虑数组中超出新长度后面的元素。
>说明:
>
>为什么返回数值是整数，但输出的答案是数组呢?
>
>请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。
>
>你可以想象内部操作如下:
>
>// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
>int len = removeDuplicates(nums);
>
>// 在函数里修改输入数组对于调用者是可见的。
>// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
>for (int i = 0; i < len; i++) {
>    print(nums[i]);
>}

```java
public class RemoveDuplicateSortdArray {
    public static void main(String[] args) {
        int[] nums = new int[]{0,0,1,2,3,3,4};
        int len = removeDuplicates(nums);
        for (int i = 0; i < len; i++) {
            System.out.println(nums[i]);
        }
    }
    /**
     * 快慢指针法
     * @param nums 已经排序的数组
     * @return
     * 0 1 1 2 3 3 4 i = 1;j = 2
     * 0 1 1 2 3 3 4 i = 2;j = 3
     * 0 1 2 3 3 3 4 i = 3;j = 4
     * 0 1 2 3 4 3 4 i = 4;j = 6
     *
     */
    public static int removeDuplicates(int[] nums) {
        if(0 == nums.length) return 0;
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if(nums[j] != nums[i]){
                i++;
                nums[i] = nums[j];
            }
        }
        return i+1;
    }
}
```

## Day 5

### 合并两个有序链表

>21.合并两个有序链表
>
>将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
>
>示例：
>
>输入：1->2->4, 1->3->4
>输出：1->1->2->3->4->4

```java 
/**
     * 采用递归的思想
     * 时间复杂度： O(n)
     * 空间复杂度： O(1)
     * @param l1
     * @param l2
     * @return
     */
    public static ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(null == l1){
            return l2;
        }
        if(null == l2){
            return l1;
        }
        if(l1.val < l2.val){
            l1.next = mergeTwoLists(l1.next,l2);
            return l1;
        }else{
            l2.next = mergeTwoLists(l1,l2.next);
            return l2;
        }
    }
```



### 移除元素

>27.移除元素
>
>给定一个数组 nums 和一个值 val，你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度。
>
>不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。
>
>元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。
>
>示例 1:
>
>给定 nums = [3,2,2,3], val = 3,
>
>函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。
>
>你不需要考虑数组中超出新长度后面的元素。
>示例 2:
>
>给定 nums = [0,1,2,2,3,0,4,2], val = 2,
>
>函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。
>
>注意这五个元素可为任意顺序。
>
>你不需要考虑数组中超出新长度后面的元素。
>
>说明:
>
>为什么返回数值是整数，但输出的答案是数组呢?
>
>请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。
>
>你可以想象内部操作如下:
>
>// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
>int len = removeElement(nums, val);
>
>// 在函数里修改输入数组对于调用者是可见的。
>// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
>for (int i = 0; i < len; i++) {
>    print(nums[i]);
>}

```java
/**
     * 快慢指针
     * 时间复杂度：O(n)
     * 空间复杂度:O(1)
     * @param nums
     * @param val
     * @return
     */
    public static int removeElement(int[] nums, int val){
        if(nums.length <= 0){
            return 0;
        }
        int j = 0;
        for (int i = 0; i < nums.length; i++) {
            if(nums[i] != val){
                nums[j] = nums[i];
                j++;
            }
        }
        return j;
    }
```

## Day 6

### 字符串找子串

>#### [28. 实现 strStr()](https://leetcode-cn.com/problems/implement-strstr/)
>
>实现 strStr() 函数。
>
>给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。
>
>说明:
>
>当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。
>
>对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。
>
>示例 1:
>
>```
>输入: haystack = "hello", needle = "ll"
>输出: 2
>```
>
>**示例 2:**
>
>```
>输入: haystack = "aaaaa", needle = "bba"
>输出: -1
>```

```java
public static int strStr(String haystack, String needle) {
        if(null == needle || needle.length() == 0){
            return 0;
        }
        return haystack.indexOf(needle);
    }
```

### 链表相加

>#### [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)
>
>给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。
>
>如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。
>
>您可以假设除了数字 0 之外，这两个数都不会以 0 开头。
>
>**示例：**
>
>```
>输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
>输出：7 -> 0 -> 8
>原因：342 + 465 = 807
>```

```java
public class AddTwoNumbers {
    /**
    public static void main(String[] args) {
        ListNode i0 = new ListNode(2);
        ListNode i1 = new ListNode(4);
        ListNode i2 = new ListNode(3);
        i0.next = i1;
        i1.next = i2;

        ListNode j0 = new ListNode(5);
        ListNode j1 = new ListNode(6);
        j0.next = j1;

        ListNode res = addTwoNumbers(i0, j0);
        while (null != res){
            System.out.println(res.val);
        }
    }
    **/

    static  class ListNode{
        int val;
        ListNode next;
        ListNode(int x) { val = x; }
    }

    /**
     * 前提：
     * 非空，非负，每个节点只能存储 一位 数字
     * @param l1
     * @param l2
     * @return
     */
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int carryVal = 0;
        ListNode res = new ListNode(0);
        ListNode cur = res;
        while(null != l1 || null != l2){
            int l1Val = null == l1 ? 0 : l1.val;
            int l2Val = null == l2 ? 0 : l2.val;
            int valSum = (l1Val + l2Val + carryVal) ;
            int val = valSum%10 ;
            carryVal = valSum/10;
            cur.next = new ListNode(val);
            cur = cur.next;
            if(null != l1){
                l1 = l1.next;
            }
            if(null != l2){
                l2 = l2.next;
            }
        }
        if(carryVal >= 1){
            cur.next = new ListNode(carryVal);
        }
        return res.next;
    }
}
```


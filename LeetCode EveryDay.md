# LeetCode EveryDay

## 基础排序算法

### 1，快速排序-分治

> 思路
>
> - 确定分界点：q[left],q[right],q[(left+right)/2]
> - 调整区间 小于x的在左边，大于x的在右边（<font color=red>重点<font>）
> - 递归处理左右两边排序



## Day one

认识时间复杂度

## 时间复杂度



> 两数之和（2019.09）
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



## Day Two

>国庆旅行
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

>整数反转
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

## Day Three

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


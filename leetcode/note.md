# array
在C++中二维数组是连续分布的,地址是连续一条线的
Java是没有指针的，同时也不对程序员暴露其元素的地址，寻址操作完全交给虚拟机.
![4 AVMZHZ`HW9ZVF6LG_~J H](https://user-images.githubusercontent.com/57675566/155604361-57caa792-f3b0-44a9-bf7c-25aea57267c7.png)
## binary search
1.前提条件
- 数组是有序数组，数组中无重复元素  ascending order 升序排列
- 边界条件不变，区间就是不变量，关于left right和middle的关系，一般定义两种：[left, right]，[left, right)
-  write an algorithm with O(log n) runtime complexity. 时间复杂度暗示，空间复杂度是O（1）

2.1 二分法第一种写法
定义 target 是在一个在左闭右闭的区间里，也就是[left, right]。
while判断要left=right加上，因为根据设置可以实现
```Java
class Solution {
    public int search(int[] nums, int target) {
        // 避免当 target 小于nums[0] nums[nums.length - 1]时多次循环运算
        if (target < nums[0] || target > nums[nums.length - 1]) {
            return -1;
        }
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + ((right - left) >> 1);
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] < target)
                left = mid + 1;
            else if (nums[mid] > target)
                right = mid - 1; 右边是有效空间，再次循环的时候到的了，所以要-1
        }
        return -1;
    }
}
```
2.2 二分法第二种写法
target 【left。right）里
left不可能等于right，因为区间上没有包括右边
```Java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length; // 因为这里范围不包括右边
        while (left < right) { //因为left == right的时候，在[left, right)是无效的空间，所以使用 <
            int mid = left + ((right - left) >> 1);
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] < target)
                left = mid + 1;// target 在右区间，在[middle + 1, right)中
            else if (nums[mid] > target)
                right = mid; //target 在左区间，在[left, middle)中 右边是无效空间，所以可以不用-1，因为到不了
        }
        return -1;
    }
}
```
### question note
**35. Search Insert Position**
>Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
>You must write an algorithm with O(log n) runtime complexity.
可以分成4种情况，但是1，3,4 的return是可以合并的。再写之前用例子画一下
1. target在数组所有值之前 left=right那个循环，right 再-1. 变成 【0，-1】。 所以再while循环外return right+1
2. 目标值是数组中的某个 在while loop中的判断之后，return middle
3. target在数组所有值之后 return right+1
4. 目标值插入数组的某位置return right+1

**69.Sqrt(x)**
>Given a non-negative integer x, compute and return the square root of x.
>Since the return type is an integer, the decimal digits are **truncated(截断)**, and only **the integer part** of the result is returned.
>Note: You are not allowed to use any built-in exponent function or operator, such as pow(x, 0.5) or x ** 0.5.

**367. Valid Perfect Square**
>Given a positive integer num, write a function which returns True if num is a perfect square else False.
>Follow up: Do not use any built-in library function such as sqrt

这两题非常相似，用mid与给出的target number -num进行比较，注意如果要用mid* mid与num比较，要讲使用long变量，不然会overflow，如果用int，那么为了防止overflow，mid=left+（right-left）/2
同时 比较为 mid> or < target/mid 。 

## remove elements
1.条件
- 一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。
- 不要使用额外的数组空间，你必须仅使用 $O(1)$ 额外空间并原地修改输入数组
- **must do this in-place** --就是只能再这个结构里面改，空间复杂度不能增加

2.1 暴力搜索,使用两个for loop， 时间复杂度：O(n^2), 空间复杂度：O(1)
```Java
 int removeElement(vector<int>& nums, int val) {
        int size = nums.size();
        for (int i = 0; i < size; i++) {
            if (nums[i] == val) { // 发现需要移除的元素，就将数组集体向前移动一位
                for (int j = i + 1; j < size; j++) {
                    nums[j - 1] = nums[j];
                }
                i--; // 因为下标i以后的数值都向前移动了一位，所以i也向前移动一位
                size--; // 此时数组的大小-1
            }
        }
        return size;
```
2.2 双指针法 ： 通过一个快指针和慢指针在一个for循环下完成两个for循环的工作 时间复杂度：O(n) 空间复杂度：O(1)
```Java
class Solution {
    public int removeElement(int[] nums, int val) {

        // 快慢指针
        int fastIndex = 0;
        int slowIndex;
        for (slowIndex = 0; fastIndex < nums.length; fastIndex++) {
            if (nums[fastIndex] != val) {
                nums[slowIndex] = nums[fastIndex];
                slowIndex++;
            }
        }
        return slowIndex;

    }
}
```
2.3 滑动窗口（sliding window） （207）


### question note
26. Remove Duplicates from Sorted Array
>keep two pointers i and j, where i is the slow-runner while j is the fast-runner. As long as nums[i] = nums[j], we increment j to skip the duplicate.
>When we encounter nums[j] not equal nums[i], the duplicate run has ended so we must copy its value to nums[i+1]. ii is then incremented

283. Move Zeroes
>Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
>Note that you must do this in-place without making a copy of the array.
将题目转换成发现0就移除，再返回非0的最后一个数字的index，再在剩下的array里填满0

844. Backspace String Compare
>Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.
>Note that after backspacing an empty text, the text will continue empty.
>eg: ab## c#d# return: true
双指针法：
时间复杂度O（n+m）空间复杂度O（1）
**从后向前遍历string s 和 t，记录#的数量，如果#数量抵消至0，就开始比较s[i]==t[j] return true or not**
主要逻辑：
1. while大循环 i>=0||j>=0 。 i是string s的长度， j是string t的长度
2. while小循环，是关于string s的。
- 从后向前，当前为 #， nums+1
- 当前不为#, nums不为0， nums-1
- 当前不为#,nums 为0， break， 与t[j]比较
3. 关于string t的while循环，同理
4. 根据得到的阶段性的i，j进行判断， 在i和j都大于等于0的情况下如果s[i]不等于t[j]， return false
5. 如果i，j只有一个大于等于0， 也是false
6. **别忘了i和j每个循环的--**
7. 跳出大循环，return true

977.Squares of a Sorted Array
>Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.
>Input: nums = [-4,-1,0,3,10]
>Output: [0,1,9,16,100]
>Explanation: After squaring, the array becomes [16,1,0,9,100].
>After sorting, it becomes [0,1,9,16,100].
**最关键的点在于思考非倒序数列的意义--原数组中的元素平方最大值一定产生在原数组的最左边或者最右边。**
所以用双指针法：
定义一个新数组result，和A数组一样的大小，让k指向result数组终止位置。
定义左右指针 left 和right
**在left<=right的前提下**：
if(Math.abs(nums[left])>Math.abs(nums[right]) 将左边的放入 result最后一位
else，右边的放入result最后一位

209：Minimum Size Subarray Sum
>Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the >sum is greater than or equal to target. If there is no such subarray, return 0 instead.
>Input: target = 7, nums = [2,3,1,2,4,3]
>Output: 2
>Explanation: The subarray [4,3] has the minimal length under the problem constraint
**这里储存子数列最小长度的变量result要开始设置为Integer_max**



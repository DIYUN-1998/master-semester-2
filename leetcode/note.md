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
```Java
```
**367. Valid Perfect Square**
>Given a positive integer num, write a function which returns True if num is a perfect square else False.
>Follow up: Do not use any built-in library function such as sqrt

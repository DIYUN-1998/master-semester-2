# userful tips， from ：https://seanprashad.com/leetcode-patterns/

>If input array is sorted then
- Binary search
- Two pointers
>If asked for all permutations/subsets then
- Backtracking

>If given a tree then
- DFS
- BFS

>If given a graph then
- DFS
- BFS

>If given a linked list then
- Two pointers

>If recursion is banned then
- Stack

>If must solve in-place then
- Swap corresponding values
- Store one or more different values in the same pointer

>If asked for maximum/minimum subarray/subset/options then
- Dynamic programming

>If asked for top/least K items then
- Heap

>If asked for common strings then
- Map
- Trie

>Else
- Map/Set for O(1) time & O(n) space
- Sort input for O(nlogn) time and O(1) space

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
不断的调节子序列的起始位置和终止位置，从而得出我们要想的结果
主要确定以下三点：
- 窗口内内容
- 如何移动窗口起始位置
- 如何移动窗口结束位置
**窗口位置如何移动**
子序列长度为（right-left+1）
result一开始是设置的Integermax或者Integermin，与子序列长度比较，可以用三元运算符，也可以用内置函数Math.min()
记得比较完之后变更子序列的起始位置

2.4 螺旋矩阵（lc 59）
给定一个正整数 n，生成一个包含 1 到 $n^2$ 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。
示例:
输入: 3 输出: [ [ 1, 2, 3 ], [ 8, 9, 4 ], [ 7, 6, 5 ] ]


**重点在于用算法模拟整个过程**
画每四条边，这四条边怎么画，**每画一条边都要坚持一致的左闭右开，或者左开又闭的原则**，这样这一圈才能按照统一的规则画下来
拐角处让给新的一条边来继续画。这也是坚持了每条边左闭右开的原则。


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
there are two method:
1. brute force method:
- two loop, the outter loop is i loop , i is the left side of pointer
- **sum=0;** remember to write it ,cause when we find a sublength >=target, we break the j loop and put the sub in result to find another sublength ,to compare if there is a sublength smaller than previous.
```Java
for(int i=0;i<nums.length;i++){
            sum=0;
            for(int j=i;j<nums.length;j++){
                sum+=nums[j];
                if(sum>=target){
                    sublength=j-i+1;
                    result=result<sublength? result:sublength;
                    break;
                }
            }
        }
     **   return result==Integer.MAX_VALUE? 0: result;**
```
- dont forget if the result is as original value, reuturn 0
2. sliding window
-only the right pointer j has for loop, when finding a potential sublength, compare and left pointer ++
```Java
for(int j=0;j<nums.length;j++){
            sum+=nums[j];
            while(sum>=target){
                sub=j-i+1;
                result= result<sub? result:sub;
                sum-=nums[i++];
            }
        }
        return result==Integer.MAX_VALUE? 0:result;
```

167 Two Sum II - Input Array Is Sorted
>Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.
>Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.
>The tests are generated such that there is exactly one solution. You may not use the same element twice.
>Your solution must use only constant extra space.
**从缩减搜索空间的角度思考**
如果用暴力解法求解，一次只检查一个单元格，那么时间复杂度一定是 O(n^2)。要想得到 O(n)的解法，我们就需要能够一次排除多个单元格.
**双指针从两端往中间缩减，而不是一个快一个慢**
**比如数组长度为8， 计算 A[0] + A[7] ，与 target 进行比较。如果不相等的话，则要么大于 target，要么小于 target
假设此时 A[0] + A[7] 小于 target。这时候，我们应该去找和更大的两个数。由于 A[7] 已经是最大的数了，其他的数跟 A[0] 相加，和只会更小。也就是说 A[0] + A[6] 、A[0] + A[5]、……、A[0] + A[1] 也都小于 target，这些都是不合要求的解，可以一次排除**

557. 反转字符串中的单词 III
>给定一个字符串 s ，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。
>输入：s = "Let's take LeetCode contest"
>输出："s'teL ekat edoCteeL tsetnoc"
1.写一个将char数组里的字符反转的方法，用双指针
2.将string 转成char array。只需要关注空格和最后 array的最后一位就行（因为最后一个单词后无空格）
3.写一个循环，如果到空格位，那么start到空格位-1这些字符反转，然后**更新start，新的起始点是start=i+1**。
4.如果是最后一个单词，就是index=s.length-1，引入反转函数。
5.最后 ** return new String(array);**

904. Fruit Into Baskets


# linkedlist
## 种类
链接的入口节点称为链表的头结点也就是head。
1.单链表
![1646334573(1)](https://user-images.githubusercontent.com/57675566/156635311-f2b14d9e-d9d9-4b5c-9e4c-968f1c28f7d9.png)
2.双链表
双链表：每一个节点有两个指针域，一个指向下一个节点，一个指向上一个节点。
**双链表 既可以向前查询也可以向后查询。**
![1646334625(1)](https://user-images.githubusercontent.com/57675566/156635432-f26ebb3b-20db-428a-b109-1606006484b2.png)

3.循环链表
![1646334657(1)](https://user-images.githubusercontent.com/57675566/156635494-f9cf5028-944e-476a-b891-0baa9977c0cd.png)

## 存储方式
链表在内存中可不是连续分布的。
链表是通**过指针域的指针链接在内存中各个节点**。
所以链表中的节点在内存中不是连续分布的 ，而是散乱分布在内存中的某地址上，分配机制取决于操作系统的内存管理。
Java中，删除一个节点就是原来指向这个节点的直接指向这个节点之后一位，因为java的内存回收机制，所以不用自己手动释放内存
**删除第五个节点，需要从头节点查找到第四个节点通过next指针进行删除操作，查找的时间复杂度是$O(n)$**
##与array 对比
数组：O(n)-插入，删除时间复杂度 O(1) 查询时间复杂度 **适用数据量固定，频繁查询，较少增删**
链表  O(1)-.................. O(N) ..............**数据量不固定，频繁增删，较少查询**

## 链表的定义（白板code时候要用）
```Java
public class ListNode {
    // 结点的值
    int val;

    // 下一个结点
    ListNode next;

    // 节点的构造函数(无参)
    public ListNode() {
    }

    // 节点的构造函数(有一个参数)
    public ListNode(int val) {
        this.val = val;
    }

    // 节点的构造函数(有两个参数)
    public ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}

双向链表：
class ListNode {
    int val;
    ListNode next,prev;
    ListNode(int val){
    this.val=val;
}
```
### 解决问题的时候一处理头节点有两个方法：
1. 在头节点之前创造一个虚拟节点用那个节点做头：
ListNode dummy =new ListNode (-1, head);
这样，head就是dummy.next **注意最后return 的时候要return head ！！**
这样的话一开始只需要判断head是不是为null就行，判断完了再造虚拟节点

2. 不创建虚拟dummy，仍然用现在的head。但是如果要删除的node在头部的话在solution一开始要有一个额外操作
```Java
  while (head != null && head.val == val) {
        head = head.next;
    }
    // 已经为null，提前退出
    if (head == null) {
        return head;
    }
```
注意那里是while不是if，因为会有比如 在链表 【7,7,7,7】里删除value为7 的值得问题。这里就要全删，一个if是不能完成的。

**707Design Linked List**
设计题，重点注意，可以设计单向也可以双向
1.单向链表
在写初始化链表前，先定义size和head（sentinel node）
public MyLinkedList() {}： 初始化链表，给size和head赋值
public int get(int index) {}获取第index节点的值，注意index里的第一位给了虚拟头结点，所以for循环查找第index+1位
public void addAtHead(int val) {}
public void addAtTail(int val) {} 这两个一样，用addAtIndex就可以，注意赋值
public void addAtIndex(int index, int val) {} 先把不成立的情况去掉，index>size 和index<0
然后找到要插入节点的前节点，然后插入
public void deleteAtIndex(int index){}同样，但是要比上一个简单，只要找到删除节点的前节点，然后让前节点的next=前节点的next.next就行

2.双向链表

206. Reverse Linked List
>Given the head of a singly linked list, reverse the list, and return the reversed list.
>Input: head = [1,2,3,4,5]  Output: [5,4,3,2,1]
1. 双指针：在head前再建一个value是null的空指针，然后初始pre指针就是这个虚拟节点，初始cur指针就是第一个node，然后让每个node的next指向前一个
2. 注意再让指向前一个之前，要建一个listnode来保存初始的next指向
也可以用递归，就是
```Java
class Solution {
    public ListNode reverseList(ListNode head) {
        return reverse(null, head);
    }

    private ListNode reverse(ListNode prev, ListNode cur) {
        if (cur == null) {
            return prev;
        }
        ListNode temp = null;
        temp = cur.next;// 先保存下一个节点
        cur.next = prev;// 反转
        // 更新prev、cur位置
        // prev = cur;
        // cur = temp;
        return reverse(cur, temp); 注意给递归方法的赋值，相当于双指针的后两步
    }
}
```
24.Swap Nodes in Pairs
>Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)
>Input: head = [1,2,3,4]  Output: [2,1,4,3]
**无论哪种方法都要创造dummy node。做prev**
1. 非递归写法
这里的dummy node 和head, head.next初始分别是 nullor0,1,2.
要保证head 和head.next都不是null，不然一个没有或者只有一个都不能反转，只能直接return head
在while循环里
![1646751832(1)](https://user-images.githubusercontent.com/57675566/157264864-55a46c90-1756-4cbf-bdad-fc5b81bc2e99.png)
```Java
  ListNode temp = head.next.next; // 缓存 next
      prev.next = head.next;          // 将 prev 的 next 改为 head 的 next
      head.next.next = head;          // 将 head.next(prev.next) 的next，指向 head
      head.next = temp;               // 将head 的 next 接上缓存的temp
      prev = head;                    // 步进1位
      head = head.next;               // 步进1位
```
2.递归方法
思考三点
- 返回值：这里要的是反转完成后的子链的头。比如2，4
- 调用单元做了什么：设需要交换的两个点为 head 和 next，head 连接后面交换完成的子链表，next 连接 head，完成交换
- 停止递归的条件：如上，当有head或者head.next为null的时候没有两个值无法反转
```Java
 if(head == null || head.next == null){
            return head;
        }
        ListNode next = head.next;
        head.next = swapPairs(next.next);
        next.next = head;
        return next;
or
 if (head == null || head.next == null)  
            return head;
        ListNode rest = head.next.next;
        ListNode newHead = head.next;
        newHead.next = head;
        head.next = swapPairs(rest);
        return newHead;
```


















# 算法之路

### 生活中的算法应用
区块链  是主线 一个链表，每个节点指针指向前一个节点，每个节点里是一个二叉树（二叉树里存的是hash值）


### 常用算法 时间复杂度 主定律  
- 二叉树查找  O(log n) 

- 二叉树遍历  O(n)

- 两维数组查找  O(n)  一维数组查找 O(log n)

- 排序 如：快排、归并排序  O(nlogn)


### 切题四件套

- Clarification(理清题目)

- Possible solutions（多想几种解法）
  比较时间、空间复杂度
  
- Coding（多写）

- Test Code（测试案例）

### 数组
数组内存地址是连续的
数组查找  时间复杂度O(1)

插入、删除  平均时间复杂度 O(n) 最好情况O(1) 最坏情况O(n)

### 链表(Linked List)
单链表、双链表

链表查找  需要从头结点开始往后找 时间复杂度为O(n)

插入、删除  只需要把前一个节点next指针指向它、它的next指针指向后面节点，时间复杂度为O(1)


应用场景：一、插入删除操作比较多  二、不知道有多少个元素，每新增一个就添加在后面

[反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)


[交换节点-24. Swap Nodes in Pairs](https://leetcode-cn.com/problems/swap-nodes-in-pairs/submissions/)

[判断链表是否有环-141. Linked List Cycle](https://leetcode-cn.com/problems/linked-list-cycle/submissions/)

### 堆栈(stack) 和 队列(Queue)


[数据流中第K大元素-703. Kth Largest Element in a Stream](https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/submissions/)

### Map 和 Set 


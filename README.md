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

## 数据结构

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



## 算法

### 深度优先搜索(DFS)和广度优先搜索(BFS)

DFS 代码模板

递归写法
```
visited = set() 

def dfs(node, visited):
if node in visited: # terminator
	# already visited 
	return 

	visited.add(node) 

	# process current node here. 
	...
	for next_node in node.children(): 
		if not next_node in visited: 
			dfs(next_node, visited)

```

非递归写法

```
def DFS(self, tree): 

	if tree.root is None: 
		return [] 

	visited, stack = [], [tree.root]

	while stack: 
		node = stack.pop() 
		visited.add(node)

		process (node) 
		nodes = generate_related_nodes(node) 
		stack.push(nodes) 

	# other processing work 
	...

```

BFS 代码

```
def BFS(graph, start, end):

	queue = [] 
	queue.append([start]) 
	visited.add(start)

	while queue: 
		node = queue.pop() 
		visited.add(node)

		process(node) 
		nodes = generate_related_nodes(node) 
		queue.push(nodes)

	# other processing work 
	...

```

### 剪枝
就是减掉淘汰、次优分支，是一种思想
使用场景：状态树比较复杂的，比如：国际象棋、斐波拉契数列、各种棋等

### 双向BFS
一个从头开始，一个从后面开始

```
//双向BFS 模板 
//思想：从头和尾都往中间走
var ladderLength = function(beginWord, endWord, wordList) {
    //判断边界条件
    let wordListSet = new Set(wordList);
    if(!wordListSet.has(endWord)){
        return 0;
    }
    //相比单向BFS中使用的Queue 使用set具有判重的特点
    //创建头set
    let beginSet = new Set();
    beginSet.add(beginWord);
    //创建尾set
    let endSet = new Set();
    endSet.add(endWord);
    //设置级别
    let level = 1;
    //只要头部的set大于0
    while (beginSet.size > 0) {
        //临时变量
        let next_beginSet = new Set();
        //遍历
        for(let key of beginSet){
            for(let i = 0;i < key.length;i++){
                for(let j = 0;j < 26;j++){
                   let s =  String.fromCharCode(97+j);
		   //不相等时 处理
                   if(s != key[i]){
                        let new_word = key.slice(0,i)+s+key.slice(i+1);
                        if(endSet.has(new_word)){
                            return level + 1;
                        }
                        if(wordListSet.has(new_word)){
                            next_beginSet.add(new_word);
                            wordListSet.delete(new_word);
                        }
                   }
                }
            }
        }
        beginSet = next_beginSet;
        level++;
	
        //头部分大于尾时，交换头尾部分
	//这样都只要计算beginSet就好了
        if(beginSet.size > endSet.size){
            [beginSet,endSet] = [endSet,beginSet]
        }
    }
    return 0;

};
```

### 启发式搜索
将BFS的queue替换成优先队列Priority Queue，带有智能


### AVL树、红黑树
##### AVL树
{-1,0,1}

左旋、右旋、左右旋、右左旋

特点：
严格平衡二叉树

##### 红黑树
不多于两倍
红黑为节点

使用场景：多读，少写就用AVL树，比如微博那些
读写都多，那就用红黑树





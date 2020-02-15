# 算法之路

### 生活中的算法应用
区块链  是主线 一个链表，每个节点指针指向前一个节点，每个节点里是一个二叉树（二叉树里存的是hash值）


### 常用算法 时间复杂度 主定律  
- 二叉树查找  O(log n) 

- 二叉树遍历  O(n)

- 两维数组查找  O(n)  一维数组查找 O(log n)

- 排序 如：快排、归并排序  O(nlogn)


### 切题

- Clarification(理清题目)

- Possible solutions（多想几种解法）
  比较时间、空间复杂度
  
- Coding（多写）

- Test Code（测试案例）

### 刷题

- 第一遍<br>
  1. 读题思考 5分钟
  2. 直接看解法:
  3. 背诵和默写

- 第二遍
马上自己写
多种解法比较、体会，重点是执行时间 领先80%以上人

- 第三遍
过了一天后，再重复做题
不同解法的熟练程度，专项练习

- 第四遍
过了一周之后反复练习

- 第五遍
面试前一周恢复性练习


## 数据结构 & 算法

#### [数据结构脑图](https://naotu.baidu.com/file/b832f043e2ead159d584cca4efb19703?token=7a6a56eb2630548c)

#### [算法脑图](https://naotu.baidu.com/file/0a53d3a5343bd86375f348b2831d3610?token=5ab1de1c90d5f3ec)

#### [数组、链表、跳表](https://github.com/Jackzigen/LeetCode/blob/master/数组、链表、跳表.md)

#### [堆栈(stack) 、队列(Queue)、Map 、Set](https://github.com/Jackzigen/LeetCode/blob/master/栈、队列、哈希表.md)

#### [二叉树、递归](https://github.com/Jackzigen/LeetCode/blob/master/二叉树、递归.md)

#### [分治、回溯、DFS、BFS](https://github.com/Jackzigen/LeetCode/blob/master/分治、回溯、DFS、BFS.md)

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

### [动态规划](https://github.com/Jackzigen/LeetCode/blob/master/动态规划.md)

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
#### AVL树
AVL树是一个平衡二叉搜索树
平衡因子--左子树高度减去右子树高度（有时候相反）
balance factor = {-1,0,1}

平衡的操作
左旋、右旋、左右旋、右左旋

不足点：
结点需要存储额外信息（-1，0，1），
调整次数频繁，比如：插入一个结点，就要动很多

#### 红黑树
红黑树是一种近似平衡的二叉搜索树，它能确保**左右子树的高度差小于两倍**
特点：
- 结点要么是红要么是黑
- 根结点是黑的
- 每个叶子结点（NIL结点，空结点）是黑色的
- 不能有相邻的两个红色结点
- 从任一结点的到其叶子结点的路径都包含相同数目的黑色结点

使用场景：多读，少写就用AVL树，比如微博那些
读写都多，那就用红黑树

### 位运算

**异或**
相同为 0，不同为 1。也可用“不进位加法”来理解。 
异或操作的一些特点:
x ^ 0 =x
x ^ 1s = ~x // 注意 1s = ~0
x ^ (~x) = 1s
x ^ x= 0
c = a ^ b => a ^ c = b, b ^ c = a a ^ b ^ c = a ^ (b ^ c) = (a ^ b) ^ c
// 交换两个数 // associative

使用场景
判断奇偶:
x % 2 == 1 —> (x & 1) == 1 x % 2 == 0 —> (x & 1) == 0

x >> 1 —> x / 2
即: x = x / 2; —> x = x >> 1;

mid = (left + right) / 2; —> X = X & (X-1) 清零最低位的 1

X & -X => 得到最低位的 1

X & ~X => 0



### 布隆过滤器
哈希表HashTable+拉链法存储重复元素

Bloom Filter vs Hash Table
一个很长的二进制向量和一系列随机映射函数。布隆过滤器可以用于检索一个元素是否在一个集合中。
bloom filter只存储在或者不在，hashTable还可以存储格外的详细信息（如：值）。

优点是空间效率和查询时间都远远超过一般的算法，缺点是有一定的误识别率和删除困难。

**布隆过滤器的使用场景**
在访问后台数据库时，先使用布隆过滤器查询判断在不在，再进行下一步DB具体查询

### Cache缓存
LRU Cache 最近最少使用
哈希表+双向链表 实现，O(1)查询、修改、更新

### 排序
手写快排
```
function quickSort(array, left, right) {
    //边界条件
     if(right <= left) return;
    //
     var partitionIndex = partition(array, left, right);
     //对标杆两侧进行快排
     quickSort(array, left, partitionIndex - 1);
     quickSort(array, partitionIndex + 1, right);
}

//分隔值
function partition(array, left, right) {
    //partitionIndex 小于pivot的元素个数  pivot 标杆位置
    var partitionIndex = left, pivot = right;
    for(let i = left; i < right; i++) {
        //小于标杆的，都放到左边
        if(array[i] < array[pivot]) {
            swap(array, i, partitionIndex);
            partitionIndex ++;
        }
    }
    //一开始标杆的位置在最右边，现在调它到合适的位置
    swap(array, pivot, partitionIndex);
    return partitionIndex;
}

//交换两个元素
function swap(array, i, j) {
    var temp = array[i];
    array[i] = array[j];
    array[j] = temp;
}
```






### 题目

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？



网格中的障碍物和空位置分别用 1 和 0 来表示。

说明：m 和 n 的值均不超过 100。

示例 1:

输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右

链接：https://leetcode-cn.com/problems/unique-paths-ii



### high起来
**动态规划**<br/>
```
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    //行
    let n = obstacleGrid.length;
    //列
    let m = obstacleGrid[0].length;
    //创建二维数组
    let dp = new Array(n);
    for(let i = 0; i < n; i++) {
        dp[i] = new Array(m).fill(0);
    }
    //处理边界
    dp[0][0] = obstacleGrid[0][0] == 0 ? 1 : 0;
    
    if(dp[0][0] == 0) {
        return 0;
    }

    //行
    //i从1开始
    for(let i = 1; i < m; i++) {
        if(obstacleGrid[0][i] != 1) {
             dp[0][i] = dp[0][i-1];
        }
    }
    //列
    //j从1开始
    for(let j = 1; j < n; j++) {
        if(obstacleGrid[j][0] != 1) {
             dp[j][0] = dp[j-1][0];
        }
    }

    //从1开始
    for(let i = 1; i < n; i++) {
        for(let j = 1; j < m; j++) {
            if(obstacleGrid[i][j] != 1){
              dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
    }
     
    return dp[n-1][m-1];
};
```

**动态规划+降维优化**<br/>
```
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    var n = obstacleGrid.length;
    var m = obstacleGrid[0].length;
    var dp = Array(m).fill(0);
    dp[0] = 1;
    for(let i = 0;i < n;i++){
        for(let j = 0;j < m;j++){
            if(obstacleGrid[i][j] == 1){
                dp[j] = 0;
            }else if(j > 0){
                dp[j] += dp[j-1];
            }
        }
    }
    return dp[m-1];
};

```

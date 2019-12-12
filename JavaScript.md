## JavaScript的一些常见操作

- 创建数组<br/>

1.一位数组
```
//大小为n的空数组
var cur = new Array(n);
//值全为1
var cur = new Array(n).fill(1);
```

2.二维数组
```
var dp = new Array(n);
for(var i = 0;i<n;i++){
    dp[i] = new Array(m);
    dp[i][0] = 1;
}
```

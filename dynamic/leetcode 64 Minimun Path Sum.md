## 64  Minimun Path Sum

Given a *m* x *n* grid filled with non-negative numbers, find a path from top left to bottom right which *minimizes* the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example:**

```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```



### solution

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        int[][] minPath = new int[row][col];//记录到达每个节点需要走的最短路径
        minPath[0][0] = grid[0][0];
        for(int i = 1; i < row; i++ ){
            minPath[i][0] = grid[i][0]+ minPath[i-1][0];
        }
        for(int j = 1;j < col ;j++){
            minPath[0][j] = grid[0][j]+minPath[0][j-1];
        }
        for(int i = 1; i < row ;i++){
            for(int j= 1; j < col ;j++){
                minPath[i][j] = Math.min(minPath[i-1][j],minPath[i][j-1]) + grid[i][j];//到达节点的方式只有从上或者从左边到达，更新到达节点的最小路径
            }
        }
        
        return minPath[row-1][col-1];
        
    }
}
```


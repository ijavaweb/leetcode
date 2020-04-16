---
categories: leetcode
tags: leetcode
---



## 152 Maximum Product Subarray

* **description**

  Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

  **Example 1:**

  ```
  Input: [2,3,-2,4]
  Output: 6
  Explanation: [2,3] has the largest product 6.
  ```

  **Example 2:**

  ```
  Input: [-2,0,-1]
  Output: 0
  Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
  ```

* **solution 1** 

  ```java
  //使用动态规划
  class Solution {
      public int maxProduct(int[] nums) {
          int l = nums.length;
          int[][] dp = new int[l][2];
          int result = nums[0];
          dp[0][0] = nums[0];
          dp[0][1] = nums[0];
          for(int i = 1; i < l; i++){
              if(nums[i] >= 0){
                  dp[i][0] = Math.max(dp[i-1][0]*nums[i],nums[i]);
                  dp[i][1] = Math.min(dp[i-1][1]*nums[i],nums[i]);
              }else{
                  dp[i][0] =Math.max(dp[i-1][1]*nums[i],nums[i]) ;
                  dp[i][1] = Math.min(dp[i-1][0]*nums[i],nums[i]);
              }   
          }
          for(int i = 0; i < dp.length;i++){
              if(result< dp[i][0]){
                  result = dp[i][0];
              }
          }
          return result;
      }
  } 
  ```

  

* **solution2**

  ```java
  //使用简单循环
  class Solution {
      public int maxProduct(int[] nums) {
          if(nums.length == 1){
              return nums[0];
          }
          int min = 0;
          int max = 0;
          int globalMax = 0;
          
          for(int num:nums){
              int prevMin = min*num;
              int prevMax = max*num;
              min = Math.min(num, Math.min(prevMin, prevMax));
              max = Math.max(num, Math.max(prevMin, prevMax));
              globalMax = Math.max(globalMax, max);
          }
          return globalMax;
      }
  } 
  ```

  
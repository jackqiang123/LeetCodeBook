# Leetcode5

This can be solved by dynamic programming.
In my view, the issue of find optimal solution (e.g., the max or the min), we will use dynamic programming mostly. Other method like greedy can also appear sometimes.

An important observation of this DP is when system transition equations are 
dp[i][j] = f(dp[k][l]), where i < k < l < j,
we will do loop by i from the end and back to the head; while j from i and forward to the end. Otherwise, we fail to do the right order computation and thus wrong result.

```
// Given a string S, find the longest palindromic substring in S.
// You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.
//

public class Solution {
    public String longestPalindrome(String s) {
      int len = s.length();
      int left = 0;
      int right = 0;
      if (len <= 1) return s;
      int res = 1;
      boolean [][] dp = new boolean[len][len];
      for (int i = len - 1; i >= 0; i--){
        for (int j = i; j < len; j++){
          if (i == j) dp[i][j] = true;
          else dp[i][j] = i + 1 <= j -1 ? (dp[i+1][j-1] && s.charAt(i) == s.charAt(j)) : s.charAt(i) == s.charAt(j);
          if (dp[i][j]) {
              if (res < j - i + 1)
              {
                  res = Math.max(res, j - i + 1);
                  left = i;
                  right = j;
              }
          }
        }
      }
      return s.substring(left, right + 1);
    }
}

```
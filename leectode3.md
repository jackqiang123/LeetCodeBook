# Leetcode3

Method 1: use an array to mark the last position that each char appears. When we find one char that already appears in the valid range, we will forward left pointer to last position PLUS one.

Method 2: the method above is at some risk of bug. Like I missed PLUS one. An easier way is to forward left pointer step by step until we meet that char to go over it. This idea can be used in later find max sub-string with k distinct String.

```
// Given a string, find the length of the longest substring without repeating characters.
//
// Examples:
//
// Given "abcabcbb", the answer is "abc", which the length is 3.
//
// Given "bbbbb", the answer is "b", with the length of 1.
//
// Given "pwwkew", the answer is "wke", with the length of 3.
// Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
        if (s.length() == 1) return 1;
        int res = 1;
        int []lasttime = new int[256];
        for (int i = 0; i < lasttime.length; i++)
          lasttime[i] = -1;
        int i = 0; int j = 0;
        while(j < s.length())
        {
          if (lasttime[s.charAt(j)] < i){
            res = Math.max(res, j - i + 1);
            lasttime[s.charAt(j)] = j;
            j++;
          }
          else{
            i = lasttime[s.charAt(j)] + 1; 
            lasttime[s.charAt(j)] = j;
            j++;
          }
        }
        return res;
    }
}
```
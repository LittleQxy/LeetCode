## LeetCode 5.19 每日打卡 + 每日三题

### LeetCode 680：验证回文字符串II

#### 题目

[https://leetcode-cn.com/problems/valid-palindrome-ii/](https://leetcode-cn.com/problems/valid-palindrome-ii/)

给定一个非空字符串 `s`，**最多**删除一个字符。判断是否能成为回文字符串。

#### 思路

双指针判断

#### 代码

```java
class Solution {
    public boolean validPalindrome(String s) {
        int i = 0,j = s.length()-1;
        while(i < j){
            if(s.charAt(i) != s.charAt(j)){
                return help(s,i,j-1) || help(s,i+1,j);
            }
            i++;
            j--;
        }
        return true;
    }

    public boolean help(String s,int i,int j){
        while(i < j){
            if(s.charAt(i) != s.charAt(j))
                return false;
            i++;
            j--;
        }
        return true;
    }
}
```



### LeetCode 9：回文数

#### 题目

[https://leetcode-cn.com/problems/palindrome-number/submissions/](https://leetcode-cn.com/problems/palindrome-number/submissions/)

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

#### 思路

首先负数直接返回false，之后将数字倒转判断是否相同

#### 代码

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0)
            return false;
        
        int cmp = 0;
        int tmp = x;
        while(tmp > 0){
            cmp = cmp*10+tmp%10;
            tmp = tmp/10; 
        }
        return cmp == x;
    }
}
```

### LeetCode 5 ：最长回文子串

#### 题目

[https://leetcode-cn.com/problems/longest-palindromic-substring/](https://leetcode-cn.com/problems/longest-palindromic-substring/)

给定一个字符串 `s`，找到 `s` 中最长的回文子串。你可以假设 `s` 的最大长度为 1000。

#### 思路

马拉车算法，[https://zhuanlan.zhihu.com/p/70532099](https://zhuanlan.zhihu.com/p/70532099)

#### 代码

```java
class Solution {
    //字符串处理
    public String process(String str){
        int n = str.length();
        if(n == 0)
            return "^$";
        
        StringBuffer ans = new StringBuffer("^");
        for(int i = 0;i < n;i++){
            ans.append("#");
            ans.append(str.substring(i,i+1));
        }
        ans.append("#$");
        return ans.toString();
    }

    public String longestPalindrome(String s) {
        String str = process(s);

        int n = str.length();
        int[] dp = new int[n];//以i为中心的回文串的半径
        int C = 0,R = 0;

        for(int i = 1;i < n;i++){
            int i_mirror = 2*C - i;
            if(R>i){
                dp[i] = Math.min(R-i,dp[i_mirror]);
            }else{
                dp[i] = 0;
            }

            while((i+1+dp[i]) < n &&  str.charAt(i+1+dp[i]) == str.charAt(i-1-dp[i]))//进行扩展
                dp[i]++;
            
            if(i + dp[i] > R){
                R = i+dp[i];
                C = i;
            }
        }

        int index = 0;
        int len  = 0;
        for(int i = 1;i < n;i++){
            if(dp[i] > len){
                len = dp[i];
                index = i;
            }
        }

        int beg = (index-len)/2;
        return s.substring(beg,beg+len);
    }
}
```


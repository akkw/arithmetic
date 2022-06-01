>算法链接: [有效的字母异位词](https://leetcode.cn/leetbook/read/top-interview-questions/xar9lv/)  
作者:  akka  
关键字:  哈希表、字符串、排序  
搜索关键字: 字母异位词  
时间复杂度:  O(n)
>>算法分析: 计算字符串中各个字符出现的次数,然后统计两个字符传中字符出现的次数
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s == null || t == null || s.length() != t.length()) {
            return false;
        }

        int[] sStatistics = new int[26];
        int[] tStatistics = new int[26];
        char[] chars = s.toCharArray();
        char[] chars1 = t.toCharArray();

        for (int i = 0; i < s.length(); i++) {
            sStatistics[chars[i] - 'a'] += 1;
            tStatistics[chars1[i] - 'a'] += 1;
        }

        for (int i = 0; i < 26; i++) {
            if (sStatistics[i] != tStatistics[i]) {
                return false;
            }
        }

        return true;
    }
}
```
---


>算法链接: [分割回文串](https://leetcode.cn/leetbook/read/top-interview-questions/xaxi62/)  
作者:  akka  
关键字:  字符串、动态规划、回朔
搜索关键字: 字母异位词  
时间复杂度:  O(n)
>>算法分析: 
回文字符串性质: s[0] == s[len-1]则一定是回文字符串,否则一定不是
动态规划：我们利用这个性质，将字符串的所有字串分割，分割结果可以用一个二维数组表示，假设所有的字串都是回文字符串。
然后找出不满足性质的字符串，标记为不是回文字符串，如果一个字符串是回文字符串我们判断它的拓展区间是不是回文字符串
回朔：从一个小标开始，向左移动找出所有动态规划结果为回文字符串的串，在某个下i下标回朔完成后应当将结果中的串移除，避免字符重复使用


```java
class Solution {
    static boolean dp[][];
    static List<List<String>> result = new ArrayList<>();
    static List<String> ans = new ArrayList<>();
    static int n;

    public static void main(String[] args) {
        
    }
    public static List<List<String>> partition(String s) {
        n = s.length();
        dp = new boolean[n][n];
        // 假设所有字符串都是回文串
        for (int i = 0; i < n; ++i) {
            Arrays.fill(dp[i],true);
        }
        //找出不是回文串的字符串
        for (int i = n - 1; i >= 0; --i) {
            for (int j = i + 1; j < n; ++j) {
                dp[i][j] = (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]);
            }
        }

        dfs(s, 0);
        return result;
    }

    /**
     * 回朔目的:
     * 1、找到预先处理的子回文字符串
     * 2、
     * @param s 字符串
     * @param i 字串的起始位置
     */
    private static void dfs(String s, int i) {
        if (i == n) {
            //遍历到字符串末尾时，将结果记录下来
            result.add(new ArrayList<>(ans));
            return;
        }

        for (int j = i; j < n; ++j) {
            if (dp[i][j]) {
                ans.add(s.substring(i, j + 1));
                // 如果(i, j) 满足回文字符串，则将j+1 作为i去找剩余字符串中的回文串
                dfs(s,j + 1);
                // 移除后面的字符串，防止使用重复
                ans.remove(ans.size() - 1);
            }
        }
    }
}
```
---


>算法链接: [单词拆分](https://leetcode.cn/leetbook/read/top-interview-questions/xa503c/)  
作者:  akka  
关键字:  动态规划, 字典树
搜索关键字: 单词
时间复杂度:  O(nlog n)
>>算法分析: 将字符串分为[0, j) [j,i]如果[0,j)符合要求，[j,i] 也符合要求 那么[0,j]也符合要求  
```java
class Solution {
    public static boolean wordBreak(String s, List<String> wordDict) {
        boolean dp[] = new boolean[s.length() + 1];
        HashSet<String> wordDictSet = new HashSet<>(wordDict);
        dp[0] = true;

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordDictSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```
---


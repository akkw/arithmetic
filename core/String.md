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

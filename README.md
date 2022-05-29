>算法链接: [题目名字]()  
关键字:  
搜索关键字:  
作者:  
时间复杂度:  
>>算法分析:  
```java
class Solution {
    
}
```
---

>算法链接: [字符串中的第一个唯一字符](https://leetcode.cn/leetbook/read/top-interview-questions/xaph0j/)  
关键字: 队列 哈希表 字符串 计数  
搜索关键字:  
作者:qiangzhiwei  
时间复杂度:  
>>算法分析: 创建一个长为26的字符索引，都填充为-1，如果字符串第一次出现，记录它在字符串中的位置，否则记为-2。
```java
class Solution {
    public int firstUniqChar(String s) {
        int[] index = new int[26];
        Arrays.fill(index, -1);

        char[] chars = s.toCharArray();

        for (int i = 0; i < chars.length; i++) {
            int n = chars[i] - 'a';
            if (index[n] == -1) {
                index[n] = i;
            } else {
                index[n] = -2;
            }
        }
        int min = Integer.MAX_VALUE;
        for (int i : index) {
            if (i == -1 || i == -2) {
                continue;
            }
            min = Math.min(min, i);
        }
        return min ==  Integer.MAX_VALUE ? -1 : min;
    }
}
```

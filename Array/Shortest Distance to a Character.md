# [821. 字符的最短距离](https://leetcode-cn.com/problems/shortest-distance-to-a-character/)
## 题目描述
```
给你一个字符串 s 和一个字符 c ，且 c 是 s 中出现过的字符。

返回一个整数数组 answer ，其中 answer.length == s.length 且 answer[i] 是 s 中从下标 i 到离它 最近 的字符 c 的 距离 。

两个下标 i 和 j 之间的 距离 为 abs(i - j) ，其中 abs 是绝对值函数。

 

示例 1：

输入：s = "loveleetcode", c = "e"
输出：[3,2,1,0,1,0,0,1,2,2,1,0]
解释：字符 'e' 出现在下标 3、5、6 和 11 处（下标从 0 开始计数）。
距下标 0 最近的 'e' 出现在下标 3 ，所以距离为 abs(0 - 3) = 3 。
距下标 1 最近的 'e' 出现在下标 3 ，所以距离为 abs(1 - 3) = 3 。
对于下标 4 ，出现在下标 3 和下标 5 处的 'e' 都离它最近，但距离是一样的 abs(4 - 3) == abs(4 - 5) = 1 。
距下标 8 最近的 'e' 出现在下标 6 ，所以距离为 abs(8 - 6) = 2 。
示例 2：

输入：s = "aaab", c = "b"
输出：[3,2,1,0]
 

提示：
1 <= s.length <= 104
s[i] 和 c 均为小写英文字母
题目数据保证 c 在 s 中至少出现一次

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shortest-distance-to-a-character
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
## 思路
******
### 思路一：[中心扩展法](https://github.com/suukii/91-days-algorithm/blob/master/basic/array-stack-queue/02.shortest-distance-to-a-character.md)

对每个字符都分别向左向右进行遍历，字符与目标c的距离为desc。

### 代码
```java
class Solution {
    public int[] shortestToChar(String s, char c) {
        int len = s.length();
        int[] answer = new int[len];
        for(int i = 0; i < len; i++){

            int left = i;
            int right = i;
            int disc = 0;
            while(left >= 0 || right < len - 1){
                if(s.charAt(left) == c){
                    disc = i - left;
                    break;
                }
                if(s.charAt(right) == c){
                    disc = right - i;
                    break;
                }
                if(left > 0) left--;
                if(right < len - 1) right++;
            }
            answer[i] = disc;
        }
        return answer;
    } 
}
```
### 复杂度分析
- 时间复杂度：O(N^2)
- 空间复杂度：O(1)

```
执行结果：
通过
显示详情
执行用时：6 ms, 在所有 Java 提交中击败了17.44%的用户
内存消耗：38.7 MB, 在所有 Java 提交中击败了29.60%的用户
```
******
### 思路二：贪心算法（官方题解）
### 代码
### 复杂度分析

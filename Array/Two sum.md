## [1、两数之和](https://leetcode-cn.com/problems/two-sum/)

## 题目描述
```
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。
最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。
你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。

示例 2:
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
 
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/plus-one
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
## 思路
### 思路1：暴力法

1、创建一个新数组用来保存返回结果的下标。
2、遍历给定数组，当前下标为i，判断数组内是否存在元素与 i 相加等于 target
3、符合条件返回结果.

### 代码
Java:
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        int i,j;
        for(i = 0;i < nums.length;++i){
            for(j = i+1; j <nums.length; ++j){
                if( nums[i] + nums[j] == target){
                    result[0] = i;
                    result[1] = j;
                    break;
                }
            }
        }
        return result;
    }
}
```
### 复杂度分析
- 时间复杂度：O(N*2),其中 NN 是数组中的元素数量。最坏情况下数组中任意两个数都要被匹配一次。
- 空间复杂度：O(1)

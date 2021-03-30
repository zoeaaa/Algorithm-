## [66、加一](https://leetcode-cn.com/problems/plus-one/)
```
题目描述
给定一个由 整数 组成的 非空 数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

 

示例 1：

输入：digits = [1,2,3]
输出：[1,2,4]
解释：输入数组表示数字 123。
示例 2：

输入：digits = [4,3,2,1]
输出：[4,3,2,2]
解释：输入数组表示数字 4321。
示例 3：

输入：digits = [0]
输出：[1]
 

提示：

1 <= digits.length <= 100
0 <= digits[i] <= 9

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/plus-one
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

### 思路
1、给定数组有三种情况：末尾不是9；末尾是9；全是9。

2、末位为9时向前加一

3、全是9时数组首元素为1

### 代码
```java
class Solution {
    public int[] plusOne(int[] digits) {
     for(int i = digits.length - 1; i >= 0; i--){
        digits[i]++;       //加一
        digits[i] = digits[i] % 10;
        if(digits[i] != 0){   //判断末位加一后是否为0，否：输出数组，是：继续循环
            return digits;
        }
     }
     digits = new int[digits.length+1];//如果输入数组为99，999等数字，需要进位
     digits[0] = 1;
     return digits;   
    }
}

```

### 复杂度分析
- 时间复杂度：O(n)
- 空间复杂度：O(1)

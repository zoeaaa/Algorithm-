# [394、字符串姐解码](https://leetcode-cn.com/problems/decode-string/)

## 题目描述
```
给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

 

示例 1：

输入：s = "3[a]2[bc]"
输出："aaabcbc"
示例 2：

输入：s = "3[a2[c]]"
输出："accaccacc"
示例 3：

输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
示例 4：

输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"
通过次数88,408提交次数

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/decode-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

### 思路一：辅助栈
遍历字符串有s中的每个字符c:
1. 数字：数字有可能为多位数，要进行计算。
2. 字母：在res的尾部拼接c
3. '【':数字和字母分别入其对应的栈，并将两者空置
4. '】':stack出栈，res = 刚出栈的res + 当前res * 刚出栈的数字num

### 代码
```java
class Solution {
    public String decodeString(String s) {
        Stack<Integer> nums = new Stack<>();//数字栈，存放入栈数字
        Stack<String> strs  = new Stack<>();//字符栈，存放入栈字符

        //StringBuilder和StringBuffer是String类的同伴类。它们表示一个可变的字符序列。
        StringBuilder res = new StringBuilder();

        int num = 0;

        for(Character c : s.toCharArray()){//
            if(c >= '0' && c <= '9'){
            //获得倍数
            //ascall码相减得到的才是数字差，如果不减的话数字的char会被解析成数字，比如‘0’对应48，所以需要减‘0’
                num = num * 10 + c -'0';
            }else if(c == '['){
                nums.push(num);//将num入栈
                num = 0;//num置0

                strs.push(res.toString());//字符进栈
                res = new StringBuilder();//入栈后清空
            }else if(c == ']'){//此时res为 “[” 之后到 “]” 之间的字符串内容
                String tem = strs.peek();//字符串出栈
                for(int j = 0;j < nums.peek(); j++){
                    tem += res.toString();
                }
                res = new StringBuilder(tem);//tmp才是拼接后的正确结果
                nums.pop();//用过的倍数丢弃
                strs.pop();//用过的字符串丢弃
            }else{
                res.append(c);
            }
        }
        return res.toString();
    }
}
```
### 复杂度分析
- 时间复杂度：O(N)，遍历了一次数组，N为数组长度
- 空间复杂度：O(N)，使用了额外的栈，是字符串大小的线性倍数
```
执行结果：通过
显示详情
执行用时：2 ms, 在所有 Java 提交中击败了53.77%的用户
内存消耗：37 MB, 在所有 Java 提交中击败了13.80%的用户
```

******
### 思路二：递归

### 代码

### 复杂度分析
- 时间复杂度：
- 空间复杂度：

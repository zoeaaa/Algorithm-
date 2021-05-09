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

- [暴力枚举](https://github.com/zoeaaa/Algorithm-/blob/main/Array/1%E3%80%81Two%20sum.md#暴力枚举)

- [哈希表](https://github.com/zoeaaa/Algorithm-/blob/main/Array/1%E3%80%81Two%20sum.md#哈希表)

## 暴力枚举

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

C:
```c
int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    for (int i = 0; i < numsSize; ++i) {
        for (int j = i + 1; j < numsSize; ++j) {
            if (nums[i] + nums[j] == target) {
                int* ret = malloc(sizeof(int) * 2);//按照提示申请动态数组
                ret[0] = i, ret[1] = j;
                *returnSize = 2;
                return ret;
            }
        }
    }
 //   *returnSize = 0;
    return NULL;
}
```
### 复杂度分析
- 时间复杂度：O(n2),其中 NN 是数组中的元素数量。最坏情况下数组中任意两个数都要被匹配一次。
- 空间复杂度：O(1)

## 哈希表

哈希表可以将寻找 target - x 的时间复杂度降到O(1)。

### 代码
Java:
```java []
class Solution {
    public int[] twoSum(int[] nums, int target) {

        Map<Integer,Integer> Hash = new HashMap<Integer,Integer>();
        for(int i = 0; i < nums.length; i++){
            if (Hash.containsKey(target - nums[i])){
                return new int[] {Hash.get(target - nums[i]),i};//若存在目标，返回结果
            }
            Hash.put(nums[i],i);//若不存在目标，将其值存入哈希表
        }
    return new int[0];
    }
}
```

Python3:
```python []
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable = dict();
        #遍历数组
        for i , num in enumerate(nums):
            #在哈希表中寻找target - num
            if target - num in hashtable:
                return [hashtable[target - num],i] #若存在，返回结果
            hashtable[nums[i]] = i #若目标不存在，将数组值存入哈希表
        return []
```

Javascipt
```javascript []
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {

    let map = new Map();
    for(let i = 0, len = nums.length; i < len; i++){
        if(map.has(target - nums[i])){
            return [map.get(target - nums[i]), i];
        }else{
            map.set(nums[i],i);
        }
    }
    return [];
};
```
### 复杂度分析：
- 时间复杂度：O(N)
- 空间复杂度：O(N)

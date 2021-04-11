# 数组、栈、队列
## [1、数组特性](https://github.com/leetcode-pp/91alg-2/blob/master/lecture/basic-01.md)
- 一个数组表示的是一系列的元素
- 数组（static array）的长度是固定的，一旦创建就不能改变（但是可以有 dynamic array）
- 所有的元素需要是同一类型（个别的语言除外）
- 可以通过下标索引获取到所储存的元素（随机访问）。 比如 array[index]
- 下标可以是是 0 到 array.length - 1 的任意整数


****
以Java为例

- 声明数组变量

```java

int [] arr;       //首选方法
int arr[];        //相同效果，非首选方法
```

- 创建数组

Java语言使用new操作符来创建数组，语法如下：
```java
arrayRefVar = new dataType[arraySize];
//上面的语法语句做了两件事：
//一、使用 dataType[arraySize] 创建了一个数组。
//二、把新创建的数组的引用赋值给变量 arrayRefVar
```

- 数组变量的声明，和创建数组可以用一条语句完成，如下所示：
```java
dataType[] arrayRefVar = new dataType[arraySize];
```
*****


## [2、数组的常规操作]()
数组的基本操作及[复杂度分析](https://blog.csdn.net/qq_35478489/article/details/98482371)

1、随机访问，时间复杂度O(1)
```c
arr = [1,2,33]
arr[0] //1
arr[2] //33
```
2、遍历，时间复杂度O(N)
```c
for num in nums:
  print(num)
```
3、任意位置插入元素、删除元素
```c
arr = [1,2,33]
//在索引2前插入一个5
arr.insert(2,5)
print(arr) //[1,2,5,33]
```
我们不难发现， 插入 2 之后，新插入的元素之后的元素（最后一个元素）的索引发生了变化，从 2 变成了 3，而其前面的元素没有影响。从平均上来看，数组插入元素和删除元素的时间复杂度为O(N)。最好的情况删除和插入发生在尾部，时间复杂度为 O(1)。

基本上数组都支持这些方法。 虽然命名各有不同，但是都是上面四种操作的实现：
- each()： 遍历数组
- pop(index)：删除数组中索引为 index 的元素
- insert(item, index)：数组索引为 index 处插入元素

 ### 时间复杂度小结 
- 随机访问 -> O(1)
- 根据索引修改 -> O(1)
- 遍历数组 -> O(N)
- 插入数值到数组 -> O(N)
- 插入数值到数组最后 -> O(1)
- 从数组删除数值 -> O(N)
- 从数组最后删除数值 -> O(1)


### 每日一题

- [x]  [【day-01】66.加一](https://github.com/zoeaaa/Algorithm-/blob/main/Array/66%E3%80%81Plus%20One.md)
- [x]  [【day-02】821.字符的最短距离](https://github.com/zoeaaa/Algorithm-/blob/main/Array/821%E3%80%81Shortest%20Distance%20to%20a%20Character.md)
- [x]  [【day-03】1381.设计一个支持增量操作的栈](https://github.com/zoeaaa/Algorithm-/blob/main/Array/1381.%20Design%20a%20Stack%20With%20Increment%20Operation.md)
- [x]  [【day-04】394.字符串解码](https://github.com/zoeaaa/Algorithm-/blob/main/Array/394%E3%80%81Decode%20String.md)
- [ ]  [【day-05】232.用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)
- [ ]  [【day-06】768.最多能完成排序的块 II](https://leetcode-cn.com/problems/max-chunks-to-make-sorted-ii/)

#### 数组拓展题目

- [ ]  [75.颜色分类](https://leetcode-cn.com/problems/sort-colors/)
- [ ]  [28.实现 strStr()](https://leetcode-cn.com/problems/implement-strstr/)
- [ ]  [380.常数时间插入、删除和获取随机元素](https://leetcode-cn.com/problems/insert-delete-getrandom-o1/)
- [ ]  [189.旋转数组](https://leetcode-cn.com/problems/rotate-array/)
- [ ]  [59. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)
- [ ]  [859. 亲密字符串](https://leetcode-cn.com/problems/buddy-strings/)

## [2、栈]()
- 后进后出

### 栈的常用操作与时间复杂度
- 进栈 - push - 将元素放置到栈顶
- 出栈 - pop - 将栈顶元素弹出
> pop与peek的区别：peek只取值，不改变栈；pop取值，并删除栈顶元素
- 取栈顶 - top - 得到栈顶元素的值
- 判断是否为空栈 - isEmpty - 判断栈内是否有元素
由于栈只允许在尾部操作，我们用数组进行模拟的话，可以很容易达到 O(1)的时间复杂度。
```java
import java.util.Stack;
 
public class StackTest {
 
	/**
	 * @param args
	 */
	public static void main(String[] args) {
 
		Stack<Integer> stack = new Stack<Integer>();
 
		for (int i = 0; i < 5; i++) {
			stack.push(i);
		}
		
		System.out.println("isEmpty:"+stack.isEmpty());//判断栈内是否有元素
		System.out.println("capacity:"+stack.capacity());//获取栈的容量
		System.out.println("peek:"+stack.peek());//取堆栈顶点
 
		System.out.println("*********遍历操作**********");
		
		// 集合遍历方式
		for (Integer x : stack) {
			System.out.println(x);
		}
		System.out.println("--------------------------");
		// 栈弹出遍历方式
		// while (s.peek()!=null) { //不健壮的判断方式，容易抛异常，正确写法是下面的
		while (!stack.empty()) {
			System.out.println(stack.pop());
		}
		
	}
}
```

> 当然也可以用链表实现，即链式栈。

- 进栈 - O(1)
- 出栈 - O(1)
- 取栈顶 - O(1)
- 判断是否为空栈 - O(1)

### 相关题目
- [ ] [150. 逆波兰表达式求值]()

题目推荐
- [ ] [1381. 设计一个支持增量操作的栈]()
- [x] [394. 字符串解码](https://github.com/zoeaaa/Algorithm-/blob/main/Array/394%E3%80%81Decode%20String.md)
- [ ] [946. 验证栈序列]()

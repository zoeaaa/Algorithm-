# [树]()

## 二叉树
- [每日一题](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/Readme.md#每日一题)
- [题目推荐](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/Readme.md#题目推荐)
- [Leetcode的树](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/Readme.md#Leetcode的树)

## 1. 二叉树的种类

- 完全二叉树
- 满二叉树
- [二叉搜索树(BST)](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/Readme.md#二叉搜索树)
- [平衡二叉树](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/Readme.md#平衡二叉树)
- 红黑树
- 。。。

## 2. 二叉树的存储方式

- 链式存储（链表存储）
- 顺序存储（数组存储）

## 3. 二叉树的遍历

- 深度优先遍历
     - [递归](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/Readme.md#递归)
     - [迭代](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/Readme.md#迭代)
- 广度优先遍历

## 二叉搜索树

 二叉搜索树是二叉树的一种，具有以下性质：

  1. 左子树的所有节点值小于根的节点值（注意不含等号）
  
  2. 右子树的所有节点值大于根的节点值（注意不含等号）

另外二叉搜索树的中序遍历结果是一个有序列表。

## 平衡二叉树

## 深度优先遍历
### 递归

递归与栈的关系：

<div align=center>
     
![递归.png](https://i.loli.net/2021/04/27/bAYC25xOcFDu6Zi.png)
     
</div>

递归算法的三个要素：

1. 「确定递归函数的参数和返回值：」确定参与递归的元素；确定每一次递归元素的返回类型，从而确定递归函数的返回类型。
2. 「确定终止条件：」如果递归没有终止条件，则无法终止程序。操作系统的内存栈必然会溢出。
3. 「确定单层递归的逻辑：」确定每一层递归的逻辑信息，在之后会反复调用。

**************************************************************

#### 以[前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)为例

1、确定函数的参数和返回值
```java
public List<Integer> preorderTraversal(TreeNode root)
```
2、确定终止条件
```java
if(root == null) return;
```
3、确定单层递归的逻辑
```java
preorderList.add(root.val);//中
preorderTraversal(root.left);//前
preorderTraversal(root.right)；//后
```

完整代码
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    List<Integer> preorderList = new ArrayList<>();
    public List<Integer> preorderTraversal(TreeNode root) {
        
        if(root != null){
            preorderList.add(root.val);
            preorderTraversal(root.left);
            preorderTraversal(root.right);
        }
        return preorderList;
    }
}
```

参照前序遍历的解法，中序和后序遍历也不难理解了。

[中序遍历：](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
```java
class Solution {
    List<Integer> preorderList = new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {

        if(root != null){
            inorderTraversal(root.left);
            preorderList.add(root.val);
            inorderTraversal(root.right);
        }
        return preorderList;
    }
}
```

[后序遍历：](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)
```java
class Solution {
    List<Integer> preorderList = new ArrayList<>();
    public List<Integer> postorderTraversal(TreeNode root) {
        if(root != null){
            postorderTraversal(root.left);
            postorderTraversal(root.right);
            preorderList.add(root.val);
        }
        return preorderList;
    }
}
```

*********************************************************************

### 迭代

为什么可以用迭代法（非递归方式）来实现二叉树的前中后序遍历

> 递归的实现就是：`每一次递归调用都会把函数的局部变量、参数值和返回地址等压入栈中`，然后递归返回的时候，从栈顶弹出上一次递归的各项参数，所以这就是递归为什么可以返回上一层位置的原因。

本质上是在模拟递归，因为在递归的过程中使用了系统栈，所以在递归的解法中常用`Stack`来模拟系统栈。

前序遍历
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {

        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();

        if(root == null) return res;
        TreeNode cur = root;
        while(cur != null || !stack.isEmpty()){
            if(cur != null){
                res.add(cur.val);
                stack.push(cur);
                cur = cur.left;
            }else{
                cur = stack.pop();
                cur = cur.right;
            }
        }
        return res;
    }
}
```

中序遍历
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {

        List<Integer> res = new Stack<>();
        Stack<TreeNode> stack = new Stack<>();

        TreeNode cur = root;

        while(cur != null || !stack.isEmpty()){
            if(cur != null){
                stack.push(cur);
                cur = cur.left;
            }else{
                cur = stack.pop();
                res.add(cur.val);
                cur = cur.right;
            }
        }
        return res;
    }
}
```

后序遍历
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {

        Stack<TreeNode> resStack = new Stack<>();
        Stack<TreeNode> stack = new Stack<>();

        TreeNode cur = root;
        while(cur != null || !stack.isEmpty()){
            if(cur != null){
                resStack.push(cur);
                stack.push(cur);
                cur = cur.right;
            }else{
                cur = stack.pop();
                cur = cur.left;
            }
        }
        List<Integer> res = new ArrayList<>();
        while(!resStack.isEmpty()){
            res.add(resStack.pop().val);
        }
        return res;
    }
}
```

[迭代统一写法：标记法](https://mp.weixin.qq.com/s/c_zCrGHIVlBjUH_hJtghCg)

## [广度优先遍历](https://mp.weixin.qq.com/s?__biz=MzA5ODk3ODA4OQ==&mid=2648167212&idx=1&sn=6af5ffe5b69075b21bb4743ddcee4e7c&chksm=88aa236abfddaa7cae70b42edb299d0a52d9f1cc4fc1fdba1116972fc0ca0275b8bfdf10851b&token=1607921395&lang=zh_CN#rd)

**BFS**不是层序遍历。

BFS 的核心在于求最短问题时候可以提前终止，这才是它的核心价值，层次遍历是一种不需要提前终止的 BFS 的副产物。

> 如果仅仅是遍历二叉树的话,DFS会更加方便。BFS更适合用于解决最短路径相关问题。

BFS 遍历使用**队列**数据结构：
```java
void bfs(TreeNode root) {
    Queue<TreeNode> queue = new ArrayDeque<>();
    queue.add(root);
    while (!queue.isEmpty()) {
        TreeNode node = queue.poll(); 
        if (node.left != null) {
            queue.add(node.left);
        }
        if (node.right != null) {
            queue.add(node.right);
        }
    }
}
```
**1. 层序遍历**

什么是层序遍历呢？简单来说，就是把二叉树分层，每一层从左到右进行遍历。

层序遍历要求的输出结果和BFS是不同的。层序遍历要求返回的是能区分每一层的二维数组，而BFS返回的结果是一维数组，无法区分。

因此，层序遍历的代码修改为：
```java
// 二叉树的层序遍历
void bfs(TreeNode root) {
    Queue<TreeNode> queue = new ArrayDeque<>();
    queue.add(root);
    while (!queue.isEmpty()) {
        int n = queue.size();
        for (int i = 0; i < n; i++) { 
            // 变量 i 无实际意义，只是为了循环 n 次
            TreeNode node = queue.poll();
            if (node.left != null) {
                queue.add(node.left);
            }
            if (node.right != null) {
                queue.add(node.right);
            }
        }
    }
}
```

**2. 最短路径**

在一棵树中，一个结点到另一个结点的路径是唯一的，但在图中，结点之间可能有多条路径，其中哪条路最近呢？这一类问题称为最短路径问题。最短路径问题也是 BFS 的典型应用，而且其方法与层序遍历关系密切。

在二叉树中，BFS 可以实现一层一层的遍历。在图中同样如此。从源点出发，BFS 首先遍历到第一层结点，到源点的距离为 1，然后遍历到第二层结点，到源点的距离为 2…… 可以看到，用 BFS 的话，距离源点更近的点会先被遍历到，这样就能找到到某个点的最短路径了。


**3. 相关题目**

- [x] [102.二叉树的层序遍历](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/102.%20%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.md)
- [ ] [107.二叉树的层次遍历II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)
- [ ] [199.二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)
- [ ] [637.二叉树的层平均值](https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/)
- [ ] [429.N叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)
- [ ] [515.在每个树行中找最大值](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/)
- [ ] [116.填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)
- [ ] [117.填充每个节点的下一个右侧节点指针II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)

### 每日一题

- [x] [104.二叉树的最大深度](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/104.%20%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.md)
- [x] [100.相同的树](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/100.%20%E7%9B%B8%E5%90%8C%E7%9A%84%E6%A0%91.md)
- [x] [129.求根到叶子节点数字之和](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/129.%20%E6%B1%82%E6%A0%B9%E8%8A%82%E7%82%B9%E5%88%B0%E5%8F%B6%E8%8A%82%E7%82%B9%E6%95%B0%E5%AD%97%E4%B9%8B%E5%92%8C.md)
- [x] [513.找树左下角的值](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/513.%20%E6%89%BE%E6%A0%91%E5%B7%A6%E4%B8%8B%E8%A7%92%E7%9A%84%E5%80%BC.md)
- [ ] [297.二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)
- [ ] [987.二叉树的垂序遍历](https://leetcode-cn.com/problems/vertical-order-traversal-of-a-binary-tree/)


### 题目推荐
- [ ] [589. N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)（熟悉 N 叉树）
- [ ] [662. 二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/) (请分别使用 BFS 和 DFS 解决，空间复杂度尽可能低)
- [ ] [834. 树中距离之和](https://leetcode-cn.com/problems/sum-of-distances-in-tree/description/)（谷歌面试题）
- [ ] [967. 连续差相同的数字](https://leetcode-cn.com/problems/numbers-with-same-consecutive-differences/description/) (隐形树的遍历)
- [ ] [1145. 二叉树着色游戏](https://leetcode-cn.com/problems/binary-tree-coloring-game/)（树上进行决策）

### Leetcode的树
- [x] [100.相同的树](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/100.%20%E7%9B%B8%E5%90%8C%E7%9A%84%E6%A0%91.md)
- [x] [102.二叉树的层序遍历](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/102.%20%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.md)
- [x] [104.二叉树的最大深度](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/104.%20%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.md)
- [ ] [107.二叉树的层次遍历II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)
- [ ] [116.填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)
- [ ] [117.填充每个节点的下一个右侧节点指针II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)
- [x] [129.求根到叶子节点数字之和](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/129.%20%E6%B1%82%E6%A0%B9%E8%8A%82%E7%82%B9%E5%88%B0%E5%8F%B6%E8%8A%82%E7%82%B9%E6%95%B0%E5%AD%97%E4%B9%8B%E5%92%8C.md)
- [ ] [199.二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)
- [ ] [297.二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)
- [ ] [429.N叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)
- [x] [513.找树左下角的值](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/513.%20%E6%89%BE%E6%A0%91%E5%B7%A6%E4%B8%8B%E8%A7%92%E7%9A%84%E5%80%BC.md)
- [ ] [515.在每个树行中找最大值](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/)
- [ ] [589. N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)（熟悉 N 叉树）
- [ ] [637.二叉树的层平均值](https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/)
- [ ] [662. 二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/) (请分别使用 BFS 和 DFS 解决，空间复杂度尽可能低)
- [ ] [834. 树中距离之和](https://leetcode-cn.com/problems/sum-of-distances-in-tree/description/)（谷歌面试题）
- [x] [872. 叶子相似的树](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/872.%20%E5%8F%B6%E5%AD%90%E7%9B%B8%E4%BC%BC%E7%9A%84%E6%A0%91.md)(5.10每日一题)
- [ ] [967. 连续差相同的数字](https://leetcode-cn.com/problems/numbers-with-same-consecutive-differences/description/) (隐形树的遍历)
- [ ] [1145. 二叉树着色游戏](https://leetcode-cn.com/problems/binary-tree-coloring-game/)（树上进行决策）
- [ ] [987.二叉树的垂序遍历](https://leetcode-cn.com/problems/vertical-order-traversal-of-a-binary-tree/)
- [ ] [1145. 二叉树着色游戏](https://leetcode-cn.com/problems/binary-tree-coloring-game/)（树上进行决策）


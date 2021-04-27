# [树]()

## 二叉树

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
     - [迭代](https://github.com/zoeaaa/Algorithm-/blob/main/Tree/Readme.md##迭代)
- 广度优先遍历

## 二叉搜索树

 二叉搜索树是二叉树的一种，具有以下性质：

  1. 左子树的所有节点值小于根的节点值（注意不含等号）
  
  2. 右子树的所有节点值大于根的节点值（注意不含等号）

另外二叉搜索树的中序遍历结果是一个有序列表。

## 平衡二叉树

### 递归

> 递归的实现就是：`每一次递归调用都会把函数的局部变量、参数值和返回地址等压入栈中`，然后递归返回的时候，从栈顶弹出上一次递归的各项参数，所以这就是递归为什么可以返回上一层位置的原因。

递归与栈的关系：


递归算法的三个要素：

1. 「确定递归函数的参数和返回值：」确定参与递归的元素；确定每一次递归元素的返回类型，从而确定递归函数的返回类型。
2. 「确定终止条件：」如果递归没有终止条件，则无法终止程序。操作系统的内存栈必然会溢出。
3. 「确定单层递归的逻辑：」确定每一层递归的逻辑信息，在之后会反复调用。

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


### 迭代

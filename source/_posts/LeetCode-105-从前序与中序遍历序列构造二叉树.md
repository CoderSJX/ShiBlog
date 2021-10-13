title: 'LeetCode:105. 从前序与中序遍历序列构造二叉树'
author: Shi
tags:
  - Leetcode
categories:
  - Algorithm
date: 2021-10-13 18:07:00
---
### **[105. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)**

难度中等1253

给定一棵树的前序遍历 `preorder` 与中序遍历  `inorder`。请构造二叉树并返回其根节点。

解题：

1. 二叉树的题，要么是递归，要么就是堆栈，再就是dfs，bfs
2. 先构建根节点，递归构建左子树、右子树
3. 关键在于，每次怎么找到根节点
4. preorder是先序遍历，所以每次先出现的都是根节点
5. 并且，对于任何一个叶子节点而言，他也是他的子树的根节点。
6. 所以用preIndex来指示，当前遍历需要建立以哪个节点为根节点的树。
7. 因为中序遍历，在根节点的左边，全是位于根节点左子树里的值，
8. 在根节点的右边，全是位于根节点右子树里的值。
9. 我们需要先存储每个根节点在中序遍历中的位置。
10. 然后把该根节点构建完成后，递归建立从left到该根节点位置的其他值的节点
11. 递归建立从该节点位置后面到right的其他值的节点，
12. 也就是建立左右子树，
13. 然后把左右子树接在该根节点上。

```java
import java.util.HashMap;
import java.util.Map;

public class BuildTreeWithPreAndInOrder {
    private int[] preorder;
    private int[] inorder;
    private int preIndex = 0;
    private Map<Integer, Integer> positions = new HashMap<>();
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.inorder = inorder;
        this.preorder = preorder;
        for (int i = 0; i < preorder.length; i++) {
            positions.put(inorder[i], i);
        }
        return helper(0, inorder.length);
    }
    public TreeNode helper(int left, int right) {
        if (left >= right) return null;
        int val = preorder[preIndex];
        Integer mid = positions.get(val);
        TreeNode root = new TreeNode(val);
        preIndex++;
        root.left = helper(left, mid);
        root.right = helper(mid + 1, right);
        return root;
    }
}
```
title: 'LeetCode:199. 二叉树的右视图'
author: Shi
tags:
  - Leetcode
categories:
  - Algorithm
date: 2021-10-13 17:29:00
---
### **[199. 二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)**

难度中等547

给定一个二叉树的 **根节点** `root`，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

解题：

1. 每层只保留最右边的节点
2. 每次递归都把该节点的值放到数组里，数组的下标表示二叉树的层级
3. 那么只要将递归的顺序调整一下，那么最后res数组中保存的就是最右边的值
4. 将顺序调过来就是左视图。

```java
package tree;

import java.util.ArrayList;
import java.util.List;

public class RightSideView {
    private List<Integer> res = new ArrayList<>();

    public List<Integer> rightSideView(TreeNode root) {
        helper(root,0);
        return res;
    }

    private void helper(TreeNode root,int index) {
        if (root == null) return;
        if(index>res.size()){
            res.add(root.val);
        }else{
            res.set(index,root.val);
        }
//右视图
        helper(root.left,index+1);
        helper(root.right,index+1);
    }

}

```

```java
package tree;

import java.util.ArrayList;
import java.util.List;

public class RightSideView {
    private List<Integer> res = new ArrayList<>();

    public List<Integer> rightSideView(TreeNode root) {
        helper(root,0);
        return res;
    }

    private void helper(TreeNode root,int index) {
        if (root == null) return;
        if(index>res.size()){
            res.add(root.val);
        }else{
            res.set(index,root.val);
        }
        helper(root.right,index+1);
//左视图
        helper(root.left,index+1);
    }

}

```
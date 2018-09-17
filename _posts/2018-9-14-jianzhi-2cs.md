---
title: 二叉树相关
description:
categories: 算法
tags:
- 剑指offer
- 二叉树
- leetcode
---  


### 思路
1. 二叉树多用递归思想，确定边界条件。
2. 二叉树相关性质。

### 重建二叉树  
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
````javascript
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function reConstructBinaryTree(pre, vin)
{
    if(!pre||pre.length==0){
        return;
    }
    var treeNode={
        val:pre[0]
    }
    for(var i=0;i<pre.length;i++){
        if(vin[i]==pre[0]){
            treeNode.left=reConstructBinaryTree(pre.slice(1,i+1), vin.slice(0,i));
            treeNode.right=reConstructBinaryTree(pre.slice(i+1), vin.slice(i+1));
        }
    }
    return treeNode
}
````

### 二叉树的镜像    
````javascript
  /* function TreeNode(x) {
      this.val = x;
      this.left = null;
      this.right = null;
  } */
  function Mirror(root)
  {
      if(!root){
          return false;
      }
      var temp=root.left;
      root.left=root.right;
      root.right=temp;
      Mirror(root.left);
      Mirror(root.right);
  }
````  
  
### 平衡二叉树  
输入一棵二叉树，判断该二叉树是否是平衡二叉树。二叉树的每个节点的左子树和右子树的深度不大于1
````javascript
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function IsBalanced_Solution(pRoot)
{
    if(pRoot==null){
        return true;
    }
    return Math.abs(deep(pRoot.left)-deep(pRoot.right))<=1?true:false;
}

function deep(root){
    if(!root){
        return 0;
    }
    return Math.max(deep(root.left),deep(root.right))+1;
}
````
### 对称二叉树    
请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。
````javascript
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function isSymmetrical(pRoot)
{
    return isSym(pRoot,pRoot);
}
function isSym(root1,root2){
     if(root1 == null && root2 == null){
        return true;
    }
    if(root1 == null || root2 == null){
        return false;
    }
    if(root1.val != root2.val){
        return false;
    }
    return isSym(root1.left, root2.right) && isSym(root1.right, root2.left);
    
}
````

### 二叉搜索树的后序遍历序列
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

#### 分治思想  
非递归也是一个基于递归的思想：
左子树一定比右子树小，因此去掉根后，数字分为left，right两部分，
right部分的最后一个数字是右子树的根他也比左子树所有值大，因此我们可以每次只看有子树是否符合条件即可。  
````javascript
function VerifySquenceOfBST(sequence)
{
    if(sequence.length==0){
        return false;
    }
    var n=sequence.length;
    var i=0;
    while(n--){
        while(sequence[i]<sequence[n]){
            i++
        }
        while(sequence[i]>sequence[n]){
            i++;
        }
        if(i<n){
            return false;
        }
        i=0;
    }
    return true;
}
````
 


---
title: 二叉树的前中后序层次遍历
description:
categories: 算法
tags:
- 剑指offer
- 二叉树
- leetcode
---   
### 前序--leetcode144
#### 思路
1. 采用一个辅助栈`stack`，将头节点`root`压入栈中。
2. 从`stack`弹出栈顶节点，并放入返回数组，将节点的右孩子，左孩子压入栈。
3. 重复步骤2，直到`stack`为空。  

#### 代码
````javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var preorderTraversal = function(root) {
    var res=[];
    var stack=[];
    if(root==null){
        return [];
    }
    stack.push(root);
    while(stack.length){
        root=stack.pop();
        res.push(root.val);
        if(root.right!=null){
            stack.push(root.right)
        }
        if(root.left){
            stack.push(root.left)
        }
    }
    return res;
};
````  
### 中序--leetcode94  
#### 思路
1. 用一个辅助栈`stack`
2. 先把`root`压入栈中，依次把左边界压入栈中，令`root=root.left`
3. 重复步骤2，直到`root==null`,从`stack`弹出栈顶元素，放入返回数组，并且`root=root.right`

#### 代码  
````javascript
var inorderTraversal = function(root) {
    var stack=[];
    var res=[];
    while(stack.length||root!=null){
        if(root!=null){
            stack.push(root);
            root=root.left;
        }else{
            root=stack.pop();
            res.push(root.val);
            root=root.right;
        }
    }
    return res;
};
````  
### 后序--leetcode145
#### 思路  
1. 记一个辅助栈是s1，将`root`压入s1
2. 从s1弹出的节点记为cur，依次将cur的左孩子和右孩子压入s1
3. 每一个从s1弹出的节点都放入另一个s2中，直到s1为空，从s2中依次弹出节点放入返回数组  

#### 代码
````javascript
var postorderTraversal = function(root) {
    if(root==null){
        return [];
    }
    var res=[],s1=[],s2=[];
    s1.push(root);
    while(s1.length){
        root=s1.pop();
        s2.push(root);
        if(root.left){
            s1.push(root.left);
        }
        if(root.right){
            s1.push(root.right);
        }
    }
    while(s2.length){
        res.push(s2.pop().val);
    }
    return res;
};
````  
### 二叉树的层次遍历--leetcode102
#### 思路  
1. 宽度优先遍历，记一个队列`queue`
2. 记录当前队列长度，即二叉树每一层上的节点数, 从`queue`出队
3. 每出队一个节点，向队列中压入其左右孩子  
 
#### 代码
````javascript
var levelOrder = function(root) {
    if(root==null){
        return [];
    }
    var queue=[],res=[];
    queue.push(root);
    while(queue.length){
        var len=queue.length;
        var temp=[];
        for(var i=0;i<len;i++){
            var node=queue.shift();
            temp.push(node.val);
            if(node.left){
                queue.push(node.left);
            }
            if(node.right){
                queue.push(node.right);
            }
        }
        res.push(temp);
    }
    return res;
};
````  
### 二叉树的锯齿形层次遍历--leetcode103  
#### 思路   
参考上一题层次遍历，增加一个标志变量，改变每一层输出顺序。
````javascript
var zigzagLevelOrder = function(root) {
    if(root==null){
        return [];
    }
    var queue=[],res=[],flag=true;
    queue.push(root);
    while(queue.length){
        var temp=[];
        var len=queue.length;
        for(var i=0;i<len;i++){
            var node=queue.shift();
            temp.push(node.val);
            if(node.left){
                queue.push(node.left);
            }
            if(node.right){
                queue.push(node.right);
            }
        }
        if(!flag){
            temp.reverse();
        }
        flag=!flag;
        res.push(temp);
    }
    return res;
};
````
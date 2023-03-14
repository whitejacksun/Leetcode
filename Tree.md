Tree is a recursive structure.

[**94. Binary Tree Inorder Traversal**](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

Given the ```root``` of a binary tree, return the inorder traversal of its nodes' values.

traversal:
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stk = new Stack<TreeNode>();
        List<Integer> res = new ArrayList<Integer>();
        TreeNode curr = root;
        while(curr != null || !stk.empty()){
            while(curr != null){
                stk.push(curr);
                curr = curr.left;
            }
            curr = stk.pop();
            res.add(curr.val);
            curr = curr.right;
        }
        return res;
    }
}
```


[**100. Same Tree**](https://leetcode.com/problems/same-tree/description/)

Given the roots of two binary trees ```p``` and ```q```, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

recursive:
```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null)return true;
        if(p == null && q != null || p != null && q == null)return false;
        if(p.val != q.val)return false;
        return isSameTree(p.left,q.left) && isSameTree(p.right,q.right);
    }
}
```

[**104. Maximum Depth of Binary Tree**](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

Given the ```root``` of a binary tree, return its maximum depth.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.


递归.每一步都取左右子树中更长的那一边
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null)return 0;
        return Math.max(maxDepth(root.left),maxDepth(root.right))+1;
    }
}
```

[**110. Balanced Binary Tree**](https://leetcode.com/problems/balanced-binary-tree/description/)

```java
class Solution {
    private boolean res = true;

    public int maxDepth(TreeNode root) {
        if(root == null)return 0;
        int l = maxDepth(root.left);
        int r = maxDepth(root.right);
        if(Math.abs(l - r) > 1)res = false;
        return Math.max(l,r)+1;
    }
    public boolean isBalanced(TreeNode root) {
        maxDepth(root);
        return res;
    }
}
```

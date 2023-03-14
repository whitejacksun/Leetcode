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


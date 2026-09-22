# Lab: Merge Two Binary Trees

## Code

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
    private TreeNode merge(TreeNode curr1, TreeNode curr2){
        //if curr1 and curr2 are not null, add them 
        if(curr1 != null && curr2 != null)
        {
            TreeNode main = new TreeNode(curr1.val + curr2.val);
            main.left = merge(curr1.left, curr2.left);
            main.right = merge(curr1.right, curr2.right);
            return main;
        }
        //if curr1 is null and curr2 is not, add curr2 to tree
        else if(curr1 == null && curr2 != null)
        {
            TreeNode main = new TreeNode(curr2.val);
            main.left = merge(curr1, curr2.left);
            main.right = merge(curr1, curr2.right);
            return main;
        }
        //if curr2 is null and curr1 is not, add curr1 to tree
        else if(curr1 != null && curr2 == null)
        {
            TreeNode main = new TreeNode(curr1.val);
            main.left = merge(curr1.left, curr2);
            main.right = merge(curr1.right, curr2);
            return main;
        }
        //base case
        else 
            return null;
    }

    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        //check if roots are null, return null or root1/root2
        if(root1 == null && root2 == null)
            return null;
        else if(root1 == null && root2 != null)
            return root2;
        else if(root1 != null && root2 == null)
            return root1;
        
        TreeNode root = new TreeNode(root1.val+root2.val);
        root.left = merge(root1.left, root2.left);
        root.right = merge(root1.right, root2.right);
        return root;
    }
}
```

## Description

I started off with my checks to see if either of the roots were null, then I could just return null or root1/root2. 
Then I create a new root, and call the helper function on the left and the right child of the root. 
The private recursive function essentially does the exact same thing but the control flow is backwards so the base case is in the else statement.

This is definitely not the most efficient way that I could have done this program. 
I did not need the private helper function since both the public and the private function basically have the exact same structure. 
I'm pretty sure if I just put the last four lines of my public function in an else statement the program would have worked the same way and been significantly more efficient. 

## Runtime and Memory Analysis

My solution's runtime is O(n), where n is the total number of nodes in whichever tree is bigger in the best case. 
Even after one tree runs out of nodes along a certain path, my code keeps recursing into the leftover part of the other tree and creating new nodes instead of just stopping and returning it directly.
So, I end up visiting every node of the bigger tree, not just where the two trees overlap.

If I had instead put the last four lines of my public function into an else statement (w/out the private helper), the recursion would only continue into a pair of nodes when both sides are still non-null.
When one side goes null, it would return the existing subtree directly instead of continuing to recurse into it. 
That means the best case would be the total number of nodes in whichever tree is smaller, which is more efficient than my best case.
In the worst case, both solutions would just be the sum of the number of nodes of each tree, as none of the nodes could overlap.

Memory is similar. I create a new node for every node in the bigger tree. 
The alternative would only allocate new nodes where both trees overlap, and just reuse the existing subtree everywhere else.
In the worst case, both solutions allocate the same number of new nodes, since if none of the nodes overlap there's nothing to reuse either way.
My solution also uses more call stack space, since it keeps recursing down whichever tree is taller instead of stopping as soon as one side runs out like the alternative does.

## Solution1
``` java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        Stack<TreeNode> curLevel = new Stack<>();
        Stack<TreeNode> nextLevel = new Stack<>();
        List<Integer> record = new LinkedList<>();
        List<List<Integer>> res = new LinkedList<>();
        int level = 0;
        if (root == null) {
            return res;
        }
        
        curLevel.push(root);
        while (!curLevel.empty()) {
            TreeNode cur = curLevel.pop();
            record.add(cur.val);
            placeToNextLevel(cur, nextLevel, level);
            
            if (curLevel.empty()) {
                level++;
                res.add(record);
                curLevel = nextLevel;
                nextLevel = new Stack<>();
                record = new LinkedList<>();
            }
        }
        return res;
    }
    private void placeToNextLevel(TreeNode cur, Stack<TreeNode> nextLevel, int level) {
        if (level % 2 == 0) {
            if (cur.left != null) {
                nextLevel.push(cur.left);
            }
            if (cur.right != null) {
                nextLevel.push(cur.right);
            }
        }
        else {
            if (cur.right != null) {
                nextLevel.push(cur.right);
            }
            if (cur.left != null) {
                nextLevel.push(cur.left);
            }
        }
    }
}
```

## note
* time O(n), space O(n)
* use stack instead of queue because we want to achieve LIFO 
* use two queues: one queue for storing the current level nodes and the other for storing next level nodes
* be careful of empty root node

## LeetCode 5.20 每日三题

### LeetCode 453：岛屿的周长

#### 题目

[https://leetcode-cn.com/problems/island-perimeter/](https://leetcode-cn.com/problems/island-perimeter/)

给定一个包含 0 和 1 的二维网格地图，其中 1 表示陆地 0 表示水域。

网格中的格子水平和垂直方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。

岛屿中没有“湖”（“湖” 指水域在岛屿内部且不和岛屿周围的水相连）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

#### 思路

从上下左右四个方向看

#### 代码

```java
class Solution {
    public int islandPerimeter(int[][] grid) {

        int n = grid.length,m = grid[0].length;
        int ans = 0;
        //1.从左向右看
        for(int i = 0;i < n;i++){
            boolean he = false;
            for(int j = 0;j < m;j++){
                if(grid[i][j] == 1 && !he){
                    ans++;
                    he = true;
                }
                if(grid[i][j] == 0)
                    he = false;
            }
        }
        
         //1.从右向左看
        for(int i = n-1;i >= 0;i--){
            boolean he = false;
            for(int j = m-1;j >= 0;j--){
                if(grid[i][j] == 1 && !he){
                    ans++;
                    he = true;
                }
                if(grid[i][j] == 0)
                    he = false;
            }
        }


         //1.从左向右看
        for(int i = 0;i < m;i++){
            boolean he = false;
            for(int j = 0;j < n;j++){
               // System.out.println(i+" "+j);
                if(grid[j][i] == 1 && !he){
                    ans++;
                    he = true;
                }
                if(grid[j][i] == 0)
                    he = false;
            }
        }

        for(int i = m-1;i >= 0;i--){
            boolean he = false;
            for(int j = n-1;j >= 0;j--){
                if(grid[j][i] == 1 && !he){
                    ans++;
                    he = true;
                }
                if(grid[j][i] == 0)
                    he = false;
            }
        }
        return ans;
    }
}
```

### LeetCode 701：二叉搜索树中的插入操作

#### 题目

[https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/)

给定二叉搜索树（BST）的根节点和要插入树中的值，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。 保证原始二叉搜索树中不存在新值。

注意，可能存在多种有效的插入方式，只要树在插入后仍保持为二叉搜索树即可。 你可以返回任意有效的结果。

#### 思路

递归插入，如果比左子树大，就插入右子树，如果比左子树小，就插入到左子树

#### 代码

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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);

    // insert into the right subtree
    if (val > root.val) root.right = insertIntoBST(root.right, val);
    // insert into the left subtree
    else root.left = insertIntoBST(root.left, val);
    return root;
    }
}
```


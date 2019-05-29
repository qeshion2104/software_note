# Algorithm Note

## Leetcode 461 Hamming Distance    
### res:
- [Hamming Distance definition](http://www.csie.ntnu.edu.tw/~u91029/Correction.html)
- [c++ 位元計算](https://openhome.cc/Gossip/CppGossip/LogicalBitwise.html)
### mysolution:
```C++
class Solution {
public:
    int hammingDistance(int x, int y) {
        int i = (x ^ y);
        int counter = 0;
        while (i != 0) {
            if (i&1) { counter++; }
            i = i >> 1;
        }
        return counter;
    }
};
```

## Leetcode 617. Merge Two Binary Trees
### res:
### mysolution:
```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        if (t1 == NULL && t2 == NULL) {
            return NULL;
        }
        else if (t1 == NULL) {
            t1 = new TreeNode(t2->val);
        }
        else if (t2 == NULL) {
            // do nothing
        }
        //  (t1 && t2)
        else {
            t1->val = t1->val + t2->val;
        }
        
        // if t2 not exist, we don't need to do anymore t1 will keep same
        if (t2 != NULL) {
            t1->left = mergeTrees(t1->left, t2->left);
            t1->right = mergeTrees(t1->right, t2->right);
        }
        
        return t1;
    }
};  
```
may clean like below (by answer):
```C++
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        if (t1 == NULL) {
            return t2;
        }
        else if (t2 == NULL) {
            return t1;
        }
        else {
            t1->val = t1->val + t2->val;
        }
        
        t1->left = mergeTrees(t1->left, t2->left);
        t1->right = mergeTrees(t1->right, t2->right);
        
        return t1;
    }
};  
```

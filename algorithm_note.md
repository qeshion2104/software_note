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

## Leetcode 728. Self Dividing Numbers

### res:
- [convert char to int](https://stackoverflow.com/questions/5029840/convert-char-to-int-in-c-and-c) 
- [convert int to string](https://stackoverflow.com/questions/5590381/easiest-way-to-convert-int-to-string-in-c)
### mysolution:
```C++
class Solution {
public:
    vector<int> selfDividingNumbers(int left, int right) {
        // use while get digit from % 10 every loop v /= 10; can get result more quickly
        vector<int> result = {};
        string str;
        bool is_divisible;
        for (int i = left; i <= right; i++) {
            str = to_string(i);
            is_divisible = true;
            for (char& c : str) {
                if (c == '0' || i % (c - '0') != 0) {
                    is_divisible = false;
                    break;
                }
            }
            if (is_divisible) {
                result.push_back(i);
            }
        }
        return result;
    }
};
```
## Leetcode 942. DI String Match
### res:
### mysolution:
```C++
class Solution {
public:
    vector<int> diStringMatch(string S) {
        
        int top = S.length();
        int lower = 0;
        vector<int> result;
        for (char& c : S) {
            if (c == 'D') {
                result.push_back(top--);
            } else {
                result.push_back(lower++);
            }
        }
        result.push_back(lower);
        return result;
    }
};
```
## Leetcode 852. Peak Index in a Mountain Array
### res:
### mysolution:
```C++
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& A) {
        // 2分搜索法
        int left_bound = 0;
        int right_bound = A.size();
        int index;
        while (true) {
            index = (left_bound + right_bound) / 2;
            if (index < A.size() - 1 && A[index] < A[index + 1]) {
                // go right
                left_bound = index;
            } else if (index > 0 && A[index] < A[index - 1]) {
                // go left
                right_bound = index;
            } else {
                break;
            }
        }
        return index;
    }
};
```

## Leetcode 933. Number of Recent Calls
### res:
- [C++ 容器介紹 queue](http://larry850806.github.io/2016/06/06/STL1/#queue)
### mysolution:
```C++
class RecentCounter {
    private:
        queue<int> q;
    public:
        RecentCounter() {}
        int ping(int t) {
            q.push(t);
            while (q.front() < (t - 3000)) {
                q.pop();
            }
            return q.size();
        }
};
```
## Leetcode 944. Delete Columns to Make Sorted
### res:
- [convert int to c](https://stackoverflow.com/questions/5029840/convert-char-to-int-in-c-and-c)
- [initialize vector with 0](https://stackoverflow.com/questions/13110130/initialize-a-vector-to-zeros-c-c11)
- [int to string](https://blog.csdn.net/xiaoquantouer/article/details/51746476)
### mysolution:
```C++
class Solution {
public:
    int minDeletionSize(vector<string>& A) {
        vector<int> max(A[0].size(), 0);
        int D = 0;
        for (int i = 0; i < A.size(); i++){
            for (int j = 0; j < A[i].size(); j++) {
                if (max[j] == -1) {
                    continue;
                }
                
                if (A[i][j] >= max[j]) {
                    max[j] = int(A[i][j]);
                } else {
                    max[j] = -1;
                    D++;
                }
            }
        }
        return D;
    }
};
```
## Leetcode 561. Array Partition I
### res:
- [sort](http://www.cplusplus.com/reference/algorithm/sort/)
### mysolution:
```C++
class Solution {
public:
    int arrayPairSum(vector<int>& nums) {
        // 2n to n pair
        // r1
        // after sorted
        // a[i] + a[i+2], ....
        sort(nums.begin(), nums.end());
        int r = 0;
        for (int i = 0; i < nums.size(); i = i+2) {
            r+=nums[i];
        }
        return r;
    }
};
```
## Leetcode 589. N-ary Tree Preorder Traversal
### res:
- [c++ vector concat](https://stackoverflow.com/questions/201718/concatenating-two-stdvectors)
### mysolution:
```C++
class Solution {
public:
    vector<int> preorder(Node* root) {
        vector<int> v;
        if (!!root) {
            // V
            v.push_back(root->val);
            // LR
            for (Node* child : root->children) {
                vector<int> temp = preorder(child);
                if (temp.size() > 0) {
                    v.insert(v.end(), make_move_iterator(temp.begin()), make_move_iterator(temp.end()));
                }
            }
        }
        return v;
    }
};
```


## Leetcode 965. Univalued Binary Tree
### res:
### mysolution:
```C++
class Solution {
public:
    bool isUnivalTree(TreeNode* root) {
        return isUniPreOrder(root, root->val);
    }
    bool isUniPreOrder(TreeNode* root, int val) {
        if (!root) {
            return true;
        } else {
            return root->val == val && isUniPreOrder(root->left, val) && isUniPreOrder(root->right, val);
        }
    }
};
```
## Leetcode 883. Projection Area of 3D Shapes
### res:
### mysolution:
```C++
class Solution {
public:
    int projectionArea(vector<vector<int>>& grid) {
        int xy = 0;
        int xz = 0;
        int yz = 0;
        int xz_max = 0;
        int yz_max = 0;
        // N X N
        for (int i = 0; i < grid.size(); i++) {
            int xz_max = 0;
            int yz_max = 0;
            for (int j = 0; j < grid[i].size(); j++) {
                if (grid[i][j] > 0) {
                    xy++;
                }
                if (grid[i][j] > xz_max) {
                    xz_max = grid[i][j];
                }
                if (grid[j][i] > yz_max) {
                    yz_max = grid[j][i];
                }
            }
            xz += xz_max;
            yz += yz_max;
        }
        return xy+xz+yz;
    }
};
```

## Leetcode 559. Maximum Depth of N-ary Tree
### res:
### mysolution:
```C++
class Solution {
public:
    int maxDepth(Node* root) {
        return helper(root, 1);
    }
    
    int helper(Node* root, int i) {
        if (!root) {
            return 0;
        }
        if (root->children.size() == 0) {
            return i;
        } else {
            int max=0;
            for (Node* child : root->children) {
                int j = helper(child, i+1);
                if (j > max) {
                    max = j;
                }
            }
            return max;
        }
    }    
};
```


## Leetcode XXX
### res:
- 111
### mysolution:
```C++
...
```

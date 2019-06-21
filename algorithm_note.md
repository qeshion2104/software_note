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
## Leetcode 908. Smallest Range I
### res:
### mysolution:
```C++
class Solution {
public:
    int smallestRangeI(vector<int>& A, int K) {
        // this is a problem about find min and max
        int min=10000;
        int max=0;
        for (int i: A) {
            if (i > max) max=i;
            if (i < min) min=i;
        }
        return max - min > 2 * K ? max - min - 2 * K : 0;
    }
};
```

## Leetcode 1030. Matrix Cells in Distance Order
### res:
### mysolution:
```C++
// 參考別人code 後 得出的答案 當然 並不是最快的
        // 由中心向外擴展的算法 就只需要 O(MN) 次 搭配visted 陣列 可以寫出更clean的code
    vector<vector<int>> allCellsDistOrder(int R, int C, int r0, int c0) {
        vector<vector<int>> matrix;
        for (int i=0; i<R; i++) {
            for (int j=0; j<C; j++) {
                matrix.push_back({i, j});
            }
        }
        // from smallest distance to largest distance
        // refer variable outside function
        auto comp = [&r0, &c0](const vector<int>& v1, const vector<int>& v2) {
            return abs(v1[0] - r0) + abs(v1[1] - c0) < abs(v2[0] - r0) + abs(v2[1] - c0);
        };
        sort( matrix.begin( ), matrix.end( ), comp);
        
        return matrix;
    }
```

## Leetcode 811. Subdomain Visit Count
### res:
- [Easiest way to convert int to string in C++](   https://stackoverflow.com/questions/5590381/easiest-way-to-convert-int-to-string-in-cParse)
- [(split) a string in C++ using string delimiter (standard C++):](https://stackoverflow.com/questions/14265581/parse-split-a-string-in-c-using-string-delimiter-standard-c)
- [How to convert string to int and int to string in C++:](https://www.systutorials.com/131/convert-string-to-int-and-reverse/)
- [Find xth character in string:](http://www.cplusplus.com/forum/beginner/145368/)
- [How to lterate over a map in c++: ](https://thispointer.com/how-to-iterate-over-a-map-in-c/)
### mysolution:
```C++
class Solution {
public:
    vector<string> subdomainVisits(vector<string>& cpdomains) {
        map<string, int> myMap;
        vector<string> res;
        size_t pos = 0;
        for (string & str : cpdomains) {
            // spilt number and domain by space
            pos = str.find(" ");
            int number = stoi(str.substr(0, pos));
            str.erase(0, pos + 1);
            
            // separate domain with .        
            pos = 0;
            do {
                if (pos != 0) {
                    str.erase(0, pos + 1);
                }
                // insert or update domain in Map
                myMap[str] = myMap[str] ? myMap[str] + number : number;     
            }
            while ( (pos = str.find(".")) != string::npos );
        }
        // convert myMap to vector [key, value]
        for ( const auto &myPair : myMap ) {
            res.push_back(to_string(myPair.second) + " " + myPair.first);
        }
        
        return res;
    }
};
```

## Leetcode 700   Search in a Binary Search Tree
### res:
- [queue:](https://blog.csdn.net/u012539514/article/details/17751123)
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
    TreeNode* searchBST(TreeNode* root, int val) {
//         // use BFS
//         queue<TreeNode *> q;
//         q.push(root);
//         TreeNode * cur = nullptr;
//         while (!q.empty()) {
//             cur = q.front();
//             q.pop();
//             if (cur != nullptr) {
//                 if (cur->val == val) {
//                     break;
//                 } else {
//                     q.push(cur->left);
//                     q.push(cur->right);
//                 }
//             } else {
//                 // do nothing
//             }
//         }
//         if (cur == nullptr) {
//             return NULL;
//         } else {
//             return cur;
//         }
        
        // more powerful way to use feture about BST
        if (!root) return NULL;
        if (root->val == val) return root;
        else if (root->val > val) return searchBST(root->left, val);
        else return searchBST(root->right, val);
    }
};
```

## Leetcode 1046. Last Stone Weight
### res:
- [priority_queue](http://nckunoname.pixnet.net/blog/post/79316741-stl%E7%9A%84priority_queue%E7%9A%84%E7%94%A8%E6%B3%95)
### mysolution:
```C++
class Solution {
public:
    int lastStoneWeight(vector<int>& stones) {
        priority_queue<int> q;
        for (auto i: stones) {
            q.push(i);
        }
        while(q.size() >= 2) {
            int first = q.top();
            q.pop();
            int second = q.top();
            q.pop();
            if (first != second) {
                q.push(first-second);
            }
        }
        return !q.empty() ? q.top() : 0;
    }
};
```
## Leetcode 669. Trim a Binary Search Tree
### res:
### mysolution:
```C++
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int L, int R) {
            
        if (root == NULL) {
            return NULL;
        }
        
        if (check(root->val, L, R)) {
            // pass
            // go right
            root->left = trimBST(root->left, L, R);
            // go left
            root->right = trimBST(root->right, L, R);
            return root;
        } else {
            // not pass
            // if < L return R
            if (root->val < L) {
                return trimBST(root->right, L, R);
            }
            // else > R return left return L
            else return trimBST(root->left, L, R);
        }
    }
    
    bool check(int val, int L, int R) {
        return val >= L && val <= R;
    }
};


=== can be simplyfy to ===
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int L, int R) {
            
        if (root == NULL) return NULL;
        
        if (root->val < L) return trimBST(root->right, L, R);
        if (root->val > R ) return trimBST(root->left, L, R);
        
        root->left = trimBST(root->left, L, R);
        root->right = trimBST(root->right, L, R);
        return root;
    }
};
```


## Leetcode 136. Single Number
### res:
- [c++ unorder_set](https://www.sczyh30.com/posts/C-C/cpp-stl-hashmap/)
- [c++ unorder_set](http://www.cplusplus.com/reference/unordered_map/unordered_map/begin/)
- [c++ vector to set](https://www.techiedelight.com/convert-vector-set-cpp/)
- [c++ 位元運算](http://www.86duino.com/?p=1411&lang=TW)
### mysolution:
```C++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        // Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
        // must be O(N) and space with O(1)
        // hmm....
        // so we can not sort then scan ...
        
        
        // r1  for loop O(N) find= O(1) t = O(N)
        //     space for unorder_map = O(N)
        // unordered_map<int, int> umap;
        // for (int i: nums) {
        //     if (umap.find(i) == umap.end()) umap[i]=i;
        //     else umap.erase(i);
        // }
        // auto it = umap.begin();
        // return it->first;
        
        // r2 purely math solution ( a + b + c ) * 2 - ( a + b + c + a + b) = c
        // for loop O(N) and sum O(N) = O(2N)
        // space O(N) set
        // unordered_set<int> uset;
        // int sum=0;
        // for (int i: nums) {
        //     sum+=i;
        //     uset.insert(i);
        // }
        // int s_sum = 0;
        // for (const int& i: uset) {
        //     s_sum += i;
        // }
        // return s_sum * 2 - sum;
        
        // awsome r3 use Bit Manipulation
        // XOR  a XOR 0 = a
        //      a XOR a = 0
        //      a XOR b XOR a = (a XOR a) XOR b = 0 XOR b = b
        // so we can loop and XOR all bits together to find answer
        // TIME = O(N) and SPACE= O(1)
        
        int sum = 0;
        for (int i: nums) {
            sum ^= i;
        }
        return sum;
    }
};
```


## Leetcode 575. Distribute Candies
### res:
### mysolution:
```C++
class Solution {
public:
    int distributeCandies(vector<int>& candies) {
        // candies.size() % 2 = 0;
        // devide in to two side
        // and must be max kind sister could get
        // so the logic is here
        // divide into to group A, B
        // A has much distinct Type as possible, and the other for B
        // the max type is equal to candies.size() / 2 < sumType ? candies.size() / 2 : sumType;
        int sumType = 0;
        unordered_set<int> u_set;
        for (int i: candies) {
            if (u_set.find(i) == u_set.end()) {
                u_set.insert(i);
                sumType++;
            }
        }
        int size_2 = candies.size() / 2;
        return min(size_2, sumType);
    }
};
```


## Leetcode 496. Next Greater Element I
### res:
### mysolution:
```C++
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        // r1 brute force
        // time O(n^2) space O(1)
        for (int i=0; i < nums1.size(); i++) {
            bool findIndex = false;
            bool isSet = false;
            for (int j=0; j < nums2.size(); j++) {
                if (findIndex && nums2[j] > nums1[i]) {
                    nums1[i] = nums2[j];
                    isSet = true;
                    break;
                } else if (nums1[i] == nums2[j]) {
                    findIndex = true;
                }
            }
            if (!isSet) {
                nums1[i] = -1;
            }
        }
        return nums1;
        
        // r2 store index first for O(n) and loop for O(1/2n^2)
        //      space = O(n)
        unordered_map<int, int> index_map;
        for (int i=0; i < nums2.size(); i++) {
            index_map[nums2[i]] = i;
        }
        
        for (int& j: nums1) {
            int index = index_map[j];
            bool isSet = false;
            for (int k=index; k < nums2.size(); k++) {
                if (j < nums2[k]) {
                    j = nums2[k];
                    isSet = true;
                    break;
                }
            }
            if (!isSet) {
                j = -1;
            }
        }
        return nums1;
        
        // r3 use stack and map caluate great first
        
        unordered_map<int, int> res;
        stack<int> st;
        for (int i:  nums2) {
            int cur = i;
            // scan until empty or !> top, leave only numbe smaller than cur
            while(!st.empty() && cur > st.top()) {
                res[st.top()] = cur;
                st.pop();
            }
            st.push(cur);
        }
        // get answer if count not exist mean no great next
        for (int &i : nums1) {
            i = res.count(i) ? res[i] : -1;
        }
        return nums1;
    }
};
```
## Leetcode 412 Fizz Buzz
### res:
### mysolution:
```C++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> vs;
        for (int i = 1; i <= n; i++) {
            if (i % 3 == 0 && i % 5 == 0) {
                vs.push_back("FizzBuzz");
            } else if (i % 3 ==0) {
                vs.push_back("Fizz");
            } else if (i % 5 ==0) {
                vs.push_back("Buzz");
            } else {
                vs.push_back(int2str(i));
            } 
        }
        return vs;
    }
    string int2str(int &i) {
      string s;
      stringstream ss(s);
      ss << i;

      return ss.str();
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

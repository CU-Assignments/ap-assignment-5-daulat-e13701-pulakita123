[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/0Zzlu9gw)
# AP-ASSIGNMENT-5-DAULAT-E13701
TREE
https://leetcode.com/problems/maximum-depth-of-binary-tree/
```
#include <iostream>
using namespace std;

class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr)
            return 0;
        
        int leftDepth = maxDepth(root->left);
        int rightDepth = maxDepth(root->right);
        
        return max(leftDepth, rightDepth) + 1;
    }
};

```
![image](https://github.com/user-attachments/assets/8d41c24b-d342-4305-8411-ace825e53d42)


https://leetcode.com/problems/validate-binary-search-tree/
```
#include <iostream>
#include <limits>

using namespace std;

class Solution {
public:
    bool isValidBST(TreeNode* root, long minVal = LONG_MIN, long maxVal = LONG_MAX) {
        if (root == nullptr) 
            return true;
        
        if (root->val <= minVal || root->val >= maxVal) 
            return false;
        
        return isValidBST(root->left, minVal, root->val) &&
               isValidBST(root->right, root->val, maxVal);
    }
};

```
![image](https://github.com/user-attachments/assets/ea51f716-c3c4-41d5-ba69-c52f3c7387c4)

https://leetcode.com/problems/symmetric-tree/
```
#include <iostream>

using namespace std;

class Solution {
public:
    bool isMirror(TreeNode* t1, TreeNode* t2) {
        if (!t1 && !t2) return true;  // Both nodes are null
        if (!t1 || !t2) return false; // Only one node is null
        
        return (t1->val == t2->val) &&
               isMirror(t1->left, t2->right) &&
               isMirror(t1->right, t2->left);
    }

    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        return isMirror(root->left, root->right);
    }
};

```
![image](https://github.com/user-attachments/assets/a0e85a72-36cb-401a-a4da-8e728954d553)

https://leetcode.com/problems/binary-tree-level-order-traversal/
```
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if (!root) return result;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int levelSize = q.size();
            vector<int> level;

            for (int i = 0; i < levelSize; i++) {
                TreeNode* node = q.front();
                q.pop();
                level.push_back(node->val);

                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            result.push_back(level);
        }
        return result;
    }
};

```
![image](https://github.com/user-attachments/assets/d4948d55-b93c-4936-8d3b-f5ae2d7630b8)

https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/
```
#include <iostream>
#include <vector>

using namespace std;

class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums, int left, int right) {
        if (left > right) return nullptr; // Base case: return null if invalid range

        int mid = left + (right - left) / 2; // Middle element to keep tree balanced
        TreeNode* root = new TreeNode(nums[mid]); // Create root node

        root->left = sortedArrayToBST(nums, left, mid - 1);  // Recursively build left subtree
        root->right = sortedArrayToBST(nums, mid + 1, right); // Recursively build right subtree

        return root;
    }

    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return sortedArrayToBST(nums, 0, nums.size() - 1);
    }
};

```
![image](https://github.com/user-attachments/assets/116235c3-9b8a-4580-bc34-3d3f9879a5ed)

https://leetcode.com/problems/binary-tree-inorder-traversal/
```
#include <iostream>
#include <vector>

using namespace std;

class Solution {
public:
    void inorder(TreeNode* root, vector<int>& result) {
        if (root == nullptr) return;
        
        inorder(root->left, result);   // Traverse left subtree
        result.push_back(root->val);   // Visit root
        inorder(root->right, result);  // Traverse right subtree
    }

    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        inorder(root, result);
        return result;
    }
};

```
![image](https://github.com/user-attachments/assets/9da8260f-e2a4-4139-bfd3-ce204a257033)

https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
```
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

class Solution {
public:
    unordered_map<int, int> inorderIndexMap; // Hash map to store index of elements in inorder

    TreeNode* buildTreeHelper(vector<int>& inorder, vector<int>& postorder, 
                              int inStart, int inEnd, int& postIndex) {
        if (inStart > inEnd) return nullptr;

        int rootVal = postorder[postIndex--]; // Get root from postorder
        TreeNode* root = new TreeNode(rootVal); // Create root node

        int inIndex = inorderIndexMap[rootVal]; // Find root position in inorder

        // Build right subtree first (because postorder visits left -> right -> root)
        root->right = buildTreeHelper(inorder, postorder, inIndex + 1, inEnd, postIndex);
        root->left = buildTreeHelper(inorder, postorder, inStart, inIndex - 1, postIndex);

        return root;
    }

    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int n = inorder.size();
        int postIndex = n - 1; // Start from last element of postorder

        // Store inorder values and their indices in a hash map for quick lookup
        for (int i = 0; i < n; i++)
            inorderIndexMap[inorder[i]] = i;

        return buildTreeHelper(inorder, postorder, 0, n - 1, postIndex);
    }
};

```
![image](https://github.com/user-attachments/assets/170471ac-dcd6-4afe-925f-aefdc245686c)


https://leetcode.com/problems/kth-smallest-element-in-a-bst/
```
#include <iostream>
#include <vector>

using namespace std;

class Solution {
public:
    void inorder(TreeNode* root, vector<int>& elements) {
        if (!root) return;

        inorder(root->left, elements);   // Left subtree
        elements.push_back(root->val);   // Visit node
        inorder(root->right, elements);  // Right subtree
    }

    int kthSmallest(TreeNode* root, int k) {
        vector<int> elements;
        inorder(root, elements);
        return elements[k - 1];  // k-th smallest element (1-based index)
    }
};

```
![image](https://github.com/user-attachments/assets/c1f61c03-ff41-45c6-9a1e-54f5bef90a6d)

https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
```
#include <iostream>
#include <queue>

using namespace std;
struct Node;

class Solution {
public:
    Node* connect(Node* root) {
        if (!root) return nullptr;  // If tree is empty, return null
        
        queue<Node*> q;
        q.push(root);

        while (!q.empty()) {
            int levelSize = q.size();  // Number of nodes at current level

            for (int i = 0; i < levelSize; i++) {
                Node* node = q.front();
                q.pop();

                // Connect to the next node in the same level, except for the last node
                if (i < levelSize - 1) {
                    node->next = q.front();
                }

                // Push children into queue for the next level
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
        }

        return root;
    }
};

```
![image](https://github.com/user-attachments/assets/ec986af4-9045-452f-8581-02599d930b4e)


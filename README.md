#include <stdio.h>
#include <stdlib.h>


struct TreeNode {
    int val;
    struct TreeNode* left;
    struct TreeNode* right;
};

struct TreeNode* createNode(int value) {
    struct TreeNode* newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    newNode->val = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}


int isLeaf(struct TreeNode* node) {
    return node != NULL && node->left == NULL && node->right == NULL;
}


int sumOfLeftLeaves(struct TreeNode* root) {
    if (root == NULL) return 0;

    int sum = 0;

    
    if (root->left && isLeaf(root->left)) {
        sum += root->left->val;
    }
    
    
    sum += sumOfLeftLeaves(root->left);
    sum += sumOfLeftLeaves(root->right);

    return sum;
}


int main() {
   
    struct TreeNode* root = createNode(5);
    root->left = createNode(2);
    root->right = createNode(7);
    root->right->left = createNode(6);
    root->right->right = createNode(8);
    
    int result = sumOfLeftLeaves(root);
    printf("Sum of all left leaves: %d\n", result);

    return 0;
}

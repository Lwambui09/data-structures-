#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

struct Node* insert(struct Node* root, int data) {
    if (root == NULL)
        return createNode(data);
    if (data < root->data)
        root->left = insert(root->left, data);
    else if (data > root->data)
        root->right = insert(root->right, data);
    return root;
}

struct Node* createBST(int arr[], int size) {
    struct Node* root = NULL;
    for (int i = 0; i < size; i++) {
        root = insert(root, arr[i]);
    }
    return root;
}

int main() {
    int arr[] = {30, 20, 40, 10, 25, 35, 45, 5, 15};
    int size = sizeof(arr) / sizeof(arr[0]);
    
    struct Node* root = createBST(arr, size);

    return 0;
}

struct Node* minValueNode(struct Node* node) {
    struct Node* current = node;
    while (current && current->left != NULL)
        current = current->left;
    return current;
}

struct Node* deleteNode(struct Node* root, int key) {
    if (root == NULL)
        return root;
    if (key < root->data)
        root->left = deleteNode(root->left, key);
    else if (key > root->data)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == NULL) {
            struct Node* temp = root->right;
            free(root);
            return temp;
        }
        else if (root->right == NULL) {
            struct Node* temp = root->left;
            free(root);
            return temp;
        }
        struct Node* temp = minValueNode(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}

int main() {
    
    int key_to_delete = 25;

    root = deleteNode(root, key_to_delete);

    return 0;
}

int height(struct Node* root) {
    if (root == NULL)
        return -1;
    int leftHeight = height(root->left);
    int rightHeight = height(root->right);
    return (leftHeight > rightHeight) ? leftHeight + 1 : rightHeight + 1;
}

int main() {
   
    printf("Height of the BST is: %d\n", height(root));

    
    return 0;
}
 
void printLevelAndHeight(struct Node* root, int key, int level) {
    if (root == NULL)
        return;
    if (root->data == key) {
        printf("Level of node %d is: %d\n", key, level);
        printf("Height of node %d is: %d\n", key, height(root));
        return;
    }
    printLevelAndHeight(root->left, key, level + 1);
    printLevelAndHeight(root->right, key, level + 1);
}

int main() {

    int node_to_check = 10;
    
    printLevelAndHeight(root, node_to_check, 0);

  
    return 0;
}

# DS-15
DS code
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *left, *right;
};

struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

struct Node* insert(struct Node* root, int data) {
    if (root == NULL) return createNode(data);
    if (data < root->data)
        root->left = insert(root->left, data);
    else if (data > root->data)
        root->right = insert(root->right, data);
    return root;
}

void printRange(struct Node* root, int low, int high) {
    if (root == NULL) return;
    if (root->data > low) printRange(root->left, low, high);
    if (root->data >= low && root->data <= high) printf("%d ", root->data);
    if (root->data < high) printRange(root->right, low, high);
}

int main() {
    struct Node* root = NULL;
    int n, val, low, high;
    printf("Enter number of nodes: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        printf("Enter value: ");
        scanf("%d", &val);
        root = insert(root, val);
    }
    printf("Enter range (low high): ");
    scanf("%d %d", &low, &high);
    printf("Nodes in range [%d, %d]: ", low, high);
    printRange(root, low, high);
    printf("\n");
    return 0;
}

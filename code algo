#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    int key;
    struct node *left;
    struct node *right;
} Node;

// ====== Create Node ======
Node* createNode(int key) {
    Node* newNode = (Node*) malloc(sizeof(Node));
    newNode->key = key;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// ====== Size ======
int size(Node* root) {
    if (root == NULL) {
        return 0;
    }
    int leftSize = size(root->left);
    int rightSize = size(root->right);
    int total = 1 + leftSize + rightSize;
    return total;
}

// ====== Height ======
int height(Node* root) {
    if (root == NULL) {
        return -1;
    }
    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    int maxHeight;
    if (leftHeight > rightHeight) {
        maxHeight = leftHeight;
    } else {
        maxHeight = rightHeight;
    }

    return 1 + maxHeight;
}

// ====== Average Leaf Depth (PME) ======
void sumLeaves(Node* root, int depth, int* sum, int* count) {
    if (root == NULL) return;

    if (root->left == NULL && root->right == NULL) {
        *sum += depth;
        *count += 1;
    }

    sumLeaves(root->left, depth + 1, sum, count);
    sumLeaves(root->right, depth + 1, sum, count);
}

float pme(Node* root) {
    int sum = 0;
    int count = 0;

    sumLeaves(root, 0, &sum, &count);

    if (count == 0) return 0;
    return (float)sum / count;
}

// ====== Max Path ======
int maxpath(Node* root) {
    if (root == NULL) return 0;

    int left = maxpath(root->left);
    int right = maxpath(root->right);

    int biggest;
    if (left > right) {
        biggest = left;
    } else {
        biggest = right;
    }

    return root->key + biggest;
}

// ====== DFS (Print Tree Structure) ======
void dfs(Node* root) {
    if (root == NULL) {
        printf("_");
        return;
    }

    printf("<%d,", root->key);
    dfs(root->left);
    printf(",");
    dfs(root->right);
    printf(">");
}

// ====== BFS (Level Order Traversal) ======

// Simple Queue
#define MAX 100

typedef struct {
    Node* data[MAX];
    int front;
    int rear;
} Queue;

void initQueue(Queue* q) {
    q->front = 0;
    q->rear = 0;
}

int isEmpty(Queue* q) {
    return q->front == q->rear;
}

void enqueue(Queue* q, Node* node) {
    q->data[q->rear++] = node;
}

Node* dequeue(Queue* q) {
    return q->data[q->front++];
}

void bfs(Node* root) {
    if (root == NULL) return;

    Queue q;
    initQueue(&q);
    enqueue(&q, root);

    while (!isEmpty(&q)) {
        Node* current = dequeue(&q);
        printf("%d ", current->key);

        if (current->left != NULL) {
            enqueue(&q, current->left);
        }

        if (current->right != NULL) {
            enqueue(&q, current->right);
        }
    }
}

// ====== Width (Max Nodes on Any Level) ======
int width(Node* root) {
    if (root == NULL) return 0;

    Queue q;
    initQueue(&q);
    enqueue(&q, root);
    enqueue(&q, NULL);  // Level marker

    int widthNow = 0;
    int maxWidth = 0;

    while (!isEmpty(&q)) {
        Node* current = dequeue(&q);

        if (current == NULL) {
            if (widthNow > maxWidth) {
                maxWidth = widthNow;
            }
            widthNow = 0;

            if (!isEmpty(&q)) {
                enqueue(&q, NULL);
            }
        } else {
            widthNow += 1;

            if (current->left != NULL) {
                enqueue(&q, current->left);
            }

            if (current->right != NULL) {
                enqueue(&q, current->right);
            }
        }
    }

    return maxWidth;
}

// ====== Main Function ======
int main() {
    Node* root = createNode(5);
    root->left = createNode(3);
    root->right = createNode(8);
    root->left->left = createNode(1);
    root->left->right = createNode(4);
    root->right->right = createNode(9);

    printf("Size: %d\n", size(root));
    printf("Height: %d\n", height(root));
    printf("Max Path Sum: %d\n", maxpath(root));
    printf("PME (Average Leaf Depth): %.2f\n", pme(root));

    printf("DFS: ");
    dfs(root);
    printf("\n");

    printf("BFS: ");
    bfs(root);
    printf("\n");

    printf("Width: %d\n", width(root));

    return 0;
}

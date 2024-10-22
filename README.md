# 2024090914022-赖伊卡-cs-02
## 常用数据结构类型
1. 随机存取指的是从一组数据元素中访问任意元素所需的时间与该元素在存储介质中的物理位置无关。也就是可以直接定位到存储介质上的任意位置进行数据的读写操作，而无需遍历或搜索前面的元素。

   数组
2. 指针代表了一个内存地址，这个地址指向了计算机内存中的某个特定位置。通过指针，程序就可以间接地操作和访问存储在该位置的数据。
3. 数组：当需要快速访问元素，且元素的数量在编译时已知或大致确定时。例如，存储班级中所有学生的成绩。
   
   链表：当数据集合的大小频繁变化，或者需要经常在集合中间插入或删除元素时。例如，实现一个动态数组或栈。
   
   栈：需要后进先出的数据处理顺序时。例如，函数调用栈、撤销操作、括号匹配等。
   
   队列：需要先进先出的数据处理顺序时。例如，任务调度、缓冲区管理、页面置换算法等。
   
   图：表示复杂的关系网络，如社交网络、交通网络、计算机网络等。

4.ff
## 数据结构的应用
1.
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node 
{
    int data;       
    struct Node* next;
} Node;

Node* createNode(int d) 
{
    Node* newNode = malloc(sizeof(Node)); 
    if (newNode == NULL) 
    {
        printf("失败\n");
        exit(1); 
    }
    newNode->data = d;
    newNode->next = NULL;
    return newNode;
}

void addfront(Node** head, int d) 
{
    Node* newNode = createNode(d);
    
    newNode->next = *head;
    *head=newNode;
}

void addbehind(Node** head, int d) 
{
    if (*head == NULL) 
    {
        *head = createNode(d);
        return;
    }

    Node* tail = *head;
    while(tail->next!=NULL)
    {
        tail=tail->next;
    }
    Node* newNode = createNode(d);
    tail->next = newNode; 
}

void delete(Node** head, int n) 
{
    if (*head == NULL)
    {
        return;
    }

    if (n == 1) 
    {
        Node* temp = *head;
        *head = (*head)->next;
        free(temp); 
        return;
    }

    Node* current = *head;
    Node* pre = NULL;
    if (current == NULL) {
        return;
    }
    for (int i = 1; i < n; ++i) 
    {
        pre = current;
        current = current->next;
    }

        pre->next = current->next;

    free(current); 
}

void collect(Node** head) 
{
    if (*head == NULL || (*head)->next == NULL) 
    {
    
        return;
    }

    Node* tail = *head;
    while (tail->next != NULL) 
    {
        tail = tail->next;
    }
    tail->next = *head;
}

void print(Node* head) 
{
    Node* current = head;
    if (head == NULL) {
        printf("链表为空\n");
        return;
    }
    if (current->next == head) 
    {

        printf("%d\n", current->data);
        return;
    }
    while (current->next!= head)
    {
        printf("%d ", current->data);
        current = current->next; 
    }
    printf("%d\n",current->data);
}

#define H addfront
#define T addbehind
#define D delete
#define C collect
#define P print

int main()
{
    Node*head=createNode(1);
    T(&head,1);T(&head,1);T(&head,1);
    H(&head,1);H(&head,2);H(&head,3);
    T(&head,1);T(&head,3);T(&head,1);
    D(&head,9);
    H(&head,1);H(&head,2);H(&head,1);
    T(&head,2);T(&head,2);T(&head,2);
    H(&head,2);H(&head,1);H(&head,2);
    D(&head,1);
    H(&head,1);H(&head,2);H(&head,2);
    T(&head,1);T(&head,2);T(&head,2);
    D(&head,23);
    T(&head,2);T(&head,1);T(&head,1);
    T(&head,2);T(&head,2);T(&head,2);
    H(&head,1);H(&head,2);H(&head,1);
    H(&head,1);H(&head,1);H(&head,1);
    C(&head);
    P(head);
    return 0;
}
```
![image](https://github.com/Taylor-Lai/2024090914022-laiyika-CS-02/blob/main/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-22%20173727.png)


2.
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node 
{
    int data;       
    struct Node* next;
} Node;

Node* createNode(int d) 
{
    Node* newNode = malloc(sizeof(Node)); 
    if (newNode == NULL) 
    {
        printf("失败\n");
        exit(1); 
    }
    newNode->data = d;
    newNode->next = NULL;
    return newNode;
}

void addfront(Node** head, int d) 
{
    Node* newNode = createNode(d);
    
    newNode->next = *head;
    *head=newNode;
}

void addbehind(Node** head, int d) 
{
    if (*head == NULL) 
    {
        *head = createNode(d);
        return;
    }

    Node* tail = *head;
    while(tail->next!=NULL)
    {
        tail=tail->next;
    }
    Node* newNode = createNode(d);
    tail->next = newNode; 
}

void delete(Node** head, int n) 
{
    if (*head == NULL)
    {
        return;
    }

    if (n == 1) 
    {
        Node* temp = *head;
        *head = (*head)->next;
        free(temp); 
        return;
    }

    Node* current = *head;
    Node* pre = NULL;
    if (current == NULL) {
        return;
    }
    for (int i = 1; i < n; ++i) 
    {
        pre = current;
        current = current->next;
    }

        pre->next = current->next;

    free(current); 
}

void collect(Node** head) 
{
    if (*head == NULL || (*head)->next == NULL) 
    {
    
        return;
    }

    Node* tail = *head;
    while (tail->next != NULL) 
    {
        tail = tail->next;
    }
    tail->next = *head;
}

void print(Node* head) 
{
    Node* current = head;
    if (head == NULL) {
        printf("链表为空\n");
        return;
    }
    if (current->next == head) 
    {

        printf("%d\n", current->data);
        return;
    }
    while (current->next!= head)
    {
        printf("%d ", current->data);
        current = current->next; 
    }
    printf("%d\n",current->data);
}

void josephus(Node** head, int m) 
{
    int n;
    if (!head || !*head || !(*head)->next || *head == (*head)->next)
    return;

    FILE* fp = fopen("Josephus.out", "w");
    if (!fp) 
    {
        perror("Failed to open file");
        return;
    }

    Node* prev = NULL;
    Node* current = *head;

    while (current->data != 3) 
    {
        prev = current;
        current = current->next;
    }

    n=m;
    while (current != current->next) 
    { 
        for (int count = 1; count < n; count++) 
        {
            prev = current;
            current = current->next;
            if (current == current->next) break;
        }
        prev->next = current->next;
        fprintf(fp, "%d ", current->data);
        free(current);
        current = prev->next;
        n++;
    }

    { 
        fprintf(fp, "%d ", current->data);
        free(current);
    }

    *head = NULL;
    fclose(fp);
}
#define H addfront
#define T addbehind
#define D delete
#define C collect
#define P print
#define J josephus
int main()
{
    Node*head=createNode(1);
    T(&head,1);T(&head,1);T(&head,1);
    H(&head,1);H(&head,2);H(&head,3);
    T(&head,1);T(&head,3);T(&head,1);
    D(&head,9);
    H(&head,1);H(&head,2);H(&head,1);
    T(&head,2);T(&head,2);T(&head,2);
    H(&head,2);H(&head,1);H(&head,2);
    D(&head,1);
    H(&head,1);H(&head,2);H(&head,2);
    T(&head,1);T(&head,2);T(&head,2);
    D(&head,23);
    T(&head,2);T(&head,1);T(&head,1);
    T(&head,2);T(&head,2);T(&head,2);
    H(&head,1);H(&head,2);H(&head,1);
    H(&head,1);H(&head,1);H(&head,1);
    C(&head);
    P(head);
    J(&head,1);
    return 0;
}
```
![image](https://github.com/Taylor-Lai/2024090914022-laiyika-CS-02/blob/main/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-22%20174949.png)
![image](https://github.com/Taylor-Lai/2024090914022-laiyika-CS-02/blob/main/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-22%20174936.png)

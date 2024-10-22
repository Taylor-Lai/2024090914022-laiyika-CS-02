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


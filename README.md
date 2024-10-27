# 2024090914022-赖伊卡-cs-02
## 常用数据结构类型
1. 随机存取指的是从一组数据元素中访问任意元素所需的时间与该元素在存储介质中的物理位置无关。也就是可以直接定位到存储介质上的任意位置进行数据的读写操作，而无需遍历或搜索前面的元素。

   数组
2. 指针代表了一个内存地址，这个地址指向了计算机内存中的某个特定位置。通过指针，程序就可以间接地操作和访问存储在该位置的数据。
3. 数组：存储班级中同学的成绩。
   
   链表：医院叫号，有人离开了就可以实时的删除这个“节点”。
   
   栈：浏览器界面的返回，利用就可以返回上一个最近访问的界面。
   
   队列：打印机等，先处理先提供的文件。
   
   图：社交网络分析，就像QQ会根据你的朋友网推送你可能想认识的人，还有短视频平台，根据你的喜好精准推送，等等。

5.

  （1）直接解析图片文件的格式来了解图片的存储结构和编码方式。
  
  （2）定义一个结构体来包括该图片的基本信息。
  
  （3）用fopen函数打开准备好接收的文件，来存储图片信息。
  
  （4）利用fwrite将各个参数的结构体变量存储到目标文件中。
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
    if (current == NULL)
    {
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
    if (head == NULL)
    {
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

3.
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

#define MAX_SIZE 50

typedef struct 
{
    char items[MAX_SIZE];
    int top; 
} Stack;

void first(Stack *s) 
{
    s->top = -1;
}

bool ifEmpty(Stack *s) 
{
    return s->top == -1;
}

bool push(Stack *s, char item) 
{
    if (s->top == MAX_SIZE - 1) 
    { 
        return 0;
    }
    s->items[++s->top] = item;
    return 1;
}

char pop(Stack *s) {
    if (ifEmpty(s)) 
    {
        printf("空\n");
        return 'p';
    }
    return s->items[s->top--]; 
}

int main() 
{
    Stack s;
    first(&s);
    char zifuzu[] = "kiglnmrmeiahenrteof4ardar";
    char shuzizu[] = "3112212112122112211221122112111112";
    int i, j, a = 0;

    for (i = 0; i < strlen(shuzizu); i++)
    {
        int count = shuzizu[i] - '0';

        if (i % 2 == 0)
        {
            for (j = 0; j < count && a < strlen(zifuzu); j++)
            {
                push(&s, zifuzu[a++]);
            }
        }
        else
        {
            for (j = 0; j < count && !ifEmpty(&s); j++)
            {
                char poppedChar = pop(&s);
                printf("%c", poppedChar);
            }
        }
    }
    printf("\n");
    return 0;
}
```
![image](https://github.com/Taylor-Lai/2024090914022-laiyika-CS-02/blob/main/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-22%20185003.png)


最终的答案是：glimmerinheartnofear4dark

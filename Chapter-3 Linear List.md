#### 抽象数据类型定义

```
ADT List
Data 
	数据集合为{a1,a2,...an}，每个数据类型均为DataType。数据元素之间的关系为一对一，除首位外。
Operation
	InitList(*L): 初始化，建立一个空的List
    ListEmpty(L): 检测表是否为空
    ClearList(*L): 清空
    GetElem(L, i, *e):
    LocateElem(L, e):
    ListInsert(*L, i, e):
    ListDel(*L, i, *e):
    ListLen(L):
endADT
```

#### 顺序存储结构

```c
#define MAX_SIZE 20
typedef int ElemType;
typedef struct{
    ElemType data[MAX_SIZE];
    int length;
}sqList;
```

存取时间性能为O(1)

增删查改

* 判断位置是否正常
* 取出、添加元素
* 改变表长

优点：

* 无须为表示表中元素之间的逻辑关系而增加额外的存储空间

* 可以快速地存取表中任一位置的元素

缺点：

* 插入和删除操作需要移动大量元素
* 当线性表长度变化较大时，难以确定存储空间的容量
* 造成存储空间的“碎片”

#### 链式存储结构

为了表示每个数据元素ai与其直接后继数据元素ai+1之间的逻辑关系，对数据元素a来说，除了存储其本身的信息之外，还需存储一个指示其直接后继的信息
（即直接后继的存储位置）。我们把存储数据元素信息的域称为数据域，把存储直接后继位置的域称为指针域。指针域中存储的信息称做指针或链。这两部分信息组成数据元素ai的存储映像，称为结点（Node）。

n个结点（ai的存储映像）链结成一个链表，即为线性表（a1，a2，.，an）的链式存储结构，因为此链表的每个结点中只包含一个指针域，所以叫做单链表。

最后一个节点指向“空”，即NULL

有时，我们为了更加方便地对链表进行操作，会在单链表的第一个结点前附设一个结点，称为头结点。头结点的数据域可以不存储任何信息，谁叫它是第一个呢，有这个特权。也可以存储如线性表的长度等附加信息，头结点的指针域存储指向第一个结点的指针。

```c
typedef struct Node{
    ElemType data;
    struct Node *next;
} Node;
typedef struct Node *LinkList;
```

```c
Status GetElem(LinkList L, int i, ElemType *e)
{
	int j;
	LinkList p;
    p = L->next;
    j = 1;
    while(p && j < i)
    {
        p = p->next;
        ++i;
    }
    if (!p || j > i)
        return ERR;
    *e = p->data;
    return TRUE;
}
```

```c
Status ListInsert(LinkList *L, int i, ElemType e)
{
    int j;
    Linklist p;
    p = *L;
    while(p && j < i)
    {
        p = p->next;
        ++j;
    }
    if(!p || j > i)
        return ERR;
    s = (LinkList)malloc(sizeof(Node));
    s->next = p->next;
    s->data = e
    p->next = s;
    return TRUE;
}
```

#### 单链线性表（尾差法）

```c
void CreateListTail(LinkList *L, int n)
{
    LinkList p, r;
    int i;
    srand(time(0));
    *L = (LinkList)malloc(sizeof(Node));
    r = *L;
    for(i = 0; i < n; ++i)
    {
        p = (Node *)malloc(sizeof(Node));
        p->data = rand() % 100 + 1;
        r->next = p;
        r = p;
    }
    r->next = NULL;//make sure it is tail
}
```

指针？

```c
Status ClearList(LinkList *L)
{
    LinkList p, q;
    p = (*L)->next;
    while(p->next != NULL)
    {
        q = p->next;
        free(p);
        p = q;
    }
    (*L)->next = NULL;
    return OK;
}
```

#### 静态链表

低效？？？

游标插入和删除

#### 循环链表

![image-20240428093744837](image-20240428093744837.png)

```c
p->head = p->rear;

# combine A and B
p = rearA->next;
rearA->next = rearB->next->next;
rearB->next = p;
free(p);
```

#### 双向链表

插入时前后顺序需要注意

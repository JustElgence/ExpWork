### Stack

##### Definition

限定仅在表尾进行插入和删除操作的线性表。

我们把允许插入和删除的一端称为栈顶（top），另一端称为栈底（bottom），不含任何数据元素的栈称为空栈。栈又称为后进先出（Last In First Out）的线性表，简称 LIFO 结构。

它的特殊之处就在于限制了这个线性表的插入和删除位置，它始终只在栈顶进行。这也就使得：栈底是固定的，最先进栈的只能在栈底。

栈的插入操作，叫作进栈，也称压栈、入栈。
栈的删除操作，叫作出栈，也有的叫作弹栈。

出栈顺序有限制。

```c
ADT Stack
Data 
	Same with Linear List
Operation
	InitStack(*S):
	DestroyStack(*S):
	ClearStack(*S):
	StackEmpty(*S):
	GetTop(*S, *e):
	Push(*S, e):
	Pop(*S ,*e):
	StackLength(S):
endADT
```

```c
typedef int SElemType;
typedef struct{
	SElemType data[MAX_SIZE];
	int top;
}SqStack;
```

空栈：top = -1, 满栈 top = MAX_SIZE - 1

```c
Status Push(*S, SElemType e)
{
	if(S->top == MAX_SIZE - 1)
		reutrn ERR;
	S->top ++;
	S->data[S->top] = e;
	return OK;
}
```

```c
Status Pop(*S, SElemType *e)
{
	if(S-> top == -1)
		return ERR;
	*e = S-data[S->top];
	S->top --;
	return OK;
}
```

#### 两栈共享空间

```c
typedef struct{
	SElemType data[MAX_SIZE];
	int top1;
	int top2;
}
# top1 + 1 = top2 时为栈满
```

```c
typedef struct StackNode{
	SElemType data;
}
```

#### 栈的链式存储结构

```c
typedef struct StackNode{
	SElemType data;
	struct StackNode *next;
}StackNode, *LinkStackPtr;
# name and ptr

typedef struct LinkStack{
    LinkStackPtr top;
    int count;
}LinkStack;
```

##### 进栈

```c
Status Push(LinkStack *S, SElemType e)
{
	LinkStackPtr s = (LinkStackPtr)malloc(sizeof(StackNode))
	s->data = e;
    s->next = S->top;
    S->top = s;
    S->count ++;
}
```

##### 出栈

```c
Status Pop(LinkStack *S, SElemType *e)
{
    LinkStackPtr p;
	if(!S->count)
        return ERR;
    p = s->top;
    *e = S->top->data;
    S->top = S->top->next;
    free(p);
    S->count --;
    return OK;
}
# note to free node
```

#### 后缀表达式

中缀表达式-->后缀表达式

规则：从左到右遍历中缀表达式的每个数字和符号，若是数字就输出，即成为后缀表达式的一部分；若是符号，则判断其与栈顶符号的优先级，是右括号或优先级低于栈顶符号（乘除优先加减）则栈顶元素依次出栈并输出，并将当前符号进栈，一直到最终输出后缀表达式为止。

"9+(3-1)×3+10/2"  ---->    9 3 1 - 3 * 10 2 / +

### Queue

队列（queue）是只允许在一端进行插入操作，而在另一端进行删除操作的线性表。队列是一种先进先出（First In First Out）的线性表，简称FIFO。允许插入的一端称为队尾，允许删除的一端称为队头。

```c
ADT Queue
Data
	same with linear list
Operation
	InitQueue(*Q):
	DestroyQueue(*Q):
	ClearQueue(*Q):
	QueueEmpty(Q):
	GetHead(Q, e):
	EnQueue(*Q, e):
	DeQueue(*Q, *e):
	QueueLength(Q):
endADT
```

循环队列的顺序存储结构

```c
typedef int QElemType;
typedef struct{
    QElemType data[MAX_SIZE];
    int front;
    int rear;
}SqQueue;
```

```c
int QueueLength(SeQueue Q)
{
    return(Q.rear - Q.front + MAX_SIZE);
}
```

```c
Stautus EnQueue(SeQueue *Q, QElemType e)
{
    if(QueueLength(Q) == MAX_SIZE)
        return ERR;
    Q->data[Q->rear] = e;
    Q->rear = (Q->rear + 1) % MAX_SIZE;
    return OK;
}
```

#### 队列的链式存储结构

为什么要分配内存，必须要创建一个新的节点存储信息，也就是所谓的链表

队列的链式存储结构，其实就是线性表的单链表，只不过它只能尾进头出而已，我们把它简称为链队列。为了操作上的方便，我们将队头指针指向链队列的**头结点**（不存储信息），队尾指针指向队尾。

空队列时，front和rear都指向**头结点**

```c
typedef int QElemType;
typedef struct QNode{
    QElemType data;
    struct QNode *next;
}QNode, *QNodePtr;

typedef struct{
    QueuePtr front, rear;
}LinkQueue;
```

```c
Status EnQueue(LinkQueue *Q, QElemType e)
{
	QNodePtr p = (QNodePtr)malloc(sizeof(QNode));
    if(!p)
        return ERR;
    p->data = e;
    p->next = NULL;
    Q->rear->next = p;
    Q->rear = p;
    return OK;
}

Status DeQueue(LinkQueue *Q, QElemType *e)
{
    if(Q->rear == Q->front)
        return  ERR;
    QNodePtr p;
    p = Q->front->next;
    *e = p->data;
    Q->front->next = p->next;
    if(p == Q->rear)
        Q->rear = Q->front;
    free(p);
    return OK;
}
```


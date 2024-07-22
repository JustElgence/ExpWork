#### Definition

树（Tree）是n（n20）个结点的有限集。n=0时称为空树。在任意一棵非空树中：（1）有且仅有一个特定的称为根（Root）的结点；（2）当n>1时，其余结点可分为m（m>0）个互不相交的有限集T1、T2、、Tm，其中每一个集合本身又是一棵树，并且称为根的子树（SubTree），如图 6-2-1 所示。

##### 节点分类

树的结点包含一个数据元素及若干指向其子树的分支。结点拥有的子树数称为结点的度（Degree）。度为0的结点称为叶结点（Leaf）或终端结点；度不为0的结点称为非终端结点或分支结点。除根结点之外，分支结点也称为内部结点。树的度是树内各结点的度的最大值。如图6-2-4所示，因为这棵树结点的度的最大值是结点D的度，为3，所以树的度也为3.

结点的层次（Level）从根开始定义起，根为第一层，根的孩子为第二层。若某结点在第1层，则其子树的根就在第1+1层。其双亲在同一层的结点互为堂兄弟。显然图6-2-6中的D、E、F是堂兄弟，而G、H.I、J也是。树中结点的最大层次称为树的深度（Depth）或高度，当前树的深度为4

森林（Forest）是m（m>0）棵互不相交的树的集合。对树中每个结点而言，其子树的集合即为森林。对于图6-2-1中的树而言，图6-2-2中的两棵子树其实就可以理解为森林。

#### 存储结构

##### 双亲表示法

```c
// define node first, and then create the whole tree.

#define MAX_TREE_SIZE 100
typdef int ElemTree;
typedef struct PTNode{
    ElemTree data;
    int parent;
} PTNode;

typedef struct{
    PTNode nodes[MAX_TREE_SIZE];
    int r,n;
}PTree;
```

##### 孩子表示法

```c
#define MAXI_TREE_SIZE 100
typedef struct CTNode{
    int child;
    struct CTNode *next;
} *ChildPtr;
typedef struct{
    ELemTree data;
    ChildPtr firstchild;
} *TreeBox;
typedef struct{
    TreeBox nodes[MAX_TREE_SIZE];
    int r, n;
} CTree;
```

#### 二叉树

##### 特征

* 每个结点最多有两棵子树，所以二叉树中不存在度大于2 的结点。注意不是只有两棵子树，而是最多有。没有子树或者有一棵子树都是可以的。
* 左子树和右子树是有顺序的，次序不能任意颠倒。就像人是双手、双脚，但显然左手、左脚和右手、右脚是不一样的，右手戴左手套、右脚穿左鞋都会极其别扭和难受。
* 即使树中某结点只有一棵子树，也要区分它是左子树还是右子树。图 6-5-3中，树1和树2是同一棵树，但它们却是不同的二叉树。就好像你一不小心，摔伤了手，伤的是左手还是右手，对你的生活影响度是完全不同的。

完全二叉树：按照序列排列时无空缺

##### 特点

在二叉树的第$i$层上至多有$2^{i-1}$个结点$（i>1）$。

深度为i的二叉树至多有$2^{i}-1$个结点$（i>1）$。

#### 二叉树的存储结构

##### 链式结构

```c
typedef struct BiTNode{
    TElemType data;
    BiTNode *lchild, rchild;
} BiTNode, *BiTree;
```

#### 遍历

* 前序遍历：根节点作为起始

  ```c
  void PreorderTravese(BiTree T)
  {
      if(T == NULL)
          return;
      show_Node(T->data);
      PreorderTravese(T->lchild);
      PreorderTravese(T->rchild);
  }
  ```

  

* 中序遍历：根节点作为中间

  ```c
  void MidorderTravese(BiTree T)
  {
      if(T == NULL)
          return;
      MidorderTravese(T->lchild);
      show_Node(T->data);
      MidorderTravese(T->rchild);
  }
  ```

* 后序遍历：根节点作为末尾

  ```c
  void EndorderTraveses(BiTree T)
  {
      if(T == NULL)
          return;
      EndorderTravese(T->lchild);
      EndorderTravese(T->rchild);
      show_Node(T->data);
  }
  ```

  

* 层序遍历：逐层遍历节点

```c
void orderTravese(BiTree T)
{
    
}
```



#### Threaded BiTree

```c
typedef enum {LINK, THREAD} PointTag;

typedef struct BiThrNode{
    TElemType data;
    struct BiThrNode* lchild, rchild;
    PointTag LTag;
    PointTag RTag;
} BiThrNode, *BiTrees;
```



#### 赫夫曼编码树

- **结点的路径长度**：从根结点到该结点的路径上分支的数目
- **树的路径长度**：树中每个结点的路径长度之和
- **结点的带权路径长度**：从根结点到该结点的路径长度![l_{k}](https://latex.csdn.net/eq?l_%7Bk%7D)与 结点上权![w_{k}](https://latex.csdn.net/eq?w_%7Bk%7D)的乘积
- **树的带权路径长度**：树中所有叶子结点的带权路径长度之和

在所有含 n 个叶子结点、并且叶子结点带相同权值的二叉树中，其带权路径长度WPL最小的那棵二叉树称为赫夫曼树，也叫最优二叉树。

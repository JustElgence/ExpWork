##### 深度优先遍历

原则：在没有碰到重复顶点的情况下，始终是向右手边走

这里讲到的是连通图，对于非连通图，只需要对它的连通分量分别进行深度优先遍历，即在先前一个顶点进行一次深度优先遍历后，若图中尚有顶点未被访问，则另选图中一个未曾被访问的顶点作起始点，重复上述过程，直至图中所有顶点都被访问到为止。

```c
typedef int Boolean;
Boolean visted[MAX];

void DFS(MGraph G, int i) {
    int j;
    visited[i] = true;
    opearte(G.vexs[i]);
    for(j = 0; j < G.numVertexs; ++j) {
        if(G.arc[i][j] == 1 && !visted[j])
            DFS(G, j);
    }
}

void DFSTravse(MGraph G) {
    int i;
    for (i= 0; i < G.numVertexs; ++i) 
        visited[i] = false;
    for(i = 0; i < G.numVertexs; ++i)
        if(Ivisited[i])
            DFS(G, i);
}
```

##### 广度优先遍历

按照层序压入，压出一个节点压入该节点中未访问的子节点

```c
void BFSTraverse(MGraph G) {
    int i, j;
    Queue Q;
    for(i = 0; i < G.numVertexes; ++i)
        visted[i] = false;
   for(i = 0; i < G.numVertexed; ++i) {
       if(!visited[i]) {
           visted[i] = true;
           opeate(G.vexs[i]);
           Enqueue(&Q, i);
       while(!isEmpty(Q)) {
           Dequeue(q, &i);
           for(j = 0; j < G.numVertexs; ++j) {
               if(G.arc[i][j] == 1 && !visted[j]) {
                   visted[j] = true;
                   opearate(G.vexs[j]);
                   Enqueue(q,&j);
               }
           }
       }
       }
   }
}
```

```
git status
git add 
git commit
git log --pretty=="zhushi"
git reset --hard commitId
touch .gitignore(vi this, tianjian houzhui .etc"*.a")
branch:
git branch name
git checkout name
git chekcout -b name
git merge name(合并到master目录)
git branch -d(D强制) name
git remote 
git push[-f][--set--upstream][远端名称[本地：远端]]
git branch -vv
git clone <remote res> <bendi>
git fetch 
git-f + git-merge == git-pull
```


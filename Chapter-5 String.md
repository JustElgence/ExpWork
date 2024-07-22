### Definition

串（string）是由零个或多个字符组成的有限序列，又名叫字符串。

因此，对于串的基本操作与线性表是有很大差别的。线性表更关注的是单个元素的操作，比如查找一个元素，插入或删除一个元素，但串中更多的是**查找子串位置**、一得到**指定位置子串**、**替换子串**等操作。

```c
ADT String
Data
    Singal char, forward and ahead
Operation
    StrAssign(T, *chars)
    StrCopy(T, S)
    ClearString(S)
    StringEmpty(S)
    StrLength(S)
    StrCompare(S,T)
    Concat(T,S1,S2)
    SubString(Sub, S, pos, len)
    Index(S, T, pos)
    Replace(S, T, V)
    StrInsert(s, pos, T)
    StrDelete(S, pos, len)
```

#### KMP模式匹配算法


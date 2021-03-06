## 图问题

### 无权图

| 问题 | 备注 | 代码 |
|---|---|---|
| NonweightedGraph | 无权图接口 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/NonweightedGraph.java) |
| DenseNonweightedGraph | 用邻接矩阵存储稠密图 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/DenseNonweightedGraph.java) |
| SparseNonweightedGraph | 用邻接表存储稀疏图 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/SparseNonweightedGraph.java) |
| ReadGraphHelper | 读取文件数据辅助类 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/ReadGraphHelper.java) |
| NonweightedGraphTest | 借助 ReadGraphHelper 测试 DenseNonweightedGraph 和 SparseNonweightedGraph | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/NonweightedGraphTest.java) |
| Component | 采用 DFS 求联通分量 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/Component.java) |
| Path | 采用 BFS 求最短路径 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/Path.java) |

### 带权图

| 问题 | 备注 | 代码 |
|---|---|---|
| WeightedGraph | 带权图接口 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/WeightedGraph.java) |
| DenseWeightedGraph | 用邻接矩阵存储稠密图 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/DenseWeightedGraph.java) |
| SparseWeightedGraph | 用邻接表存储稀疏图 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/SparseWeightedGraph.java) ||
| WeightedGraphTest | 借助 ReadGraphHelper 测试 DenseWeightedGraph 和 SparseWeightedGraph | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/WeightedGraphTest.java) |

### 最小生成树问题

#### 背景知识：
> 切分： 把图中的点划分为两个部分，成为一个切分
>
> 横切边： 一条边的两个端点属于切分中的不同部分
> 
> 切分定理： 给定任意切分，横切边的最小权值边必定属于最小生树

| 最小生成树算法 | 时间复杂度 | 
|---|---|
| Lazy Prim | O(ElogE)  |
| Prim | O(ElogV)  |
| Kruskal | O(ElogE)  |

##### 1. Lazy Prim
```
1. 以任意顶点作为开始
2. 访问该顶点，并将该顶点的横切边加入最小堆（或其他辅助方法）
3. 将堆中权值最小的横切边加入生成树，并回到2. 访问该边未访问的顶点，直到所有顶点均加入最小生成树
```

##### 2. Prim - 基于 Lazy Prim 的优化
```
采用 edgeTo 数组结合最小索引堆，
维护一个记录当前生成树到各顶点的最低权值横切边的数组，而不再是将所有未访问横切边加入堆中排序
```

##### 3. Kruskal
```
将所有边以权值排序，从小到大遍历，
如果将遍历的该边加入生成树中不会造成环，那么就加入生成树，否则跳过。
利用并查集作为辅助判断是否生成环
```

#### 实验对比：

采用 testG4.txt 数据对以下方法进行测试，其中包含 10000 个顶点，61731 条边。
```
Test LazyPrimMST:
Consume 186ms.
the mst weight result = 65.24072000000014

Test PrimMST:
Consume 47ms.
the mst weight result = 65.24072000000014

Test KruskalMST:
Consume 123ms.
the mst weight result = 65.24071999999985
```

#### 实现

| 问题 | 备注 | 代码 |
|---|---|---|
| Lazy Prim | 普利姆最小生成树算法 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/LazyPrimMST.java) |
| Prim | 普里姆优化-采用最小索引堆，仅维护最小权值的横切边，而不是将访问过的顶点的所有边加入堆 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/PrimMST.java) |
| Kruskal | 克鲁斯卡尔最小生成树算法 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/PrimMST.java) |
| MST | LazyPrim、Prim、Kruskal 时间效率上的比较 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/MST.java) |

### 最短路径问题

| 最短路径算法 | 时间复杂度 | 备注 |
|---|---|---|
| Dijkstra | O(ElogV)  | 前提不能具有负权边 |
| Bellman-Ford | O(EV)  | 可以有负权边，但不能具有负权环 |

#### 实现

| 问题 | 备注 | 代码 |
|---|---|---|
| Dijkstra | 迪杰斯特拉最短路径算法 | [Java](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/Dijkstra.java) |
| BellmanFord | 贝尔曼福特最短路径算法 | [Java](https://github.com/patricklin2018/DataStructures/blob/master/graph/src/BellmanFord.java) |

### 测试数据

| 数据 | 备注 | 链接 |
|---|---|---|
| testG1 | 无权图测试数据 | [testG1.txt](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/testG1.txt) |
| testG2 | 无权图测试数据 | [testG2.txt](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/testG2.txt) ||
| testG3 | 带权图测试数据 | [testG3.txt](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/testG3.txt) |
| testG3 | 带权图， 10000 个顶点， 61731条边 | [testG4.txt](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/testG4.txt) |
| testG5 | 带权图有向图测试数据 | [testG5.txt](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/testG5.txt) |
| testG6 | 不具有负权环的负权图 | [testG6.txt](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/testG6.txt) |
| testG7 | 带负权环的负权图 | [testG7.txt](https://github.com/patricklin2018/DataStructures-Algorithmns/blob/master/graph/src/testG7.txt) |
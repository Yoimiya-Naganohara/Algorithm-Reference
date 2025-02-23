[English](Depth%20First%20Search.md) | [中文](Depth%20First%20Search_cn.md)

# 深度优先搜索

深度优先搜索 (DFS) 是一种用于遍历或搜索树或图数据结构的算法。 该算法从根节点开始（在图的情况下，选择某个任意节点作为根节点），并尽可能沿着每个分支进行探索，然后再回溯。

## 代码示例 (Python)

```python
def dfs(graph, start):
    visited, stack = set(), [start]
    while stack:
        vertex = stack.pop()
        if (vertex not in visited):
            visited.add(vertex)
            stack.extend(set(graph[vertex]) - visited)
    return visited

graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}

print(dfs(graph, 'A'))
```

## 代码示例 (Java)

```java
import java.util.*;

class Main {
    static class Graph {
        private Map<String, List<String>> adjList = new HashMap<>();

        public void addVertex(String vertex) {
            adjList.put(vertex, new LinkedList<>());
        }

        public void addEdge(String source, String destination) {
            adjList.get(source).add(destination);
        }

        public Set<String> dfs(String start) {
            Set<String> visited = new LinkedHashSet<>();
            Stack<String> stack = new Stack<>();
            stack.push(start);

            while (!stack.isEmpty()) {
                String vertex = stack.pop();
                if (!visited.contains(vertex)) {
                    visited.add(vertex);
                    for (String neighbor : adjList.get(vertex)) {
                        stack.push(neighbor);
                    }
                }
            }
            return visited;
        }
    }

    public static void main(String[] args) {
        Graph graph = new Graph();
        graph.addVertex("A");
        graph.addVertex("B");
        graph.addVertex("C");
        graph.addVertex("D");
        graph.addVertex("E");
        graph.addVertex("F");

        graph.addEdge("A", "B");
        graph.addEdge("A", "C");
        graph.addEdge("B", "D");
        graph.addEdge("B", "E");
        graph.addEdge("C", "F");

        System.out.println("DFS 遍历: " + graph.dfs("A"));
    }
}
```

## 代码示例 (C)

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define MAX_VERTICES 6

struct Graph {
    int adjMatrix[MAX_VERTICES][MAX_VERTICES];
    int numVertices;
};

void initGraph(struct Graph* graph) {
    graph->numVertices = 0;
    for (int i = 0; i < MAX_VERTICES; i++) {
        for (int j = 0; j < MAX_VERTICES; j++) {
            graph->adjMatrix[i][j] = 0;
        }
    }
}

void addEdge(struct Graph* graph, int src, int dest) {
    graph->adjMatrix[src][dest] = 1;
}

void DFS(struct Graph* graph, int vertex, bool visited[]) {
    visited[vertex] = true;
    printf("已访问 %d \n", vertex);

    for (int i = 0; i < MAX_VERTICES; i++) {
        if (graph->adjMatrix[vertex][i] == 1 && !visited[i]) {
            DFS(graph, i, visited);
        }
    }
}

int main() {
    struct Graph graph;
    initGraph(&graph);
    graph.numVertices = 6;

    addEdge(&graph, 0, 1);
    addEdge(&graph, 0, 2);
    addEdge(&graph, 1, 3);
    addEdge(&graph, 1, 4);
    addEdge(&graph, 2, 5);

    bool visited[MAX_VERTICES] = {false};
    printf("从顶点 0 开始的 DFS 遍历: \n");
    DFS(&graph, 0, visited);

    return 0;
}
```

## 代码示例 (C++)

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

void DFS(int vertex, vector<vector<int>>& adjMatrix, vector<bool>& visited) {
    visited[vertex] = true;
    cout << "已访问 " << vertex << endl;

    for (int i = 0; i < adjMatrix.size(); i++) {
        if (adjMatrix[vertex][i] == 1 && !visited[i]) {
            DFS(i, adjMatrix, visited);
        }
    }
}

int main() {
    int numVertices = 6;
    vector<vector<int>> adjMatrix(numVertices, vector<int>(numVertices, 0));

    adjMatrix[0][1] = 1;
    adjMatrix[0][2] = 1;
    adjMatrix[1][3] = 1;
    adjMatrix[1][4] = 1;
    adjMatrix[2][5] = 1;

    vector<bool> visited(numVertices, false);
    cout << "从顶点 0 开始的 DFS 遍历: " << endl;
    DFS(0, adjMatrix, visited);

    return 0;
}
```

## 时间复杂度

DFS 的时间复杂度为 O(V + E)，其中 V 是顶点数，E 是边数。

## 空间复杂度

DFS 的空间复杂度在最坏情况下为 O(V)，其中 V 是顶点数。 这是由于递归调用期间调用堆栈所需的空间。

## 使用场景

DFS 用于各种应用，例如：

*   查找图中的连接组件
*   拓扑排序
*   解决只有一个解决方案的难题，例如迷宫
*   寻路算法

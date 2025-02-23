[English](Dijkstra.md) | [中文](Dijkstra_cn.md)

# Dijkstra 算法

Dijkstra 算法是一种用于查找图中节点之间最短路径的算法，该图可以表示例如道路网络。 它由计算机科学家 Edsger W. Dijkstra 于 1956 年构思，三年后发表。

## 代码示例 (Python)

```python
import heapq

def dijkstra(graph, start):
    # 使用无穷大初始化距离，并将到起始节点的距离设置为 0
    distances = {node: float('infinity') for node in graph}
    distances[start] = 0

    # 优先队列，用于存储 (距离, 节点) 元组
    priority_queue = [(0, start)]

    while priority_queue:
        current_distance, current_node = heapq.heappop(priority_queue)

        # 如果当前距离大于记录的距离，则跳过处理
        if current_distance > distances[current_node]:
            continue

        # 更新到相邻节点的距离
        for neighbor, weight in graph[current_node].items():
            distance = current_distance + weight

            # 仅当此新路径更短时才考虑
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(priority_queue, (distance, neighbor))

    return distances

# 示例用法
graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'C': 2, 'D': 5},
    'C': {'A': 4, 'B': 2, 'D': 1},
    'D': {'B': 5, 'C': 1}
}
start_node = 'A'
print(dijkstra(graph, start_node))
```

## 代码示例 (Java)

```java
import java.util.*;

class Main {
    static class Graph {
        private Map<String, Map<String, Integer>> adjList = new HashMap<>();

        public void addNode(String node) {
            adjList.put(node, new HashMap<>());
        }

        public void addEdge(String source, String destination, int weight) {
            adjList.get(source).put(destination, weight);
            adjList.get(destination).put(source, weight); // 对于无向图
        }

        public Map<String, Integer> dijkstra(String start) {
            Map<String, Integer> distances = new HashMap<>();
            for (String node : adjList.keySet()) {
                distances.put(node, Integer.MAX_VALUE);
            }
            distances.put(start, 0);

            PriorityQueue<AbstractMap.SimpleEntry<Integer, String>> pq = new PriorityQueue<>(Comparator.comparing(AbstractMap.SimpleEntry::getKey));
            pq.add(new AbstractMap.SimpleEntry<>(0, start));

            while (!pq.isEmpty()) {
                AbstractMap.SimpleEntry<Integer, String> current = pq.poll();
                int currentDistance = current.getKey();
                String currentNode = current.getValue();

                if (currentDistance > distances.get(currentNode)) {
                    continue;
                }

                for (Map.Entry<String, Integer> neighbor : adjList.get(currentNode).entrySet()) {
                    String neighborNode = neighbor.getKey();
                    int weight = neighbor.getValue();
                    int distance = currentDistance + weight;

                    if (distance < distances.get(neighborNode)) {
                        distances.put(neighborNode, distance);
                        pq.add(new AbstractMap.SimpleEntry<>(distance, neighborNode));
                    }
                }
            }

            return distances;
        }
    }

    public static void main(String[] args) {
        Graph graph = new Graph();
        graph.addNode("A");
        graph.addNode("B");
        graph.addNode("C");
        graph.addNode("D");

        graph.addEdge("A", "B", 1);
        graph.addEdge("A", "C", 4);
        graph.addEdge("B", "C", 2);
        graph.addEdge("B", "D", 5);
        graph.addEdge("C", "D", 1);

        String startNode = "A";
        System.out.println(graph.dijkstra(startNode));
    }
}
```

## 代码示例 (C)

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define V 4 // 图中的顶点数

int minDistance(int dist[], int sptSet[]) {
    int min = INT_MAX, min_index;
    for (int v = 0; v < V; v++)
        if (sptSet[v] == 0 && dist[v] <= min)
            min = dist[v], min_index = v;
    return min_index;
}

void dijkstra(int graph[V][V], int src) {
    int dist[V];
    int sptSet[V];

    for (int i = 0; i < V; i++)
        dist[i] = INT_MAX, sptSet[i] = 0;

    dist[src] = 0;

    for (int count = 0; count < V - 1; count++) {
        int u = minDistance(dist, sptSet);
        sptSet[u] = 1;
        for (int v = 0; v < V; v++)
            if (!sptSet[v] && graph[u][v] && dist[u] != INT_MAX && dist[u] + graph[u][v] < dist[v])
                dist[v] = dist[u] + graph[u][v];
    }

    printf("顶点   距源点的距离\n");
    for (int i = 0; i < V; i++)
        printf("%d \t\t %d\n", i, dist[i]);
}

int main() {
    int graph[V][V] = {
        {0, 1, 4, 0},
        {1, 0, 2, 5},
        {4, 2, 0, 1},
        {0, 5, 1, 0}
    };

    dijkstra(graph, 0);

    return 0;
}
```

## 代码示例 (C++)

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

int main() {
    int V = 4; // 顶点数
    vector<vector<int>> graph = {
        {0, 1, 4, 0},
        {1, 0, 2, 5},
        {4, 2, 0, 1},
        {0, 5, 1, 0}
    };

    int src = 0; // 源顶点
    vector<int> dist(V, numeric_limits<int>::max());
    dist[src] = 0;

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, src});

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        if (d > dist[u]) continue;

        for (int v = 0; v < V; v++) {
            if (graph[u][v] != 0) {
                if (dist[v] > dist[u] + graph[u][v]) {
                    dist[v] = dist[u] + graph[u][v];
                    pq.push({dist[v], v});
                }
            }
        }
    }

    cout << "顶点   距源点的距离" << endl;
    for (int i = 0; i < V; i++)
        cout << i << " \t\t " << dist[i] << endl;

    return 0;
}
```

## 时间复杂度

Dijkstra 算法的时间复杂度为 O((V + E) log V)，其中 V 是顶点数，E 是图中的边数。 这种复杂性是由于使用优先队列来选择具有最小距离的下一个节点而产生的。

## 空间复杂度

Dijkstra 算法的空间复杂度为 O(V)，其中 V 是图中的顶点数。 这是由于存储每个顶点的距离。

## 使用场景

Dijkstra 算法广泛应用于各种应用，包括：

*   GPS 导航系统，用于查找位置之间的最短路径
*   网络路由协议，用于确定数据包的最有效路径
*   交通管理系统，用于优化交通流量并减少拥堵
*   机器人技术，用于路径规划和避障

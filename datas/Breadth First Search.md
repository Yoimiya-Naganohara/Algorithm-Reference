[English](Breadth%20First%20Search.md) | [中文](Breadth%20First%20Search_cn.md)
# Breadth First Search

Breadth-first search (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root and explores all of the neighbor nodes at the present depth prior to moving on to the nodes at the next depth level.

## Code Example (Python)

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    while queue:
        vertex = queue.popleft()
        if vertex not in visited:
            visited.add(vertex)
            queue.extend(set(graph[vertex]) - visited)
    return visited

# Example usage:
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}
print(bfs(graph, 'A'))  # Output: {'A', 'B', 'C', 'D', 'E', 'F'}
```

## Code Example (Java)

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
            adjList.get(destination).add(source);
        }

        public Set<String> bfs(String start) {
            Set<String> visited = new LinkedHashSet<>();
            Queue<String> queue = new LinkedList<>();
            queue.add(start);

            while (!queue.isEmpty()) {
                String vertex = queue.poll();
                if (!visited.contains(vertex)) {
                    visited.add(vertex);
                    queue.addAll(adjList.get(vertex));
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
        graph.addEdge("E", "F");

        System.out.println("BFS traversal: " + graph.bfs("A"));
    }
}
```

## Code Example (C)

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
    graph->adjMatrix[dest][src] = 1;
}

void BFS(struct Graph* graph, int startVertex, bool visited[]) {
    int queue[MAX_VERTICES];
    int front = 0, rear = 0;

    visited[startVertex] = true;
    queue[rear++] = startVertex;

    while (front < rear) {
        int currentVertex = queue[front++];
        printf("Visited %d \n", currentVertex);

        for (int i = 0; i < MAX_VERTICES; i++) {
            if (graph->adjMatrix[currentVertex][i] == 1 && !visited[i]) {
                visited[i] = true;
                queue[rear++] = i;
            }
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
    addEdge(&graph, 4, 5);

    bool visited[MAX_VERTICES] = {false};
    printf("BFS traversal starting from vertex 0: \n");
    BFS(&graph, 0, visited);

    return 0;
}
```

## Code Example (C++)

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

void BFS(int startVertex, vector<vector<int>>& adjMatrix, vector<bool>& visited) {
    queue<int> q;
    visited[startVertex] = true;
    q.push(startVertex);

    while (!q.empty()) {
        int currentVertex = q.front();
        cout << "Visited " << currentVertex << endl;
        q.pop();

        for (int i = 0; i < adjMatrix.size(); i++) {
            if (adjMatrix[currentVertex][i] == 1 && !visited[i]) {
                visited[i] = true;
                q.push(i);
            }
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
    adjMatrix[4][5] = 1;

    vector<bool> visited(numVertices, false);
    cout << "BFS traversal starting from vertex 0: \n";
    BFS(0, adjMatrix, visited);

    return 0;
}
```

## Time Complexity

The time complexity of BFS is O(V + E), where V is the number of vertices and E is the number of edges in the graph.

## Space Complexity

The space complexity of BFS is O(V), where V is the number of vertices. In the worst case, the queue can hold all vertices in the graph.

## Use Cases

- Finding the shortest path in an unweighted graph
- Crawling the web
- Finding all nodes within one connected component
- Broadcasting in networks

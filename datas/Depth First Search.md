[English](Depth%20First%20Search.md) | [中文](Depth%20First%20Search_cn.md)
# Depth First Search

Depth-first search (DFS) is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking.

## Code Example (Python)

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

        System.out.println("DFS traversal: " + graph.dfs("A"));
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
}

void DFS(struct Graph* graph, int vertex, bool visited[]) {
    visited[vertex] = true;
    printf("Visited %d \n", vertex);

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
    printf("DFS traversal starting from vertex 0: \n");
    DFS(&graph, 0, visited);

    return 0;
}
```

## Code Example (C++)

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

void DFS(int vertex, vector<vector<int>>& adjMatrix, vector<bool>& visited) {
    visited[vertex] = true;
    cout << "Visited " << vertex << endl;

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
    cout << "DFS traversal starting from vertex 0: " << endl;
    DFS(0, adjMatrix, visited);

    return 0;
}
```

## Time Complexity

The time complexity of DFS is O(V + E), where V is the number of vertices and E is the number of edges.

## Space Complexity

The space complexity of DFS is O(V) in the worst case, where V is the number of vertices. This is due to the space required by the call stack during the recursive calls.

## Use Cases

DFS is used in various applications such as:
- Finding connected components in a graph
- Topological sorting
- Solving puzzles with only one solution, such as mazes
- Pathfinding algorithms

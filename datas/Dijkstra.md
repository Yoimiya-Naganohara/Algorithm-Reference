[English](Dijkstra.md) | [中文](Dijkstra_cn.md)
# Dijkstra's Algorithm

Dijkstra's algorithm is an algorithm for finding the shortest paths between nodes in a graph, which may represent, for example, road networks. It was conceived by computer scientist Edsger W. Dijkstra in 1956 and published three years later.

## Code Example (Python)

```python
import heapq

def dijkstra(graph, start):
    # Initialize distances with infinity and set the distance to the start node to 0
    distances = {node: float('infinity') for node in graph}
    distances[start] = 0

    # Priority queue to store (distance, node) tuples
    priority_queue = [(0, start)]

    while priority_queue:
        current_distance, current_node = heapq.heappop(priority_queue)

        # If the current distance is greater than the recorded distance, skip processing
        if current_distance > distances[current_node]:
            continue

        # Update the distances to the neighboring nodes
        for neighbor, weight in graph[current_node].items():
            distance = current_distance + weight

            # Only consider this new path if it's shorter
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(priority_queue, (distance, neighbor))

    return distances

# Example usage
graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'C': 2, 'D': 5},
    'C': {'A': 4, 'B': 2, 'D': 1},
    'D': {'B': 5, 'C': 1}
}
start_node = 'A'
print(dijkstra(graph, start_node))
```

## Code Example (Java)

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
            adjList.get(destination).put(source, weight); // For undirected graph
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

## Code Example (C)

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define V 4 // Number of vertices in the graph

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

    printf("Vertex   Distance from Source\n");
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

## Code Example (C++)

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

int main() {
    int V = 4; // Number of vertices
    vector<vector<int>> graph = {
        {0, 1, 4, 0},
        {1, 0, 2, 5},
        {4, 2, 0, 1},
        {0, 5, 1, 0}
    };

    int src = 0; // Source vertex
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

    cout << "Vertex   Distance from Source" << endl;
    for (int i = 0; i < V; i++)
        cout << i << " \t\t " << dist[i] << endl;

    return 0;
}
```

## Time Complexity

The time complexity of Dijkstra's algorithm is O((V + E) log V), where V is the number of vertices and E is the number of edges in the graph. This complexity arises from the use of a priority queue to select the next node with the smallest distance.

## Space Complexity

The space complexity of Dijkstra's algorithm is O(V), where V is the number of vertices in the graph. This is due to the storage of distances for each vertex.

## Use Cases

Dijkstra's algorithm is widely used in various applications, including:

- GPS navigation systems to find the shortest path between locations
- Network routing protocols to determine the most efficient path for data packets
- Traffic management systems to optimize traffic flow and reduce congestion
- Robotics for pathfinding and obstacle avoidance
````

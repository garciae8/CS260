Design for Final Project

The purpose is to design a program that simulates a GPS map for a delivery simulator game. The program will create a graph structure with vertices as delivery locations and edges as paths. It will include functionalities to add locations and paths, find the shortest route between two locations, and determine the map's minimum spanning tree.

Graph Class

Attributes:

std::vector<Vertex> vertices: Stores all the vertices (locations) in the graph.
std::vector<Edge> edges: Stores all the edges (paths) between vertices.
Methods:

void addVertex(const Vertex& vertex): Adds a new vertex (location) to the graph.
void addEdge(const Edge& edge): Adds a new edge (path) between two vertices.
std::vector<Vertex> shortestPath(const Vertex& start, const Vertex& end): Finds the shortest path between two vertices using Dijkstra's algorithm.
std::vector<Edge> minimumSpanningTree(): Finds the minimum spanning tree using Kruskal's or Prim's algorithm.
Vertex Class

Attributes:

int id: Unique identifier for the vertex.
std::string name: Name or label of the vertex.
double x, y: Coordinates for the vertex location (optional).
Methods:

Vertex(int id, const std::string& name, double x = 0, double y = 0): Constructor to initialize the vertex.
Edge Class

Attributes:

Vertex source: The starting vertex of the edge.
Vertex destination: The ending vertex of the edge.
double weight: The weight of the edge, representing the distance or cost.
Methods:

Edge(const Vertex& source, const Vertex& destination, double weight): Constructor to initialize the edge.
Example Test Cases
Test Case 1: Add Vertex

Create a graph.
Add Vertex(1, "A").
Verify the vertex is in the vertices list.
Test Case 2: Add Edge

Create a graph with two vertices.
Add Edge(Vertex(1, "A"), Vertex(2, "B"), 10).
Verify the edge is in the edges list.
Test Case 3: Shortest Path

Create a graph with multiple vertices and edges.
Add edges with different weights.
Find the shortest path between two vertices.
Verify the correctness of the returned path.
Test Case 4: Minimum Spanning Tree

Create a graph with multiple vertices and edges.
Add edges with different weights.
Find the MST.
Verify the correctness of the returned edges in the MST.


Explanation 

// Adds a new vertex (location) to the graph
void addVertex(const Vertex& vertex) {
    vertices[vertex.id] = vertex;
}


Sure, I'll explain how the code you provided meets the requirements specified, using snippets from the code.

1. Add a New Vertex
Requirement: Implement a function to add a new vertex to the graph.

Code:

cpp
Copy code
// Adds a new vertex (location) to the graph
void addVertex(const Vertex& vertex) {
    vertices[vertex.id] = vertex;
}

This function adds a new vertex to the vertices map, where the key is the vertex ID and the value is the vertex itself.


// Adds a new edge (path) between two vertices
void addEdge(const Vertex& source, const Vertex& destination, double weight) {
    Edge edge(source, destination, weight);
    edges.push_back(edge);
}

This function creates a new edge with the given source, destination, and weight, and then adds it to the edges vector.


// Finds the shortest path between two vertices using Dijkstra's algorithm
std::vector<Vertex> shortestPath(const Vertex& start, const Vertex& end) {
    std::unordered_map<int, double> distances;
    std::unordered_map<int, int> previous;
    for (const auto& vertex_pair : vertices) {
        distances[vertex_pair.first] = std::numeric_limits<double>::infinity();
    }
    distances[start.id] = 0;

    auto cmp = [&distances](int left, int right) {
        return distances[left] > distances[right];
    };
    std::priority_queue<int, std::vector<int>, decltype(cmp)> queue(cmp);
    queue.push(start.id);

    while (!queue.empty()) {
        int current = queue.top();
        queue.pop();

        if (current == end.id) {
            break;
        }

        for (const auto& edge : edges) {
            if (edge.source.id == current) {
                double newDist = distances[current] + edge.weight;
                if (newDist < distances[edge.destination.id]) {
                    distances[edge.destination.id] = newDist;
                    previous[edge.destination.id] = current;
                    queue.push(edge.destination.id);
                }
            }
        }
    }

    std::vector<Vertex> path;
    for (int at = end.id; at != start.id; at = previous[at]) {
        path.push_back(vertices[at]);
    }
    path.push_back(start);
    std::reverse(path.begin(), path.end());
    return path;
}

This function uses Dijkstra's algorithm to find the shortest path between two vertices. It uses a priority queue to explore the vertices and update the shortest known distances to each vertex. The distances map keeps track of the shortest distances, and the previous map keeps track of the path.


// Finds the minimum spanning tree using Kruskal's algorithm
std::vector<Edge> minimumSpanningTree() {
    std::vector<Edge> result;
    std::sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
        return a.weight < b.weight;
    });

    std::unordered_map<int, int> parent;
    for (const auto& vertex_pair : vertices) {
        parent[vertex_pair.first] = vertex_pair.first;
    }

    auto find = [&parent](int vertex) {
        if (parent[vertex] != vertex) {
            parent[vertex] = find(parent[vertex]);
        }
        return parent[vertex];
    };

    auto unionSets = [&parent](int a, int b) {
        int rootA = find(a);
        int rootB = find(b);
        if (rootA != rootB) {
            parent[rootB] = rootA;
        }
    };

    for (const auto& edge : edges) {
        int rootSource = find(edge.source.id);
        int rootDestination = find(edge.destination.id);
        if (rootSource != rootDestination) {
            result.push_back(edge);
            unionSets(rootSource, rootDestination);
        }
    }

    return result;
}

This function uses Kruskal's algorithm to find the minimum spanning tree. It first sorts all the edges by weight, then uses a union-find structure to build the MST by adding the smallest edges that don't form a cycle.

int main() {
    Graph g;

    Vertex v1(1, "A");
    Vertex v2(2, "B");
    Vertex v3(3, "C");
    Vertex v4(4, "D");

    g.addVertex(v1);
    g.addVertex(v2);
    g.addVertex(v3);
    g.addVertex(v4);

    g.addEdge(v1, v2, 1.0);
    g.addEdge(v2, v3, 2.0);
    g.addEdge(v3, v4, 1.0);
    g.addEdge(v1, v4, 4.0);
    g.addEdge(v1, v3, 3.0);

    std::vector<Vertex> shortest_path = g.shortestPath(v1, v4);
    std::cout << "Shortest path from " << v1.name << " to " << v4.name << ": ";
    for (const auto& vertex : shortest_path) {
        std::cout << vertex.name << " ";
    }
    std::cout << std::endl;

    std::vector<Edge> mst = g.minimumSpanningTree();
    std::cout << "Minimum spanning tree edges: ";
    for (const auto& edge : mst) {
        std::cout << "(" << edge.source.name << ", " << edge.destination.name << ") ";
    }
    std::cout << std::endl;

    return 0;
}

This main function demonstrates how to use the Graph class, adding vertices and edges, and then finding the shortest path and minimum spanning tree.
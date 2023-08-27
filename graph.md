---
description: why is everything is connected ?
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Graph

## Directed vs UnDirected Graph

#### Directed Graph

* Degree = no. edges from a graph
* Sum of degrees = 2 x | no of edges |
* max number of edge = \[ v \* (v-1) ]/2

#### Undirected Graph

* Degree = in-degree + out-degree&#x20;
* Sum of in-degree = | no of edges |
* Sum of out-degree = | no of edges |
* max number of edge = v \* (v-1)

## Concepts on graph

* Walk (sometimes path) : from going one edge to another via connected edges
  * v1 -> v2 -> v4 -> v2&#x20;
  * if no edge exists between 2 vertices, you cannot walk directly
* Path (simple path) : a walk without repeated vertices allowed
* Degree : all edges to vertices
  * in-degree : directed graph incoming edges
  * out-degree : directed graph outgoing edges
* Cyclic : if the walk starts and ends on the same vertices
  * they can directed and undirected
* Acyclic : &#x20;
  * Undirected acyclic graph (UDAG)
  * Directed acyclic graph (DAG)
* Weighted graph : edges with some weight assigned to it
  * unweighted graph : simple edges

## Adjacency Matrix vs List

#### Adjacency Matrix

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>adjacency matrix : undirected graph</p></figcaption></figure>

* If the diagonal of matrix is 0 and **upper and lower triangle are symmetric**, **then it is a undirected graph**
* size of matrix = |v|x|v|
* **If graph is not symmetric , then it is a directed graph**

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption><p>adjacency matrix : directed graph</p></figcaption></figure>

* space required : |v|x|v|
* check if u & v are adj : O(1)
* find all vertices : O(v) : simple matrix row traversal
* adding/removing edges : O(1)

#### Adjacency Matrix List

<figure><img src=".gitbook/assets/image (9).png" alt="" width="563"><figcaption><p>adjacency list undirected graph</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption><p>adjacency list directed graph</p></figcaption></figure>

* space required : O(V+E)
  * undirected : V+2E
  * directed : V+E
* check if there is a edge from u to v : O(v)
* find all adjacency of u : O(degree(u))
* Find degree of u : O(1)
* Add an edge : O(1)
* remove and edge : O(v)

## Applications of DFS vs BFS

#### Applications of Breadth First Search

* Shortest Path in unweighted graph
* Crawler in Search Engine
* Peer to Peer network
* Social Networking Search
* In garbage collection (Cheney's Algorithm)
* Cycle Detection
* Ford Fulkerson Algorithm
* Broadcasting

#### Applications of Depth First Search

* Cycle Detection
* Topological Sorting
* Solving Maze and Puzzle Problems
* Path Finding

## Adjacency List implementation in Java

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    static void printGraph(ArrayList<ArrayList<Integer>> adj) {
        for (int i = 0; i < adj.size(); i++) {
            for (int j = 0; j < adj.get(i).size(); j++) {
                System.out.print(adj.get(i).get(j) + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int V = 4;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        // Adding edges one by one
        addEdge(adj, 0, 1); addEdge(adj, 0, 2);
        addEdge(adj, 1, 2); addEdge(adj, 1, 3);

        printGraph(adj);
    }
}
```

## Breadth First Search Graph Traversal

#### How it works

* create a queue to maintain elements for breadth first search
* to avoid repeating the visited nodes in cyclic graph, create a **boolean** array of size |v| to mark array\[**i**] as true/false indicating visited status
* **CODE FOR BFS disconnected graph is same**&#x20;

#### Disconnected Graph:  How it works&#x20;

* same as BFS, the algorithm is called for every node assuming it is the source vertice of the disconnected graph.
* we keep track of visited vertices in an boolean array just like BFS but this visited array is passed from source caller to BFS algorithm (in Java : array is pass by reference)
* this visited array will avoid calling BFS for nodes of island as they would have been visited&#x20;

#### To count the number of island in graph

* keep track of island source with counter
  * every islands nodes will be ignored as they will be marked as visited by BFS

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    static void BFS(ArrayList<ArrayList<Integer>> adj, int s, boolean[] visited) {
        Queue<Integer> q = new LinkedList<>();

        visited[s] = true;
        q.add(s);

        while (q.isEmpty() == false) {
            int u = q.poll();
            System.out.print(u + " ");

            for (int v : adj.get(u)) {
                if (visited[v] == false) {
                    visited[v] = true;
                    q.add(v);
                }
            }
        }
    }

    static void BFSDin(ArrayList<ArrayList<Integer>> adj, int V) {
        boolean[] visited = new boolean[V];
        int count = 0;        // for counting number of islands
        for (int i = 0; i < V; i++)
            visited[i] = false;
        for (int i = 0; i < V; i++) {
            if (visited[i] == false) {
                BFS(adj, i, visited);
                count++;    // every islands source will be counted, as
                            // its nodes will be marked visited by BFS
            }
        }
    }

    public static void main(String[] args) {
        int V = 7;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        addEdge(adj, 0, 1); addEdge(adj, 5, 6); addEdge(adj, 4, 6);
        addEdge(adj, 0, 2); addEdge(adj, 2, 3); addEdge(adj, 1, 3); 
        addEdge(adj, 4, 5);
        
        System.out.println("Following is Breadth First Traversal: ");
        BFSDin(adj, V);
    }
}
```

## Depth First Search

#### How it works

* Depth first search is achieved with recursion just like tree
* To avoid cyclic loops, a boolean array containing visited nodes is maintain and passed in the recursion

#### Disconnected Graph:  How it works&#x20;

* same as BFS, the algorithm is called for every node assuming it is the source vertice of the disconnected graph.
* we keep track of visited vertices in an boolean array just like DFS but this visited array is present in recursion call from source caller to DFS algorithm (in Java : array is pass by reference)
* this visited array will avoid calling DFS for nodes of island as they would have been visited&#x20;

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    static void DFSRec(ArrayList<ArrayList<Integer>> adj, int s, boolean[] visited) {
        visited[s] = true;
        System.out.print(s + " ");

        for (int u : adj.get(s)) {
            if (visited[u] == false)
                DFSRec(adj, u, visited);
        }
    }

    static void DFS(ArrayList<ArrayList<Integer>> adj, int V) {
        boolean[] visited = new boolean[V];
        int count = 0;
        
        for (int i = 0; i < V; i++)
            visited[i] = false;

        // for include disconnected graphs as well
        for (int i = 0; i < V; i++) {
            if (visited[i] == false) {
                DFSRec(adj, i, visited);
                count++;
            }
        }
    }

    public static void main(String[] args) {
        int V = 5;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        addEdge(adj, 0, 1); addEdge(adj, 0, 2); addEdge(adj, 1, 2);
        addEdge(adj, 3, 4);

        System.out.println("Following is Depth First Traversal for disconnected graphs: ");
        DFS(adj, V);
    }
}
```

## ------------

## BFS : Shortest Path in an Unweighted Graph

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    static void BFS(ArrayList<ArrayList<Integer>> adj, int V, int s, int[] dist) {
        boolean[] visited = new boolean[V];
        for (int i = 0; i < V; i++)
            visited[i] = false;

        Queue<Integer> q = new LinkedList<>();

        visited[s] = true;
        q.add(s);

        while (q.isEmpty() == false) {
            int u = q.poll();

            for (int v : adj.get(u)) {
                if (visited[v] == false) {
                    dist[v] = dist[u] + 1;
                    visited[v] = true;
                    q.add(v);
                }
            }
        }
    }

    public static void main(String[] args) {
        int V = 4;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        addEdge(adj, 0, 1);
        addEdge(adj, 1, 2);
        addEdge(adj, 2, 3);
        addEdge(adj, 0, 2);
        addEdge(adj, 1, 3);
        int[] dist = new int[V];
        for (int i = 0; i < V; i++) {
            dist[i] = Integer.MAX_VALUE;
        }
        dist[0] = 0;
        BFS(adj, V, 0, dist);

        for (int i = 0; i < V; i++) {
            System.out.print(dist[i] + " ");
        }
    }
}
```

## DFS : Detect Cycle in Undirected Graph

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    static boolean DFSRec(ArrayList<ArrayList<Integer>> adj, int s, boolean[] visited, int parent) {
        visited[s] = true;

        for (int u : adj.get(s)) {
            if (visited[u] == false) {
                if (DFSRec(adj, u, visited, s) == true) {
                    return true;
                }
            } else if (u != parent) {
                return true;
            }
        }
        return false;
    }

    static boolean DFS(ArrayList<ArrayList<Integer>> adj, int V) {
        boolean[] visited = new boolean[V];
        for (int i = 0; i < V; i++)
            visited[i] = false;

        for (int i = 0; i < V; i++) {
            if (visited[i] == false)
                if (DFSRec(adj, i, visited, -1) == true)
                    return true;
        }
        return false;
    }

    public static void main(String[] args) {
        int V = 6;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        addEdge(adj, 0, 1);
        addEdge(adj, 1, 2);
        addEdge(adj, 2, 4);
        addEdge(adj, 4, 5);
        addEdge(adj, 1, 3);
        addEdge(adj, 2, 3);

        if (DFS(adj, V) == true)
            System.out.println("Cycle found");
        else
            System.out.println("No cycle found");
    }
}
```

## DFS : Part 1 : Detect Cycle in a Directed Graph

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    static boolean DFSRec(ArrayList<ArrayList<Integer>> adj, int s, boolean[] visited, boolean[] recSt) {
        visited[s] = true;
        recSt[s] = true;

        for (int u : adj.get(s)) {
            if (visited[u] == false && DFSRec(adj, u, visited, recSt) == true) {
                return true;
            } else if (recSt[u] == true) {
                return true;
            }
        }
        recSt[s] = false;
        return false;
    }

    static boolean DFS(ArrayList<ArrayList<Integer>> adj, int V) {
        boolean[] visited = new boolean[V];
        for (int i = 0; i < V; i++)
            visited[i] = false;

        boolean[] recSt = new boolean[V];
        for (int i = 0; i < V; i++)
            recSt[i] = false;

        for (int i = 0; i < V; i++) {
            if (visited[i] == false)
                if (DFSRec(adj, i, visited, recSt) == true)
                    return true;
        }
        return false;
    }

    public static void main(String[] args) {
        int V = 6;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        addEdge(adj, 0, 1);
        addEdge(adj, 2, 1);
        addEdge(adj, 2, 3);
        addEdge(adj, 3, 4);
        addEdge(adj, 4, 5);
        addEdge(adj, 5, 3);

        if (DFS(adj, V) == true)
            System.out.println("Cycle found");
        else
            System.out.println("No cycle found");
    }
}
```

## Topological Sorting (Kahn's BFS Based Algortihm)

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
    }

    static void topologicalSort(ArrayList<ArrayList<Integer>> adj, int V) {
        int[] in_degree = new int[V];

        for (int u = 0; u < V; u++) {
            for (int x : adj.get(u))
                in_degree[x]++;
        }

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < V; i++)
            if (in_degree[i] == 0)
                q.add(i);

        while (q.isEmpty() == false) {
            int u = q.poll();
            System.out.print(u + " ");

            for (int x : adj.get(u))
                if (--in_degree[x] == 0)
                    q.add(x);
        }
    }

    public static void main(String[] args) {
        int V = 5;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        addEdge(adj, 0, 2);
        addEdge(adj, 0, 3);
        addEdge(adj, 1, 3);
        addEdge(adj, 1, 4);
        addEdge(adj, 2, 3);

        System.out.println("Following is a Topological Sort of");
        topologicalSort(adj, V);
    }
}
```

## Part 2 : Detect Cycle in a Directed Graph ( using kahn's Algorithm )

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
    }

    static void topologicalSort(ArrayList<ArrayList<Integer>> adj, int V) {
        int[] in_degree = new int[V];

        for (int u = 0; u < V; u++) {
            for (int x : adj.get(u))
                in_degree[x]++;
        }

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < V; i++)
            if (in_degree[i] == 0)
                q.add(i);

        int count = 0;
        while (q.isEmpty() == false) {
            int u = q.poll();

            for (int x : adj.get(u))
                if (--in_degree[x] == 0)
                    q.add(x);

            count++;
        }
        if (count != V) {
            System.out.println("There exists a cycle in the graph");
        } else {
            System.out.println("There exists no cycle in the graph");
        }
    }

    public static void main(String[] args) {
        int V = 5;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        addEdge(adj, 0, 1);
        addEdge(adj, 4, 1);
        addEdge(adj, 1, 2);
        addEdge(adj, 2, 3);
        addEdge(adj, 3, 1);

        topologicalSort(adj, V);
    }
}
```

## Topological Sorting (DFS Based Algorithm)

```java
import java.util.*;

class Graph {

    static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v) {
        adj.get(u).add(v);
    }

    static void DFS(ArrayList<ArrayList<Integer>> adj, int u, Stack<Integer> st, boolean visited[]) {
        visited[u] = true;

        for (int v : adj.get(u)) {
            if (visited[v] == false)
                DFS(adj, v, st, visited);
        }
        st.push(new Integer(u));
    }

    static void topologicalSort(ArrayList<ArrayList<Integer>> adj, int V) {
        boolean[] visited = new boolean[V];
        for (int i = 0; i < V; i++)
            visited[i] = false;
        Stack<Integer> st = new Stack<Integer>();

        for (int u = 0; u < V; u++) {
            if (visited[u] == false) {
                DFS(adj, u, st, visited);
            }
        }

        while (st.empty() == false)
            System.out.print(st.pop() + " ");

    }

    public static void main(String[] args) {
        int V = 5;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>(V);

        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<Integer>());

        addEdge(adj, 0, 1);
        addEdge(adj, 1, 3);
        addEdge(adj, 2, 3);
        addEdge(adj, 3, 4);
        addEdge(adj, 2, 4);

        System.out.println("Following is a Topological Sort of");
        topologicalSort(adj, V);
    }
}
```

## Shortest Path in Directed Acyclic Graph

```java
import java.util.Iterator;
import java.util.LinkedList;
import java.util.Stack;

class AdjListNode {
    private int v;
    private int weight;

    AdjListNode(int _v, int _w) {
        v = _v;
        weight = _w;
    }

    int getV() {
        return v;
    }

    int getWeight() {
        return weight;
    }
}

class Graph {
    private int V;
    private LinkedList<AdjListNode> adj[];

    Graph(int v) {
        V = v;
        adj = new LinkedList[V];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList<AdjListNode>();
    }

    void addEdge(int u, int v, int weight) {
        AdjListNode node = new AdjListNode(v, weight);
        adj[u].add(node);
    }

    void topologicalSortUtil(int v, Boolean visited[], Stack stack) {

        visited[v] = true;
        Integer i;

        Iterator<AdjListNode> it = adj[v].iterator();
        while (it.hasNext()) {
            AdjListNode node = it.next();
            if (!visited[node.getV()])
                topologicalSortUtil(node.getV(), visited, stack);
        }

        stack.add(v);
    }

    void shortestPath(int s) {
        Stack stack = new Stack();
        int dist[] = new int[V];

        Boolean visited[] = new Boolean[V];
        for (int i = 0; i < V; i++)
            visited[i] = false;

        for (int i = 0; i < V; i++)
            if (visited[i] == false)
                topologicalSortUtil(i, visited, stack);

        for (int i = 0; i < V; i++)
            dist[i] = Integer.MAX_VALUE;
        dist[s] = 0;

        while (stack.empty() == false) {
            int u = (int) stack.pop();

            Iterator<AdjListNode> it;
            if (dist[u] != Integer.MAX_VALUE) {
                it = adj[u].iterator();
                while (it.hasNext()) {
                    AdjListNode i = it.next();
                    if (dist[i.getV()] > dist[u] + i.getWeight())
                        dist[i.getV()] = dist[u] + i.getWeight();
                }
            }
        }

        for (int i = 0; i < V; i++) {
            if (dist[i] == Integer.MAX_VALUE)
                System.out.print("INF ");
            else
                System.out.print(dist[i] + " ");
        }
    }
}

class Main {
    public static void main(String args[]) {

        Graph g = new Graph(6);
        g.addEdge(0, 1, 2);
        g.addEdge(0, 4, 1);
        g.addEdge(1, 2, 3);
        g.addEdge(4, 2, 2);
        g.addEdge(4, 5, 4);
        g.addEdge(2, 3, 6);
        g.addEdge(5, 3, 1);

        int s = 0;
        System.out.println("Following are shortest distances " + "from source " + s);
        g.shortestPath(s);
    }
}
```

## Prim's Algorithm / Minimum Spanning Tree

```java
import java.util.*;
import java.lang.*;
import java.io.*;

class Gfg {

    static final int V = 4;

    public static int primMST(int graph[][]) {

        int[] key = new int[V];
        int res = 0;
        Arrays.fill(key, Integer.MAX_VALUE);
        boolean[] mSet = new boolean[V];
        key[0] = 0;

        for (int count = 0; count < V; count++) {
            int u = -1;

            for (int i = 0; i < V; i++)
                if (!mSet[i] && (u == -1 || key[i] < key[u]))
                    u = i;
            mSet[u] = true;
            res += key[u];

            for (int v = 0; v < V; v++)

                if (graph[u][v] != 0 && mSet[v] == false)
                    key[v] = Math.min(key[v], graph[u][v]);
        }
        return res;
    }

    public static void main(String[] args) {
        int graph[][] = new int[][] { { 0, 5, 8, 0 }, { 5, 0, 10, 15 }, { 8, 10, 0, 20 }, { 0, 15, 20, 0 }, };

        System.out.print(primMST(graph));
    }
}
```

## Dijkstra's Shortest Path Algorithm

```java
import java.util.*;
import java.lang.*;
import java.io.*;

class Gfg {

    static final int V = 4;

    public static int[] djikstra(int graph[][], int src) {

        int[] dist = new int[V];
        int res = 0;
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;
        boolean[] fin = new boolean[V];

        for (int count = 0; count < V - 1; count++) {
            int u = -1;

            for (int i = 0; i < V; i++)
                if (!fin[i] && (u == -1 || dist[i] < dist[u]))
                    u = i;
            fin[u] = true;

            for (int v = 0; v < V; v++)

                if (graph[u][v] != 0 && fin[v] == false)
                    dist[v] = Math.min(dist[v], dist[u] + graph[u][v]);
        }
        return dist;
    }

    public static void main(String[] args) {
        int graph[][] = new int[][] { { 0, 50, 100, 0 }, { 50, 0, 30, 200 }, { 100, 30, 0, 20 }, { 0, 200, 20, 0 }, };

        for (int x : djikstra(graph, 0)) {
            System.out.print(x + " ");
        }

    }
}
```

## Kosaraju's Algorithm Part 1

```java
import java.io.*;
import java.util.*;
import java.util.LinkedList;

class Graph {
    private int V;
    private LinkedList<Integer> adj[];

    Graph(int v) {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList();
    }

    void addEdge(int v, int w) {
        adj[v].add(w);
    }

    void DFSUtil(int v, boolean visited[]) {

        visited[v] = true;
        System.out.print(v + " ");

        int n;

        Iterator<Integer> i = adj[v].iterator();
        while (i.hasNext()) {
            n = i.next();
            if (!visited[n])
                DFSUtil(n, visited);
        }
    }

    Graph getTranspose() {
        Graph g = new Graph(V);
        for (int v = 0; v < V; v++) {
            Iterator<Integer> i = adj[v].listIterator();
            while (i.hasNext())
                g.adj[i.next()].add(v);
        }
        return g;
    }

    void fillOrder(int v, boolean visited[], Stack stack) {
        visited[v] = true;

        Iterator<Integer> i = adj[v].iterator();
        while (i.hasNext()) {
            int n = i.next();
            if (!visited[n])
                fillOrder(n, visited, stack);
        }

        stack.push(new Integer(v));
    }

    void printSCCs() {
        Stack stack = new Stack();

        boolean visited[] = new boolean[V];
        for (int i = 0; i < V; i++)
            visited[i] = false;

        for (int i = 0; i < V; i++)
            if (visited[i] == false)
                fillOrder(i, visited, stack);

        Graph gr = getTranspose();

        for (int i = 0; i < V; i++)
            visited[i] = false;

        while (stack.empty() == false) {
            int v = (int) stack.pop();

            if (visited[v] == false) {
                gr.DFSUtil(v, visited);
                System.out.println();
            }
        }
    }

    public static void main(String args[]) {
        Graph g = new Graph(5);
        g.addEdge(1, 0);
        g.addEdge(0, 2);
        g.addEdge(2, 1);
        g.addEdge(0, 3);
        g.addEdge(3, 4);

        System.out.println("Following are strongly connected components " + "in given graph ");
        g.printSCCs();
    }
}
```

## Bellman Ford Shortest Path Algorithm

```java
import java.util.*;
import java.lang.*;
import java.io.*;

class Graph {

    class Edge {
        int src, dest, weight;

        Edge() {
            src = dest = weight = 0;
        }
    };

    int V, E;
    Edge edge[];

    Graph(int v, int e) {
        V = v;
        E = e;
        edge = new Edge[e];
        for (int i = 0; i < e; ++i)
            edge[i] = new Edge();
    }

    void BellmanFord(Graph graph, int src) {
        int V = graph.V, E = graph.E;
        int dist[] = new int[V];

        for (int i = 0; i < V; ++i)
            dist[i] = Integer.MAX_VALUE;
        dist[src] = 0;

        for (int i = 1; i < V; ++i) {
            for (int j = 0; j < E; ++j) {
                int u = graph.edge[j].src;
                int v = graph.edge[j].dest;
                int weight = graph.edge[j].weight;
                if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v])
                    dist[v] = dist[u] + weight;
            }
        }

        for (int j = 0; j < E; ++j) {
            int u = graph.edge[j].src;
            int v = graph.edge[j].dest;
            int weight = graph.edge[j].weight;
            if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                System.out.println("Graph contains negative weight cycle");
                return;
            }
        }
        printArr(dist, V);
    }

    void printArr(int dist[], int V) {
        System.out.println("Vertex Distance from Source");
        for (int i = 0; i < V; ++i)
            System.out.println(i + "\t\t" + dist[i]);
    }

    public static void main(String[] args) {
        int V = 4;
        int E = 5;

        Graph graph = new Graph(V, E);

        // add edge 0-1 (or A-B)
        graph.edge[0].src = 0;
        graph.edge[0].dest = 1;
        graph.edge[0].weight = 1;

        // add edge 0-2 (or A-C)
        graph.edge[1].src = 0;
        graph.edge[1].dest = 2;
        graph.edge[1].weight = 4;

        // add edge 1-2 (or B-C)
        graph.edge[2].src = 1;
        graph.edge[2].dest = 2;
        graph.edge[2].weight = -3;

        // add edge 1-3 (or B-D)
        graph.edge[3].src = 1;
        graph.edge[3].dest = 3;
        graph.edge[3].weight = 2;

        // add edge 2-3 (or C-D)
        graph.edge[4].src = 2;
        graph.edge[4].dest = 3;
        graph.edge[4].weight = 3;

        graph.BellmanFord(graph, 0);
    }
}
```

## Articulation Point

```java
import java.io.*; 
import java.util.*; 
import java.util.LinkedList; 


class Graph 
{ 
    private int V; 

    private LinkedList<Integer> adj[]; 
    int time = 0; 
    static final int NIL = -1; 

    Graph(int v) 
    { 
        V = v; 
        adj = new LinkedList[v]; 
        for (int i=0; i<v; ++i) 
            adj[i] = new LinkedList(); 
    } 

    void addEdge(int v, int w) 
    { 
        adj[v].add(w);  
        adj[w].add(v);  
    } 

    void APUtil(int u, boolean visited[], int disc[], 
                int low[], int parent[], boolean ap[]) 
    { 

        int children = 0; 

        visited[u] = true; 

        disc[u] = low[u] = ++time; 

        Iterator<Integer> i = adj[u].iterator(); 
        while (i.hasNext()) 
        { 
            int v = i.next(); 
            if (!visited[v]) 
            { 
                children++; 
                parent[v] = u; 
                APUtil(v, visited, disc, low, parent, ap); 


                low[u] = Math.min(low[u], low[v]); 


                if (parent[u] == NIL && children > 1) 
                    ap[u] = true; 

                if (parent[u] != NIL && low[v] >= disc[u]) 
                    ap[u] = true; 
            } 

            else if (v != parent[u]) 
                low[u] = Math.min(low[u], disc[v]); 
        } 
    } 

    void AP() 
    { 

        boolean visited[] = new boolean[V]; 
        int disc[] = new int[V]; 
        int low[] = new int[V]; 
        int parent[] = new int[V]; 
        boolean ap[] = new boolean[V];


        for (int i = 0; i < V; i++) 
        { 
            parent[i] = NIL; 
            visited[i] = false; 
            ap[i] = false; 
        } 

        for (int i = 0; i < V; i++) 
            if (visited[i] == false) 
                APUtil(i, visited, disc, low, parent, ap); 

        for (int i = 0; i < V; i++) 
            if (ap[i] == true) 
                System.out.print(i+" "); 
    } 

    public static void main(String args[]) 
    { 
        System.out.println("Articulation points in first graph "); 
        Graph g = new Graph(5); 
        g.addEdge(1, 0); 
        g.addEdge(0, 2); 
        g.addEdge(2, 1); 
        g.addEdge(0, 3); 
        g.addEdge(3, 4); 
        g.AP(); 
        System.out.println(); 
    } 
}
```

## Bridges in Graph

```java
import java.io.*; 
import java.util.*; 
import java.util.LinkedList; 

class Graph 
{ 
    private int V; 

    private LinkedList<Integer> adj[]; 
    int time = 0; 
    static final int NIL = -1; 

    Graph(int v) 
    { 
        V = v; 
        adj = new LinkedList[v]; 
        for (int i=0; i<v; ++i) 
            adj[i] = new LinkedList(); 
    } 

    void addEdge(int v, int w) 
    { 
        adj[v].add(w);  
        adj[w].add(v); 
    } 


    void bridgeUtil(int u, boolean visited[], int disc[], int low[], int parent[]) 
    { 

        visited[u] = true; 

        disc[u] = low[u] = ++time; 

        Iterator<Integer> i = adj[u].iterator(); 
        while (i.hasNext()) 
        { 
            int v = i.next(); 

            if (!visited[v]) 
            { 
                parent[v] = u; 
                bridgeUtil(v, visited, disc, low, parent); 


                low[u] = Math.min(low[u], low[v]); 


                if (low[v] > disc[u]) 
                    System.out.println(u+" "+v); 
            } 


            else if (v != parent[u]) 
                low[u] = Math.min(low[u], disc[v]); 
        } 
    } 

    void bridge() 
    { 
        boolean visited[] = new boolean[V]; 
        int disc[] = new int[V]; 
        int low[] = new int[V]; 
        int parent[] = new int[V]; 


        for (int i = 0; i < V; i++) 
        { 
            parent[i] = NIL; 
            visited[i] = false; 
        } 


        for (int i = 0; i < V; i++) 
            if (visited[i] == false) 
                bridgeUtil(i, visited, disc, low, parent); 
    } 

    public static void main(String args[]) 
    { 
        System.out.println("Bridges in first graph "); 
        Graph g = new Graph(5); 
        g.addEdge(1, 0); 
        g.addEdge(0, 2); 
        g.addEdge(2, 1); 
        g.addEdge(0, 3); 
        g.addEdge(3, 4); 
        g.bridge(); 
    }

}
```

## Tarjans Algorithm

```java
import java.io.*; 
import java.util.*; 

class Graph{ 

private int V; 

private LinkedList<Integer> adj[]; 
private int Time; 

@SuppressWarnings("unchecked") 
Graph(int v) 
{ 
    V = v; 
    adj = new LinkedList[v]; 

    for(int i = 0; i < v; ++i) 
        adj[i] = new LinkedList(); 

    Time = 0; 
} 

void addEdge(int v,int w) 
{ 
    adj[v].add(w); 
} 

void SCCUtil(int u, int low[], int disc[], boolean stackMember[], Stack<Integer> st) 
{ 
    disc[u] = Time; 
    low[u] = Time; 
    Time += 1; 
    stackMember[u] = true; 
    st.push(u); 

    int n; 

    Iterator<Integer> i = adj[u].iterator(); 

    while (i.hasNext()) 
    { 
        n = i.next(); 

        if (disc[n] == -1) 
        { 
            SCCUtil(n, low, disc, stackMember, st); 


            low[u] = Math.min(low[u], low[n]); 
        } 
        else if (stackMember[n] == true) 
        { 

            low[u] = Math.min(low[u], disc[n]); 
        } 
    } 

    int w = -1; 
    if (low[u] == disc[u]) 
    { 
        while (w != u) 
        { 
            w = (int)st.pop(); 
            System.out.print(w + " "); 
            stackMember[w] = false; 
        } 
        System.out.println(); 
    } 
} 

void SCC() 
{ 

    int disc[] = new int[V]; 
    int low[] = new int[V]; 
    for(int i = 0;i < V; i++) 
    { 
        disc[i] = -1; 
        low[i] = -1; 
    } 

    boolean stackMember[] = new boolean[V]; 
    Stack<Integer> st = new Stack<Integer>(); 

    for(int i = 0; i < V; i++) 
    { 
        if (disc[i] == -1) 
            SCCUtil(i, low, disc, stackMember, st); 
    } 
} 

public static void main(String args[]) 
{ 
    Graph g = new Graph(5); 

    g.addEdge(1, 0); 
    g.addEdge(0, 2); 
    g.addEdge(2, 1); 
    g.addEdge(0, 3); 
    g.addEdge(3, 4); 
    System.out.println("SSC in the graph "); 
    g.SCC(); 

} 
}
```

## Kruskal's Algorithm

```java
// Java program for Kruskal's algorithm to find Minimum 
// Spanning Tree of a given connected, undirected and 
// weighted graph 
import java.util.*;
import java.lang.*;
import java.io.*;

class Graph {
    // A class to represent a graph edge
    class Edge implements Comparable<Edge> {
        int src, dest, weight;

        // Comparator function used for sorting edges
        // based on their weight
        public int compareTo(Edge compareEdge) {
            return this.weight - compareEdge.weight;
        }
    };

    // A class to represent a subset for union-find
    class subset {
        int parent, rank;
    };

    int V, E; // V-> no. of vertices & E->no.of edges
    Edge edge[]; // collection of all edges

    // Creates a graph with V vertices and E edges
    Graph(int v, int e) {
        V = v;
        E = e;
        edge = new Edge[E];
        for (int i = 0; i < e; ++i)
            edge[i] = new Edge();
    }

    // A utility function to find set of an element i
    // (uses path compression technique)
    int find(subset subsets[], int i) {
        // find root and make root as parent of i (path compression)
        if (subsets[i].parent != i)
            subsets[i].parent = find(subsets, subsets[i].parent);

        return subsets[i].parent;
    }

    // A function that does union of two sets of x and y
    // (uses union by rank)
    void Union(subset subsets[], int x, int y) {
        int xroot = find(subsets, x);
        int yroot = find(subsets, y);

        // Attach smaller rank tree under root of high rank tree
        // (Union by Rank)
        if (subsets[xroot].rank < subsets[yroot].rank)
            subsets[xroot].parent = yroot;
        else if (subsets[xroot].rank > subsets[yroot].rank)
            subsets[yroot].parent = xroot;

        // If ranks are same, then make one as root and increment
        // its rank by one
        else {
            subsets[yroot].parent = xroot;
            subsets[xroot].rank++;
        }
    }

    // The main function to construct MST using Kruskal's algorithm
    void KruskalMST() {
        Edge result[] = new Edge[V]; // Tnis will store the resultant MST
        int e = 0; // An index variable, used for result[]
        int i = 0; // An index variable, used for sorted edges
        for (i = 0; i < V; ++i)
            result[i] = new Edge();

        // Step 1: Sort all the edges in non-decreasing order of their
        // weight. If we are not allowed to change the given graph, we
        // can create a copy of array of edges
        Arrays.sort(edge);

        // Allocate memory for creating V ssubsets
        subset subsets[] = new subset[V];
        for (i = 0; i < V; ++i)
            subsets[i] = new subset();

        // Create V subsets with single elements
        for (int v = 0; v < V; ++v) {
            subsets[v].parent = v;
            subsets[v].rank = 0;
        }

        i = 0; // Index used to pick next edge

        int res = 0;
        // Number of edges to be taken is equal to V-1
        while (e < V - 1) {
            // Step 2: Pick the smallest edge. And increment
            // the index for next iteration
            Edge next_edge = new Edge();
            next_edge = edge[i++];

            int x = find(subsets, next_edge.src);
            int y = find(subsets, next_edge.dest);

            // If including this edge does't cause cycle,
            // include it in result and increment the index
            // of result for next edge
            if (x != y) {
                result[e++] = next_edge;
                Union(subsets, x, y);

                res += next_edge.weight;
            }
            // Else discard the next_edge
        }

        // print the contents of result[] to display
        // the built MST

        System.out.println("Weight of MST is: " + res);
    }

    // Driver Program
    public static void main(String[] args) {

        int V = 5; // Number of vertices in graph
        int E = 7; // Number of edges in graph
        Graph graph = new Graph(V, E);

        // add edge 0-1
        graph.edge[0].src = 0;
        graph.edge[0].dest = 1;
        graph.edge[0].weight = 10;

        // add edge 0-2
        graph.edge[1].src = 0;
        graph.edge[1].dest = 2;
        graph.edge[1].weight = 8;

        // add edge 0-3
        graph.edge[2].src = 1;
        graph.edge[2].dest = 2;
        graph.edge[2].weight = 5;

        // add edge 1-3
        graph.edge[3].src = 1;
        graph.edge[3].dest = 3;
        graph.edge[3].weight = 3;

        // add edge 2-3
        graph.edge[4].src = 2;
        graph.edge[4].dest = 3;
        graph.edge[4].weight = 4;

        // add egde 2-4
        graph.edge[5].src = 2;
        graph.edge[5].dest = 4;
        graph.edge[5].weight = 12;

        // add edge 3-4
        graph.edge[6].src = 3;
        graph.edge[6].dest = 4;
        graph.edge[6].weight = 15;

        graph.KruskalMST();
    }
}
```



## Prim's Algorithm

```java
import java.util.*;
import java.lang.*;
import java.io.*;

class Gfg {

    static final int V = 4;

    public static int primMST(int graph[][]) {

        int[] key = new int[V];
        int res = 0;
        Arrays.fill(key, Integer.MAX_VALUE);
        boolean[] mSet = new boolean[V];
        key[0] = 0;

        for (int count = 0; count < V; count++) {
            int u = -1;

            for (int i = 0; i < V; i++)
                if (!mSet[i] && (u == -1 || key[i] < key[u]))
                    u = i;
            mSet[u] = true;
            res += key[u];

            for (int v = 0; v < V; v++)

                if (graph[u][v] != 0 && mSet[v] == false)
                    key[v] = Math.min(key[v], graph[u][v]);
        }
        return res;
    }

    public static void main(String[] args) {
        int graph[][] = new int[][] { { 0, 5, 8, 0 }, { 5, 0, 10, 15 }, { 8, 10, 0, 20 }, { 0, 15, 20, 0 }, };

        System.out.print(primMST(graph));
    }
}
```

## **Dijkstra's Algorithm Java**

```java
import java.util.*;
import java.lang.*;
import java.io.*;

class Gfg {

    static final int V = 4;

    public static int[] djikstra(int graph[][], int src) {

        int[] dist = new int[V];
        int res = 0;
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;
        boolean[] fin = new boolean[V];

        for (int count = 0; count < V - 1; count++) {
            int u = -1;

            for (int i = 0; i < V; i++)
                if (!fin[i] && (u == -1 || dist[i] < dist[u]))
                    u = i;
            fin[u] = true;

            for (int v = 0; v < V; v++)

                if (graph[u][v] != 0 && fin[v] == false)
                    dist[v] = Math.min(dist[v], dist[u] + graph[u][v]);
        }
        return dist;
    }

    public static void main(String[] args) {
        int graph[][] = new int[][] { { 0, 50, 100, 0 }, { 50, 0, 30, 200 }, { 100, 30, 0, 20 }, { 0, 200, 20, 0 }, };

        for (int x : djikstra(graph, 0)) {
            System.out.print(x + " ");
        }

    }
}
```

## **Kosaraju's Algorithm**

```java
import java.io.*;
import java.util.*;
import java.util.LinkedList;

class Graph {
    private int V;
    private LinkedList<Integer> adj[];

    Graph(int v) {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList();
    }

    void addEdge(int v, int w) {
        adj[v].add(w);
    }

    void DFSUtil(int v, boolean visited[]) {

        visited[v] = true;
        System.out.print(v + " ");

        int n;

        Iterator<Integer> i = adj[v].iterator();
        while (i.hasNext()) {
            n = i.next();
            if (!visited[n])
                DFSUtil(n, visited);
        }
    }

    Graph getTranspose() {
        Graph g = new Graph(V);
        for (int v = 0; v < V; v++) {
            Iterator<Integer> i = adj[v].listIterator();
            while (i.hasNext())
                g.adj[i.next()].add(v);
        }
        return g;
    }

    void fillOrder(int v, boolean visited[], Stack stack) {
        visited[v] = true;

        Iterator<Integer> i = adj[v].iterator();
        while (i.hasNext()) {
            int n = i.next();
            if (!visited[n])
                fillOrder(n, visited, stack);
        }

        stack.push(new Integer(v));
    }

    void printSCCs() {
        Stack stack = new Stack();

        boolean visited[] = new boolean[V];
        for (int i = 0; i < V; i++)
            visited[i] = false;

        for (int i = 0; i < V; i++)
            if (visited[i] == false)
                fillOrder(i, visited, stack);

        Graph gr = getTranspose();

        for (int i = 0; i < V; i++)
            visited[i] = false;

        while (stack.empty() == false) {
            int v = (int) stack.pop();

            if (visited[v] == false) {
                gr.DFSUtil(v, visited);
                System.out.println();
            }
        }
    }

    public static void main(String args[]) {
        Graph g = new Graph(5);
        g.addEdge(1, 0);
        g.addEdge(0, 2);
        g.addEdge(2, 1);
        g.addEdge(0, 3);
        g.addEdge(3, 4);

        System.out.println("Following are strongly connected components " + "in given graph ");
        g.printSCCs();
    }
}

```

## **Bellman Ford Shortest Path Algorithm**

```java
class Graph {

    class Edge {
        int src, dest, weight;

        Edge() {
            src = dest = weight = 0;
        }
    };

    int V, E;
    Edge edge[];

    Graph(int v, int e) {
        V = v;
        E = e;
        edge = new Edge[e];
        for (int i = 0; i < e; ++i)
            edge[i] = new Edge();
    }

    void BellmanFord(Graph graph, int src) {
        int V = graph.V, E = graph.E;
        int dist[] = new int[V];

        for (int i = 0; i < V; ++i)
            dist[i] = Integer.MAX_VALUE;
        dist[src] = 0;

        for (int i = 1; i < V; ++i) {
            for (int j = 0; j < E; ++j) {
                int u = graph.edge[j].src;
                int v = graph.edge[j].dest;
                int weight = graph.edge[j].weight;
                if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v])
                    dist[v] = dist[u] + weight;
            }
        }

        for (int j = 0; j < E; ++j) {
            int u = graph.edge[j].src;
            int v = graph.edge[j].dest;
            int weight = graph.edge[j].weight;
            if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                System.out.println("Graph contains negative weight cycle");
                return;
            }
        }
        printArr(dist, V);
    }

    void printArr(int dist[], int V) {
        System.out.println("Vertex Distance from Source");
        for (int i = 0; i < V; ++i)
            System.out.println(i + "\t\t" + dist[i]);
    }

    public static void main(String[] args) {
        int V = 4;
        int E = 5;

        Graph graph = new Graph(V, E);

        // add edge 0-1 (or A-B)
        graph.edge[0].src = 0;
        graph.edge[0].dest = 1;
        graph.edge[0].weight = 1;

        // add edge 0-2 (or A-C)
        graph.edge[1].src = 0;
        graph.edge[1].dest = 2;
        graph.edge[1].weight = 4;

        // add edge 1-2 (or B-C)
        graph.edge[2].src = 1;
        graph.edge[2].dest = 2;
        graph.edge[2].weight = -3;

        // add edge 1-3 (or B-D)
        graph.edge[3].src = 1;
        graph.edge[3].dest = 3;
        graph.edge[3].weight = 2;

        // add edge 2-3 (or C-D)
        graph.edge[4].src = 2;
        graph.edge[4].dest = 3;
        graph.edge[4].weight = 3;

        graph.BellmanFord(graph, 0);
    }
}
```

# Ex21 Count the Number of Nodes in the Left Subtree of a Binary Tree
## DATE: 13-11-2025
## AIM:
To design and implement a java program that constructs a binary tree from given level order input and counts the number of nodes present in the left subtree of the root node

## Algorithm
1. Start the program
2. Define a class Node to represent each node in the binary tree
3. Create a function insertLevelOrder(arr, root, i, n) to construct the binary tree from a given level order list.
4. Define a function countNodes(root) that returns the total number of nodes in a given subtree.
5.  Read or define the level order input array representing the binary tree.
6.  Construct the binary tree using the insertLevelOrder() function.
7.  Identify the left child of the root and call countNodes() on it.
8.  Display the number of nodes in the left subtree.
9.   Stop the program.

## Program:
```java
/*
Program to constructs a binary tree from given level order input and counts the number of nodes 
Developed by: Vamsi Krishna G
Register Number: 212223220120
*/

import java.util.*;

class Node {
    int data;
    Node left, right;
    Node(int data) {
        this.data = data;
        this.left = this.right = null;
    }
}

public class Main {
    static Node buildTree(int[] arr) {
        if (arr.length == 0) return null;
        Node root = new Node(arr[0]);
        Queue<Node> q = new LinkedList<>();
        q.add(root);
        int i = 1;

        while (!q.isEmpty() && i < arr.length) {
            Node current = q.poll();
            if (i < arr.length) {
                current.left = new Node(arr[i++]);
                q.add(current.left);
            }
            if (i < arr.length) {
                current.right = new Node(arr[i++]);
                q.add(current.right);
            }
        }

        return root;
    }

    static int countNodes(Node root) {
        if (root == null) return 0;
        return 1 + countNodes(root.left) + countNodes(root.right);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) arr[i] = sc.nextInt();
        Node root = buildTree(arr);

        if (root.left == null) {
            System.out.println(0);
        } else {
            System.out.println(countNodes(root.left));
        }
    }
}

```

## Output:
<img width="321" height="115" alt="image" src="https://github.com/user-attachments/assets/3d88487b-6602-4003-883c-9e1c2e5aafc6" />



## Result:
The program has been successfully implemented and executed.
It correctly constructs the binary tree from level order input and counts the number of nodes in the left subtree of the root node.


# Ex22 Searching for a Book ID in a Binary Search Tree (BST)
## DATE: 18-11-2025
## AIM:
To design and implement java program that constructs a Binary Search Tree (BST) using given Book IDs and checks whether a specific Book ID exists in the BST.
## Algorithm
1. Start the program.
2. Define a Node class to represent each node in the BST with attributes `data`, `left`, and `right`.
3. Define a function `insert(root, key)` to insert a new Book ID into the BST following BST rules:
   - If the BST is empty, create a new node.
   - If the key is smaller than the root’s data, insert it into the left subtree.
   - If the key is larger, insert it into the right subtree.
4. Define a function `search(root, key)` to check whether a Book ID exists in the BST:
   - If the root is `None`, return `False`.
   - If the root’s data matches the key, return `True`.
   - Otherwise, recursively search in the left or right subtree depending on the value.
5. In the main section:
   - Create an empty BST and insert a list of Book IDs into it.
   - Display the inserted Book IDs.
   - Prompt the user (or define in code) a Book ID to search for.
   - Use the `search()` function to determine if it exists.
   - Display the result.
6. Stop the program.

## Program:
```java
/*
Program to constructs a Binary Search Tree (BST) using given Book IDs 
Developed by: Vamsi Krishna G
Register Number: 212223220120
*/

import java.util.*;

public class BookIDSearch {
    static class Node {
        int data;
        Node left, right;
        Node(int data) {
            this.data = data;
        }
    }

    public static Node insert(Node root, int key) {
        if (root == null) return new Node(key);
        if (key < root.data) root.left = insert(root.left, key);
        else root.right = insert(root.right, key);
        return root;
    }

    public static boolean search(Node root, int key) {
        if (root == null) return false;
        if (root.data == key) return true;
        if (key < root.data) return search(root.left, key);
        else return search(root.right, key);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Node root = null;
        for (int i = 0; i < n; i++) {
            root = insert(root, sc.nextInt());
        }
        int q = sc.nextInt();
        while (q-- > 0) {
            int key = sc.nextInt();
            System.out.println(search(root, key) ? "Found" : "Not Found");
        }
    }
}

```

## Output:
<img width="426" height="184" alt="image" src="https://github.com/user-attachments/assets/2f3cb628-3246-4a10-88bf-bbce3361bed2" />



## Result:
The program has been successfully implemented and executed.
It constructs a Binary Search Tree from the given Book IDs and accurately determines whether a queried Book ID exists in the library system.


# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## DATE: 20-11-2025
## AIM:
To design and implement a java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.
## Algorithm
1. Start the program.
2. Represent the city junction map as a graph using an adjacency list (dictionary).
3. Define a function `bfs(graph, start)` that performs Breadth-First Search traversal:
   - Initialize a queue and a list to keep track of visited junctions.
   - Enqueue the starting junction.
   - While the queue is not empty:
     - Dequeue a junction and mark it as visited.
     - Print or store the junction in traversal order.
4. In the main section:
   - Define the city map as a graph (each node represents a junction).
   - Take a starting junction as input (or use a fixed source).
   - Call the `bfs()` function to display reachable locations.
5. Stop the program.  

## Program:
```java
/*
Program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph
Developed by: Vamsi Krishna G
Register Number: 212220220120
*/

import java.util.*;

public class EmergencyRouteBFS {
    public static void addEdge(List<List<Integer>> g, int u, int v) {
        g.get(u).add(v);
        g.get(v).add(u);
    }

    public static void bfs(List<List<Integer>> g, int src, boolean[] visited) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(src);
        visited[src] = true;
        while (!q.isEmpty()) {
            int curr = q.poll();
            System.out.print(curr + " ");
            for (int neighbor : g.get(curr)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.offer(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i < n; i++) g.add(new ArrayList<>());
        for (int i = 0; i < e; i++) addEdge(g, sc.nextInt(), sc.nextInt());
        int src = sc.nextInt();
        bfs(g, src, new boolean[n]);
    }
}

```

## Output:
<img width="332" height="209" alt="image" src="https://github.com/user-attachments/assets/1ba61535-b716-47f6-82f6-f07e473a9874" />



## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.


# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## DATE: 21-11-2025
## AIM:
To design and implement a java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
The number of reachable attractions from the same starting point using Breadth-First Search (BFS)


## Algorithm
1. Start the program.
2. Represent the heritage town map as a graph using a HashMap where each key is an attraction and its value is a list of connected attractions (walking paths).
3. Implement a BFS traversal to:
   - Visit all reachable attractions from a given starting attraction.
   - Count the total number of reachable attractions.
4. Implement another BFS-based shortest path algorithm that:
   - Uses a queue and a distance map.
   - Tracks the shortest number of hops (edges) from the start to the target attraction.
5. In the `main()` method:
   - Define the map (graph).
   - Take a starting and target attraction.
   - Display the reachable attractions and the shortest distance.
6. Stop the program.  

## Program:
```java
/*
Program to determine Shortest Path and Reachability in a Heritage Town using BFS
Developed by: Vamsi Krishna G
Register Number: 212223220120
*/

import java.util.*;

public class TouristNavigation {
    
    public static int bfs(List<List<Integer>> graph, int start, int target, int n) {
        boolean[] visited = new boolean[n];
        int[] dist = new int[n];
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        visited[start] = true;
        dist[start] = 0;

        while (!q.isEmpty()) {
            int curr = q.poll();
            if (curr == target) return dist[curr];
            for (int neigh : graph.get(curr)) {
                if (!visited[neigh]) {
                    visited[neigh] = true;
                    dist[neigh] = dist[curr] + 1;
                    q.offer(neigh);
                }
            }
        }
        return -1;
    }

    public static void dfs(List<List<Integer>> graph, boolean[] visited, int node) {
        visited[node] = true;
        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                dfs(graph, visited, neighbor);
            }
        }
    }

    public static int countReachable(boolean[] visited) {
        int count = 0;
        for (boolean v : visited) if (v) count++;
        return count;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt(), v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int start = sc.nextInt();
        int target = sc.nextInt();

        int shortest = bfs(graph, start, target, n);
        boolean[] visited = new boolean[n];
        dfs(graph, visited, start);
        int reachable = countReachable(visited);

        System.out.println("Shortest path from start to target: " + shortest);
        System.out.println("Total reachable attractions from start: " + reachable);
    }
}

```

## Output:
<img width="927" height="235" alt="image" src="https://github.com/user-attachments/assets/81ebe51d-83b2-4603-9cf9-edbf6113a8d7" />



## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.


# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm
## DATE: 24-11-2025
## AIM:
To design and implement a java program that helps an electric vehicle (EV) find the shortest travel time from its current block to the nearest charging station using Dijkstra’s shortest path algorithm.
## Algorithm
1. Start the program
2. Represent the city map as a weighted graph, where nodes represent blocks and edges represent travel times.
3. Take the current block of the EV as the source node
4. Store the locations of all charging stations
5. Use Dijkstra’s algorithm to compute the shortest distance from the source node to all other nodes in the graph.
6. Compare distances to find the nearest charging station with the minimum travel time
7. Display the shortest path and the total travel time
8. If no charging station is reachable, display an appropriate message
9. Stop the program   

## Program:
```java
/*
Program to find the Fastest Route to a Charging Station using Dijkstra’s Algorithm
Developed by: Vamsi Krishna G
Register Number: 212223220120
*/

import java.util.*;

public class EVChargingNavigation {

    static class Pair {
        int node, time;
        Pair(int node, int time) {
            this.node = node;
            this.time = time;
        }
    }

    static int findNearestChargingStation(int n, List<List<Pair>> graph, int source, Set<Integer> stations) {
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        PriorityQueue<Pair> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a.time));
        pq.offer(new Pair(source, 0));

        while (!pq.isEmpty()) {
            Pair current = pq.poll();
            for (Pair neighbor : graph.get(current.node)) {
                int newDist = dist[current.node] + neighbor.time;
                if (newDist < dist[neighbor.node]) {
                    dist[neighbor.node] = newDist;
                    pq.offer(new Pair(neighbor.node, newDist));
                }
            }
        }

        int minTime = Integer.MAX_VALUE;
        for (int s : stations) {
            if (dist[s] < minTime) minTime = dist[s];
        }
        return minTime == Integer.MAX_VALUE ? -1 : minTime;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(), m = sc.nextInt();
        List<List<Pair>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < m; i++) {
            int u = sc.nextInt(), v = sc.nextInt(), w = sc.nextInt();
            graph.get(u).add(new Pair(v, w));
            graph.get(v).add(new Pair(u, w)); // Undirected
        }

        int source = sc.nextInt();
        int k = sc.nextInt();
        Set<Integer> stations = new HashSet<>();
        for (int i = 0; i < k; i++) stations.add(sc.nextInt());

        System.out.println(findNearestChargingStation(n, graph, source, stations));
    }
}

```

## Output:
<img width="304" height="310" alt="image" src="https://github.com/user-attachments/assets/e58d31e7-55ff-42fc-8c87-e1b71a6fbd5c" />



## Result:
The program has been successfully implemented and executed.
It uses Dijkstra’s algorithm to determine the shortest travel time from the EV’s current location to the nearest charging station and correctly handles cases where no station is reachable.

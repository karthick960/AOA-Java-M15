
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE:5/11/2025
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1.Initialize each vertex as its own component using Union–Find.
2.For every component, find the cheapest outgoing edge.
3.Add all selected cheapest edges to the MST (skip if already in same component).
4.Union the merged components and reduce the component count.
5.Repeat until only one component remains; the sum of chosen edges is the MST weight.  

## Program:
```
/*
Minimum Spanning Tree -Boruvka's Algorithm
Developed by: Karthick k
Register Number: 212222040070

import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    static int boruvkaMST(int V, List<Edge> edges) {
        parent = new int[V];
        for (int i = 0; i < V; i++)
            parent[i] = i;

        int numComponents = V;
        int MSTweight = 0;

        // Keep looping until we have a single component
        while (numComponents > 1) {
            int[] cheapest = new int[V];
            Arrays.fill(cheapest, -1);

            // Step 1: Find cheapest edge for each component
            for (int i = 0; i < edges.size(); i++) {
                Edge e = edges.get(i);
                int setU = find(e.src);
                int setV = find(e.dest);

                if (setU == setV) continue;

                if (cheapest[setU] == -1 || edges.get(cheapest[setU]).weight > e.weight)
                    cheapest[setU] = i;

                if (cheapest[setV] == -1 || edges.get(cheapest[setV]).weight > e.weight)
                    cheapest[setV] = i;
            }

            // Step 2: Add the selected cheapest edges to MST
            for (int i = 0; i < V; i++) {
                int edgeIndex = cheapest[i];
                if (edgeIndex != -1) {
                    Edge e = edges.get(edgeIndex);
                    int setU = find(e.src);
                    int setV = find(e.dest);

                    if (setU == setV)
                        continue;

                    // Print the chosen edge
                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);

                    MSTweight += e.weight;
                    union(setU, setV);
                    numComponents--;
                }
            }
        }

        return MSTweight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s;
        dest = d;
        weight = w;
    }
}

*/
```

## Output:
<img width="842" height="539" alt="image" src="https://github.com/user-attachments/assets/1d8ead19-5b6c-4f26-880f-07c5b3237a2d" />



## Result:
The program successfully implemented and the expected output is verified.

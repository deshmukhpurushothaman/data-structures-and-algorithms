# Bellman-Ford Algorithm

The Bellman-Ford Algorithm finds the shortest path from a source node to all other nodes in a weighted graph, handling negative weights. Unlike Dijkstra's algorithm, Bellman-Ford can detect negative weight cycles, making it a key algorithm for graphs that may have such cycles.

## Problem Statement

Given a graph with V vertices and E edges, and a source vertex src, find the shortest path from src to every other vertex. If a negative cycle exists that is reachable from the source, report it.

## Key Points of Bellman-Ford Algorithm

1. **Initialization:** Set the distance to the source node as `0` and all other nodes as `Infinity`.
2. **Relaxation:** Repeat `V-1` times (where `V` is the number of vertices) to relax all edges. If the distance to a vertex can be minimized by traversing an edge, update the distance.
3. **Check for Negative Cycles:** After `V-1` relaxations, if any edge can still be relaxed, a negative weight cycle exists in the graph.

## Steps

Initialize Distances: Set the source node distance to 0, and Infinity for all others.
Iterate and Relax: For each edge, update the distance if a shorter path is found.
Cycle Check: After the main loop, go through all edges one last time to check for further relaxation, indicating a negative weight cycle.
Code Implementation (JavaScript)
The following code implements the Bellman-Ford algorithm, including negative cycle detection.

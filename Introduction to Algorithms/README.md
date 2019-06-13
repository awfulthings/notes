# Introduction to Algorithms

## Rabin-Karp String Matching Algorithm

Umožňuje hledat podřetězec v řetězci v lineárním čase pomocí porovnáhí hash hodnoty založené na principu „posouvání okénka“.

## Lecture 15: Single-Source Shortest Paths Problem

## Minimum spanning tree vs shortest path tree
[wiki](https://cs.stackexchange.com/questions/18797/minimum-spanning-tree-vs-shortest-path)

**Shortest-path treey:** Path from **root** vertex V to any other vertex is shortest.
**Minimu spanning tree:** Tree without circles with minimum total weight. 

## Prim algorithm
- gives minimum spanning tree, 

### Dijkstra algorithm
- gives shortest path tree
- positive weight edges
- O(VE), where E = O(V^2)


### Bellmen-Ford algorithm
- +/- weight edges
- O(V+E)

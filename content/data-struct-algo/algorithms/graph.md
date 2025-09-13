# Graph Algorithms

## Breadth-frst search

* We use a queue as to keep track of which vertices to process next.
* When we start the search, our queue consists of only our start vertex we want to start searching from.
* Visit each vertex adjacent to the current vertex. If it has not yet been visited, mark as visited, and att it to the queue.
* If the current vertex has no unvisited vertices adjacent to it, remove the next vertex from the queue and make it the current vertex.
* If there are no more unvisited vertices adjacent to the current vertex, and there are no more vertices in the queue, the algorithm is complete.

## Dijkstra

Used for solving the shortes path problem with weighted graphs.

* We make the starting vertex our current vertex.
* We checl all the vertices adjacent to the current vertex and calculate and record the weights from the starting vertex to all known locations.
* To determine the next current vertex, we find the cheapest unvisited known vertex that can be reached from our starting vertex.
* Repeat the first 3 steps untill we have visited every vertex in the graph.
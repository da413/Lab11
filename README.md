How does each pathfinding algorithm calculate and prioritize paths?


The APathfinding script uses the A* algorithm, which keeps track of the actual cost of the path so far, as well as a heuristic cost calculation to set the priority of the next step based on the cost of both. The DPathfinding script instead uses the Dijkstra algorithm, which does not use a heuristic cost calculation to determine the priority of the next step, and instead explores all possible paths with only the actual cost being considered for prioritization. The Pathfinding script uses the BFS algorithm, which does not use an actual cost or a heuristic cost calculation, and simply explores all possible paths evenly until the goal is found.


What challenges arise when dynamically updating obstacles in real-time?


One challenge was implementing the FindPath and AddObstacle calls at the right times so that the algorithm would correctly account for obstacles during runtime. Since FindPath was initially called on start, the pathfinding would already be done before AddObstacle could activate. Another challenge was dynamically adding obstacles without manual input. The solution to both problems was to 1) call a coroutine that runs AddObstacle every half second and call FindPath in update to constantly check for obstacles, and 2) generate random values in the Vector2Int every 0.5 seconds within the bounds of the grid. 




Which algorithm should you choose and how should you adapt it for larger grids or open-world settings?


For the most part, the A* algorithm is the most efficient and fastest, since it considers the direction towards the goal in determining the priority of steps, meaning it would focus on moving in the correct direction rather than evenly in all directions. If used in larger grids or open worlds, some modifications would need to be made to prevent the algorithm from exploring the entire world at once. This could be an approach similar to Unity’s NavMesh system, which uses polygons based on the terrain rather than a grid, allowing for dynamic sizing and reducing the number of steps needed to be kept in memory. It could also restrict the search area to a radius around the AI, or employ a hierarchical approach to divide the world into larger regions, and allow the algorithm to search only within the region, or from the start region to the goal region.

What would your approach be if you were to add weighted cells (e.g., "difficult terrain" areas)?


If weighted cells were added, each cell in the grid array would have to have varying costs rather than each cost being set to either 1 or 0, with higher numbers representing the more difficult terrain. This would need to be used with either the A* or Dijkstra algorithm, so that the cost would then be used to determine the priority for the next step.

import heapq

def dijkstra(graph):
    minimum_spanning_tree = []
    visited = set()
    start_vertex = list(graph.keys())[0]
    
    edge_heap = [(weight, start_vertex, neighbor) for neighbor, weight in graph[start_vertex].items()]
    
    heapq.heapify(edge_heap)
    visited.add(start_vertex)
    
    while edge_heap:
        weight, source, destination = heapq.heappop(edge_heap)
        if destination not in visited:
            visited.add(destination)
            minimum_spanning_tree.append((source, destination, weight))
            for neighbor, weight in graph[destination].items():
                if neighbor not in visited:
                    heapq.heappush(edge_heap, (weight, destination, neighbor))
    
    return minimum_spanning_tree

graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'C': 2, 'D': 5},
    'C': {'A': 4, 'B': 2, 'D': 1},
    'D': {'B': 5, 'C': 1}
}

minimum_spanning_tree = dijkstra(graph)
print("Minimum Spanning Tree:")
for edge in minimum_spanning_tree:
    print(f"{edge[0]} - {edge[1]}: {edge[2]}")

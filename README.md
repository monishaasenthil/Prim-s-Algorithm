# Prim-s-Algorithm
import heapq
import networkx as nx
from treelib import Node, Tree

import matplotlib
matplotlib.use('TkAgg')  # Use TkAgg as the backend
import matplotlib.pyplot as plt

# Your plotting code here

plt.show()

 # 'Agg' is a non-interactive backend
import os
os.environ['MPLBACKEND'] = 'Agg'
import matplotlib.pyplot as plt

def prim(graph):
    # Choose an arbitrary starting vertex
    start_vertex = next(iter(graph))

    # Priority queue to store (weight, current_vertex, next_vertex) tuples
    priority_queue = [(weight, start_vertex, next_vertex) for next_vertex, weight in graph[start_vertex].items()]
    heapq.heapify(priority_queue)

    # Set to keep track of visited vertices
    visited = {start_vertex}

    # Minimum spanning tree
    min_spanning_tree = []

    # Tree to store the hierarchy of the minimum spanning tree
    tree = Tree()
    tree.create_node(start_vertex, start_vertex)  # Add the starting vertex to the tree

    while priority_queue:
        weight, current_vertex, next_vertex = heapq.heappop(priority_queue)

        if next_vertex not in visited:
            # Add the selected edge to the minimum spanning tree
            min_spanning_tree.append((current_vertex, next_vertex, weight))
            visited.add(next_vertex)

            # Add the edge to the tree structure
            tree.create_node(next_vertex, next_vertex, parent=current_vertex)

            # Add neighboring edges to the priority queue
            for neighbor, weight in graph[next_vertex].items():
                if neighbor not in visited:
                    heapq.heappush(priority_queue, (weight, next_vertex, neighbor))

    return min_spanning_tree, tree

# Example graph represented as an adjacency list
example_graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'C': 2, 'D': 5},
    'C': {'A': 4, 'B': 2, 'D': 1},
    'D': {'B': 5, 'C': 1}
}

min_spanning_tree, tree_structure = prim(example_graph)

# Print the minimum spanning tree edges
print("Minimum Spanning Tree:")
for edge in min_spanning_tree:
    print(edge)

# Visualize the minimum spanning tree using networkx and matplotlib
G = nx.Graph(example_graph)
pos = nx.spring_layout(G)  # Layout for visualization
nx.draw(G, pos, with_labels=True, font_weight='bold', node_size=700, node_color='lightblue')
nx.draw_networkx_edges(G, pos, edgelist=min_spanning_tree, edge_color='red', width=2)
plt.show()

# Print the tree structure
print("\nTree Structure:")
tree_structure.show()

output:
<img width="458" alt="image" src="https://github.com/monishaasenthil/Prim-s-Algorithm/assets/121919243/61f8f8b3-70f3-4ed0-9213-d5bb989676b9">





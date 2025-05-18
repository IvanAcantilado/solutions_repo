# Equivalent Resistance Using Graph Theory

## Calculating Equivalent Resistance Using Graph Theory

Calculating equivalent resistance is a fundamental problem in electrical circuits, essential for understanding and designing efficient systems. Traditional methods—based on applying series and parallel resistor rules—work well for simple setups but can become unwieldy for complex networks with many components. Graph theory offers a powerful and systematic alternative for analyzing such circuits.

By modeling a circuit as a graph—where nodes represent junctions and edges represent resistors weighted by their resistance values—we can algorithmically simplify and solve intricate networks. This graph-based approach not only streamlines manual calculations but also enables automated circuit analysis, making it particularly valuable in applications like simulation software, optimization, and large-scale network design.

Beyond its practical utility, studying equivalent resistance through graph theory provides deeper insight into the intersection of electrical engineering and mathematics. It showcases the broad applicability of graph theory across disciplines such as physics, engineering, and computer science.

### Equivalent Resistance Using Graph Theory

To calculate the equivalent resistance using graph theory, the circuit is first converted into a graph where:

- **Nodes** represent electrical junctions.
- **Edges** represent resistors with weights corresponding to resistance values.

The algorithm then works by identifying series and parallel resistor configurations and systematically reducing them:

- **Series**: Two resistors are in series if they are the only components connected between two nodes (degree 2, non-branching).
- **Parallel**: Resistors are in parallel if they connect the same pair of nodes.

The goal is to simplify the graph iteratively by identifying series and parallel connections of resistors, and replacing them with an equivalent single resistor, until only one equivalent resistance remains. We can use graph traversal techniques, such as Depth-First Search (DFS), to identify series and parallel combinations and reduce the graph accordingly.

#### Key Concepts:

**Series Connection**: Resistors in series simply add up:

$$
R_{eq} = R_1 + R_2 + \dots + R_n
$$

**Parallel Connection**: Resistors in parallel combine according to the reciprocal rule:

$$
\frac{1}{R_{eq}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n}
$$

---

### Pseudocode for Algorithm

<pre><code class="language-python">
        # Define a function that calculates the equivalent resistance using graph theory
def calculate_equivalent_resistance(graph):
    while len(graph.nodes) > 1:  # Continue until we have one node left
        # Step 1: Identify series connections
        for edge in graph.edges:
            if is_series_connection(edge):
                # Combine the resistances of the series connection
                combined_resistance = sum([edge.weight for edge in edge_list])
                graph.update_edge(edge, combined_resistance)
                break
        
        # Step 2: Identify parallel connections
        for edge in graph.edges:
            if is_parallel_connection(edge):
                # Combine the resistances of the parallel connection
                combined_resistance = 1 / sum([1 / edge.weight for edge in edge_list])
                graph.update_edge(edge, combined_resistance)
                break

    # Return the equivalent resistance (final remaining node's weight)
    return graph.get_node_weight(graph.nodes[0])


# Helper function to detect if a set of resistors are in series
def is_series_connection(edge):
    # Two resistors are in series if they are directly connected without any branching
    return edge.node_a in edge.node_b

# Helper function to detect if a set of resistors are in parallel
def is_parallel_connection(edge):
    # Resistors are in parallel if they are connected at the same nodes
    return edge.node_a == edge.node_b


# Graph class definition to represent the network of resistors
class Graph:
    def __init__(self):
        self.nodes = {}  # stores node references
        self.edges = {}  # stores edge data: (node1, node2) -> resistance_value

    def add_edge(self, node1, node2, resistance):
        # Add an edge between node1 and node2 with given resistance
        self.edges[(node1, node2)] = resistance

    def get_node_weight(self, node):
        # Returns the current resistance of the node (calculated iteratively)
        pass

    def update_edge(self, edge, new_resistance):
        # Update the edge with the new resistance
        self.edges[edge] = new_resistance
</code></pre>

### Python Code

<pre><code class="language-python">import networkx as nx

def calculate_equivalent_resistance(G, start, end):
    while True:
        simplified = False

        # Check for series connections
        for node in list(G.nodes):
            neighbors = list(G.neighbors(node))
            if len(neighbors) == 2 and node not in (start, end):
                n1, n2 = neighbors
                r1 = G[node][n1]['resistance']
                r2 = G[node][n2]['resistance']
                G.remove_node(node)
                G.add_edge(n1, n2, resistance=r1 + r2)
                simplified = True
                break

        if simplified:
            continue

        # Check for parallel edges
        for u, v in list(G.edges):
            parallel_edges = [e for e in G.edges if set(e) == set((u, v))]
            if len(parallel_edges) > 1:
                resistances = [G[edge[0]][edge[1]]['resistance'] for edge in parallel_edges]
                for edge in parallel_edges:
                    G.remove_edge(*edge)
                combined_resistance = 1 / sum(1/r for r in resistances)
                G.add_edge(u, v, resistance=combined_resistance)
                simplified = True
                break

        if not simplified:
            break

    try:
        # Assume a single path from start to end now
        return G[start][end]['resistance']
    except KeyError:
        raise ValueError("Cannot reduce to a single equivalent resistance between given nodes.")

# Example usage
def main():
    G = nx.Graph()
    G.add_edge('A', 'B', resistance=2)  # R1
    G.add_edge('B', 'C', resistance=3)  # R2
    G.add_edge('C', 'D', resistance=5)  # R3

    eq_resistance = calculate_equivalent_resistance(G, 'A', 'D')
    print(f"Equivalent Resistance between A and D: {eq_resistance} Ohms")

if __name__ == "__main__":
    main()
</code></pre>

**Output should be:**

<code>Equivalent Resistance between A and D: 10 Ohms</code>

#### Explanation:

- **Graph Representation**: The graph is created using a `Graph` class where edges represent resistors, and each edge has a weight representing the resistance.
- **Identifying Series Connections**: In the `is_series_connection` function, we check if two nodes are directly connected with no branching, meaning they are in series.
- **Identifying Parallel Connections**: In the `is_parallel_connection` function, we check if two nodes are connected at the same junction, which means they are in parallel.
- **Iterative Simplification**: The `calculate_equivalent_resistance` function runs iteratively, continuously simplifying the circuit until only one node remains, which represents the total equivalent resistance.

![image](https://github.com/user-attachments/assets/c70c11c5-1092-44b3-9192-1b696299b1d6)
![image](https://github.com/user-attachments/assets/3a5ae586-fc37-4edf-9ef5-09d9b50cc60e)

---

### Handling Nested Combinations

Nested combinations occur when there are both series and parallel connections within a circuit. The algorithm handles this by following these steps:

1. **Simplifying the Circuit**: First, it checks for simple series or parallel connections and reduces them to equivalent resistances.
2. **Recursive Application**: After each reduction, the algorithm rechecks the graph to see if new series or parallel combinations emerge due to the simplifications.
3. **Handling Deep Nesting**: If the graph contains deeply nested combinations (e.g., a series of parallel combinations or vice versa), the algorithm will repeatedly simplify the graph until it reaches a final, reduced form.

---

### Examples and Analysis

#### Simple Series Circuit

- **Circuit**: A simple series circuit with three resistors: $R_1 = 2\,\Omega$, $R_2 = 3\,\Omega$, $R_3 = 5\,\Omega$.
- **Graph Representation**: Nodes are connected in a straight line (no branching), so all resistors are in series.
- **Simplification**: The equivalent resistance is:

$$
R_{\text{eq}} = R_1 + R_2 + R_3 = 2 + 3 + 5 = 10\,\Omega
$$

#### Simple Parallel Circuit

- **Circuit**: Two resistors in parallel: $R_1 = 2\,\Omega$ and $R_2 = 3\,\Omega$.
- **Graph Representation**: The resistors are connected between the same two nodes.
- **Simplification**: The equivalent resistance is:

$$
\frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} = \frac{1}{2} + \frac{1}{3} \approx 0.833
$$

So,

$$
R_{\text{eq}} \approx 1.2\,\Omega
$$

#### Mixed Series-Parallel Circuit

- **Circuit**: Three resistors: $R_1 = 2\,\Omega$ in series with a parallel combination of $R_2 = 3\,\Omega$ and $R_3 = 5\,\Omega$.
- **Graph Representation**: First simplify the parallel resistors, then add $R_1$.
- **Simplification**: First, calculate the parallel combination:

$$
\frac{1}{R_{\parallel}} = \frac{1}{3} + \frac{1}{5} = \frac{8}{15} \Rightarrow R_{\parallel} = \frac{15}{8} \approx 1.88\,\Omega
$$

Then,

$$
R_{\text{eq}} = R_1 + R_{\parallel} = 2 + 1.88 = 3.88\,\Omega
$$

---

### Algorithm Efficiency and Potential Improvements

#### Efficiency:

- **Time Complexity**: The algorithm involves iterating over the graph to identify series and parallel combinations, which can be done in linear time for each edge. Therefore, the time complexity depends on the number of edges and nodes in the graph. In the worst case, this can be $O(E)$, where $E$ is the number of edges.
- **Space Complexity**: The space complexity is $O(N + E)$, where $N$ is the number of nodes and $E$ is the number of edges, as the graph structure needs to store both.

#### Potential Improvements:

1. **Optimizing Traversal**: Instead of checking all edges, we could prioritize edges that are more likely to lead to simplifications, reducing unnecessary iterations.
2. **Advanced Graph Algorithms**: Incorporating more advanced graph algorithms, such as those used in network flow analysis, could improve performance for larger, more complex circuits.
3. **Parallel Computation**: For very large circuits, parallelizing the algorithm could significantly reduce computation time, especially when simplifying disconnected components.

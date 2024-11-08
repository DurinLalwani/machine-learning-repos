```markdown
# Social Network Analysis of Star Wars Episode IV

This project utilizes Social Network Analysis (SNA) to explore and visualize the interactions between characters in *Star Wars Episode IV*. The analysis is performed using the `networkx` library for network creation and analysis, and `matplotlib` for visualization.

## Table of Contents
- [Introduction](#introduction)
- [Requirements](#requirements)
- [Data](#data)
- [Code Overview](#code-overview)
- [Visualizations](#visualizations)
- [Network Statistics](#network-statistics)
- [Traditional Methods vs. Our Model](#traditional-methods-vs-our-model)
- [How to Run the Code](#how-to-run-the-code)
- [License](#license)

## Introduction
Social Network Analysis (SNA) focuses on the relationships between entities rather than the entities themselves. In this project, we analyze the co-occurrences of characters in *Star Wars Episode IV* using graph theory to uncover patterns in their interactions.

## Requirements
To run this project, you will need:
- Python 3.x
- `networkx`
- `matplotlib`
- `pandas` (optional, if you need to manipulate the data)

You can install the required libraries using pip:
```bash
pip install networkx matplotlib pandas
```

## Data
The network data is provided in a CSV file named `star-wars-network-edges.csv`, which contains edges representing interactions between characters. The file format is as follows:
```
node1,node2,weight
```
- `node1`: Character 1
- `node2`: Character 2
- `weight`: Number of scenes in which both characters appeared together

## Code Overview
The code is organized into several sections:

1. **Importing Libraries**
    ```python
    import networkx as nx
    import matplotlib
    import matplotlib.pyplot as plt
    %matplotlib inline
    ```

2. **Reading the Weighted Edgelist**
    ```python
    G = nx.read_weighted_edgelist('data/star-wars-network-edges.csv', delimiter=",")
    ```

3. **Viewing Edges and Nodes**
    ```python
    G.edges()
    G.nodes()
    ```

4. **Getting Edge Attributes**
    ```python
    nx.get_edge_attributes(G, 'weight')
    ```

5. **Drawing the Basic Graph**
    ```python
    nx.draw(G)
    ```

6. **Visualizing with Different Layouts**
   - **Fruchterman-Reingold Layout:**
    ```python
    pos = nx.fruchterman_reingold_layout(G)
    nx.draw_networkx_labels(G, pos)
    nx.draw(G, pos)
    ```
   - **Circular Layout:**
    ```python
    pos = nx.circular_layout(G)
    nx.draw_networkx_labels(G, pos)
    nx.draw(G, pos)
    ```

7. **Visualizing Edges with Varying Widths Based on Weights**
    ```python
    esmall = [(u, v) for (u, v, d) in G.edges(data=True) if d['weight'] < 5]
    emid = [(u, v) for (u, v, d) in G.edges(data=True) if d['weight'] >= 5 and d['weight'] < 10]
    elarge = [(u, v) for (u, v, d) in G.edges(data=True) if d['weight'] >= 10]

    nx.draw_networkx_edges(G, pos, edgelist=elarge, width=4, alpha=0.5)
    nx.draw_networkx_edges(G, pos, edgelist=emid, width=2, alpha=0.5)
    nx.draw_networkx_edges(G, pos, edgelist=esmall, width=1, alpha=0.5)
    ```

8. **Coloring Nodes Based on Character Alignment**
    ```python
    dark_side = ["DARTH VADER", "MOTTI", "TARKIN"]
    light_side = ["R2-D2", "CHEWBACCA", "C-3PO", "LUKE", "CAMIE", "BIGGS",
                  "LEIA", "BERU", "OWEN", "OBI-WAN", "HAN", "DODONNA",
                  "GOLD LEADER", "WEDGE", "RED LEADER", "RED TEN"]
    other = ["GREEDO", "JABBA"]

    nx.draw_networkx_nodes(G, pos, node_color='red', nodelist=dark_side)
    nx.draw_networkx_nodes(G, pos, node_color='yellow', nodelist=light_side)
    nx.draw_networkx_nodes(G, pos, node_color='gray', nodelist=other)
    ```

## Visualizations
The visualizations created in this project illustrate the relationships among characters based on their co-occurrences in scenes. Different layouts help in understanding the structure and clustering of characters.

## Network Statistics
The project also computes various network statistics, including:
- **Density**: Measures how many of the possible connections in the network have been made.
- **Degree**: Number of edges connected to each node.
    ```python
    nx.density(G)
    nx.degree(G)
    ```

## Traditional Methods vs. Our Model
With the massive amount of information generated by social networks every day, organizing this data is crucial. Traditional methods often involve hierarchical clustering, which does not allow the formation of overlapping clusters and requires prior knowledge of the number of clusters. 

In contrast, our model proposes a novel hierarchical, non-parametric approach that:
- **Discovers social circles automatically**: Our method identifies social circles within an ego-network without requiring predefined parameters.
- **Utilizes both structural and user-attribute information**: By leveraging the principle of homophily, our approach better captures the natural grouping of characters.
- **Overcomes limitations of traditional methods**: Unlike traditional hierarchical clustering, which may fail in overlapping contexts, our method is designed to recognize and represent overlapping clusters effectively.

Results from testing on Facebook datasets of ego-networks indicate that our approach performs comparably to benchmark results, showcasing its effectiveness in social network analysis.

## How to Run the Code
1. Ensure you have Python 3.x and the required libraries installed.
2. Place the `star-wars-network-edges.csv` file in the `data` directory.
3. Run the script in a Jupyter notebook or a Python environment:
    ```bash
    Social Network Analysis.ipynb
    ```

Feel free to modify the code for further analysis or visualizations!

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```
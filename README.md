# Network-Analysis-with-Neo4j
Analysis of Knowledge Graph using graph algorithms in Neo4j. See the [Project Report](Project%20Report.pdf) for a complete and thorough overview.

## How to run the project

### Graph Database Creation using Neo4j
This project requires [Neo4j Desktop](https://neo4j.com/download/) to run.

After downloading Neo4j, create a new graph database and take note of the password. Open and run the graph database server, and it should be running on `bolt://localhost:7687`

Then, open the [Jupyter notebook](https://github.com/irsyadadam/Network-Analysis-with-Neo4j/blob/main/Graph%20Creation%20Pipeline/KGCreate.ipynb) for compiling the data into Neo4j. Change the code and insert database password where indicated
```python
driver = GraphDatabase.driver(uri = "bolt://localhost:7687", auth = ("neo4j",[insert password here]))
```
Then, run the notebook to compile the data into a graph database!

However, just having a graph database is not enough to integrate Neo4j into Python. In the graph database server, run the following Cypher query to create a *graph instance* in the database:
```cypher
CALL gds.graph.create(
'KG',
    ["Category", "Drug", "PMID", "Protein"],
    {
        HAS_RELATED_DRUG: {orientation: 'UNDIRECTED'},
        HAS_UNIREF_ID: {orientation: 'UNDIRECTED'},
        IS_IN_CATEGORY: {orientation: 'UNDIRECTED'},
        PMID_TARGET: {orientation: 'UNDIRECTED'}
    }
)
```
This creates a graph called "KG" that can be referenced to in our Python code.

### How to run in Python
For each of the Jupyter notebooks, make sure to update the password in the `GraphDatabase.driver` as above, and that you have created the "KG" graph instance. Then, running the rest of the notebook will run as intended! We have the following notebooks:
- [Degree Distribution and Betweenness](https://github.com/irsyadadam/Network-Analysis-with-Neo4j/blob/main/Degree_Betweenness.ipynb)
- [Common Neighbors](https://github.com/irsyadadam/Network-Analysis-with-Neo4j/blob/main/commonNeighbors.ipynb)
- [Community Detection and Community-wise Betweenness](https://github.com/irsyadadam/Network-Analysis-with-Neo4j/blob/main/Community%20Detection/louvain.ipynb)
- [FastRP and K-means Clustering](https://github.com/irsyadadam/Network-Analysis-with-Neo4j/blob/main/Dimension_Reduction/tSNEKG.ipynb)

## Contributions:
### [Degree_Betweenness]
##### Author: Ethan Young
Analysis and visualization of degree distribution and betweenness centrality

### [Network Pipeline]
##### Author: Irsyad Adam
Code to upload network in Neo4j

### [Community Detection]
##### Author: Andy Goh
Analysis of communities using Louvain and Betweenness

### [Dimension_Reduction]
##### Author: Irsyad Adam
Common Neighbors; Random Projection Node embeddings and visualization with UMAP, tSNE

  [Degree_Betweenness]: Degree_Betweenness.ipynb
  
  [Community Detection]: /Community%20Detection/
  
  [Dimension_Reduction]: /Dimension_Reduction/
  
  [Network Pipeline]: /Graph%20Creation%20Pipeline/


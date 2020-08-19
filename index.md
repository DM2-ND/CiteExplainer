# CGCT Datasets
Main contributors: [Mengxia Yu](myu2@nd.edu), [Wenhao Yu](wyu1@nd.edu), and [Meng Jiang](mjiang2@nd.edu)

## Motivation
Citation networks of scientific papers have been getting much attention. However, existing datasets cannot meet the requirements of scientists. 

In this project, we release 19 theme-related, infomation-rich, and appropriate-sized datasets for research of citation network of scientific papers. All the datsets are generated from [S2ORC](https://github.com/allenai/s2orc). We extract and clean the datasets following the principles below:

- For each dataset, we take a typical paper in a specific domain as a center and get its k-hop neighbours (mostly k = 3). So that the datasets are theme-related. 
- A dataset is a conntected component if viewed as an undirected graph, which makes sure there are no isolated nodes and each node can always find a path to another node.
- The size of most datasets is controlled between 1000 to 10000 nodes, the largest is no more than 20000 nodes, and the smallest is no less than 500 nodes.
![graph example](../resources/graph_example.pdf)
## Dataset Description
The datasets are available [here](https://drive.google.com/file/d/1Gv0pGj7OIFBkixNpkGoPet-DgjTCL8xa/view?usp=sharing)
### Summary of Network Statistics Notation
- center_id: ID of the center paper of the k-hop graph
- |V|: Number of  nodes
- |E|: Number of edges
- d_avg: Average degree (unweighted)
- d_min: Minimum degree
- k: k of k-hop
- w_abs_avg: average number of words in abstract
- w_boey_avg: average number of words in body text
- w_cnxt_avg: average number of words in citation context

### Dataset 1: node2vec. Community: Graph learning. Center: node2vec.
TODO: ...

### Dataset 2: [GCN-small](https://github.com/dmsquare/CiteExplainer/tree/master/CGCT-GCN-small). Community: Graph learning. Center: GCN.

TODO: Text or table to present the [statistics](https://github.com/dmsquare/CiteExplainer/blob/master/CGCT-GCN-small/ReadMe.txt).
source paper title: T. N. Kipf and M. Welling. Semi-supervised classification with graph convolutional networks.
In ICLR, 2016

| center_id | \|V\| | \|E\| | d_avg | d_min | k | w_abs_avg | w_body_avg | w_cnxt_avg |
|------------|-------|-------|-------|-------|---|-----------|------------|------------|
|            |       |       |       |       |   |           |            |            |






# CGCT Datasets
Main contributors: [Mengxia Yu](myu2@nd.edu), [Wenhao Yu](wyu1@nd.edu), and [Meng Jiang](mjiang2@nd.edu)

## Motivation
Research on the combination of graph and text has been getting much attention. However, existing datasets cannot fully meet the requirements of scientists. Take citation network as an example, the most widely used dataset [CORA](https://relational.fit.cvut.cz/dataset/CORA) contains citation text as edge attributes yet lacks text infomation as node attributes.

In this project, we release 19 theme-related, infomation-rich, and appropriate-sized datasets for research of citation network of scientific papers. All the datsets are generated from [S2ORC](https://github.com/allenai/s2orc). We extract and clean the datasets following the principles below:

- **A citaion network dataset should be related to a specific theme.** For each dataset, we take a typical paper in a specific domain as a center and get its k-hop neighbours.
- **The datasets should contain rich graph and text infomation**  Each dataset is a connected component if viewed as an undirected graph, which means there are no isolated nodes so that every paper in the datasets has graph infomation. What's more worth mentioning is that each node is with full text and each edge is with citation contexts so that rich text infomation of the graph is available.
- **The size of the datsets should be controlled to be suitable for research.** The size of most datasets is between 1000 to 10000 nodes. The largest is no more than 20000 nodes, and the smallest is no less than 500 nodes.
![graph example](./resources/graph_example_1.png)

## Dataset Description
The datasets are available [here](https://drive.google.com/file/d/1Gv0pGj7OIFBkixNpkGoPet-DgjTCL8xa/view?usp=sharing).

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
Center paper title: “node2vec: Scalable feature learning for networks”

| center_id | \|V\| | \|E\| | d_avg | d_min | k | w_abs_avg | w_body_avg | w_cnxt_avg |
|------------|-------|-------|-------|-------|---|-----------|------------|------------|
| 29688     |  862    |  6491 | 7.52  |  3     |  3 |       172    |    5777        |       94     |


### Dataset 2: [GCN-small](https://github.com/dmsquare/CiteExplainer/tree/master/CGCT-GCN-small). Community: Graph learning. Center: GCN.

Center paper title: “Semi-supervised classification with graph convolutional networks”

| center_id | \|V\| | \|E\| | d_avg | d_min | k | w_abs_avg | w_body_avg | w_cnxt_avg |
|------------|-------|-------|-------|-------|---|-----------|------------|------------|
| 3144218  |  862    |  6482  | 7.52  |  2     |  2 |       172    |    5777        |       94     |






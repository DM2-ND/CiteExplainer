# CGCT Datasets
Main contributors: [Mengxia Yu](myu2@nd.edu), [Wenhao Yu](wyu1@nd.edu), and [Meng Jiang](mjiang2@nd.edu) ([DM2 Lab](http://www.meng-jiang.com/lab.html), University of Notre Dame)

## Motivation
Graph learning and text generation are two popular machine learning applications. Recent research shows that texts play an important role in graph data learning. For example, the widely studied citation graph dataset [CORA](https://github.com/tkipf/pygcn/tree/master/data/cora) uses paper abstract as node attribute, which improves the performance of node classification and link prediction. Also, graph structural information can enhance text generation. For example, knowledge graphs have been used to improve question answering (e.g., [KBQA](https://github.com/svakulenk0/KBQA)), dialog system, and summarization. However, very little research has been performed to explore the mutual enhancement between graph learning and text generation, specifically, between predicting links and generating textual attributes of links, due to lack of datasets that have textual description on the links. The texts on linkage can be considered as the explanation to link formation, which sheds insight on novel explanable link prediction approaches -- explaining link prediction with natural language.

We introduce a collection of **19** benchmarks for performing and evaluating text-based link prediction and graph-based text generation. These datasets are generated from [S2ORC](https://github.com/allenai/s2orc) of 81.1M papers which has citation graphs (i.e. rich paper metadata, abstracts, citation links) with a full text corpus. The data components are:
- **nodes:** papers;
- **links:** "PaperA-cites-PaperB" directed edges; there can be multiple edges between a pair of nodes;
- **node attribute:** abstract or full text of the paper node;
- **link attribute:** part of PaperA's text as context of citing PaperB, called "citation contextual text" on the link.

The principles of building the benchmarks are as follows:
- **Related to a central topic.** Each benchmark is expanded from a specific paper of a popular topic, such as [node2vec](https://dl.acm.org/doi/10.1145/2939672.2939754) or [gcn](https://arxiv.org/abs/1609.02907) in graph learning, [transformer](https://arxiv.org/abs/1706.03762) in language model, and [neuralcf](https://arxiv.org/abs/1708.05031) in recommender system.
- **Connectivity and completeness.** The citation graph in each benchmark is a connected component. Any two nodes are connected to each other by paths. In the benchmarks, the attribute of every paper node is text-rich, not only abstract but also full text. Every citation edge has textual attribute, i.e., citation contextual texts.
- **Good size for graph learning and text generation on a single GPU.** The number of nodes in the benchmarks is usually ranged between 1000 to 10000. The largest number is smaller than 20000 and the smallest is bigger than 500.

![graph example](./resources/graph_example_3.png)

## Datasets

### Downloads
The **19** benchmark datasets are available [here](https://drive.google.com/drive/folders/1MPA93HmyHX_unV0vME91-6O4u1PkQf27?usp=sharing).

### Notation of Graph Statistics
- k: Number of hops expanded from the center node
- \|V\|: Number of nodes
- \|E\|: Number of links
- d<sub>avg</sub>: Average degree
- w<sub>abst</sub>: Average number of words in abstract (node attribute)
- w<sub>body</sub>: Average number of words in body text (node attribute)
- w<sub>cite</sub>: Average number of words in citation context (link attribute)

### Experimental Settings of Citation Link Prediction
TODO: Validation methods. Evaluation metrics. Algorithms.

### Experimental Settings of Citation Contextual Text Generaion
TODO: Validation methods. Evaluation metrics. Algorithms.

### Dataset 1: [node2vec](https://drive.google.com/file/d/12zfP1UhFEaVJysCpP8EqmfwJLLTNJ0Y_/view?usp=sharing). Topic: Graph learning.
Center paper: [node2vec: Scalable feature learning for networks](https://dl.acm.org/doi/10.1145/2939672.2939754) (ID: 29688)

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  3 |  6491    | 44477 | 6.85  |       159    |    5452        |       96     |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 2-1: [GCN-small](https://github.com/dmsquare/CiteExplainer/tree/master/CGCT-GCN-small). Topic: Graph learning.

Center paper: [Semi-supervised classification with graph convolutional networks](https://arxiv.org/abs/1609.02907) (ID: 3144218)

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  2 |  862    |  6482  | 7.52  |       172    |    5777        |       94     |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 2-2: [GCN](https://drive.google.com/file/d/1ZQiOn0aUdwB699e6yl5dEr__YXBrxbby/view?usp=sharing)

Center paper: [Semi-supervised classification with graph convolutional networks](https://arxiv.org/abs/1609.02907) (ID: 3144218)

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3 |   16366  | 159353 |  9.74  |     164     |    5120       |     88      |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 3: [node2vec+gcn](https://drive.google.com/file/d/1VNJUUlJhw-ndi5VfuTNNJw2zS4kAVGTf/view?usp=sharing)

Center paper:
[node2vec: Scalable feature learning for networks](https://dl.acm.org/doi/10.1145/2939672.2939754) (ID: 29688)
[Semi-supervised classification with graph convolutional networks](https://arxiv.org/abs/1609.02907) (ID: 3144218)

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3  | 1152  |  8760   | 7.60  |     173      |    5801       |        94   |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 4: [BiLSTM_CRF](https://drive.google.com/file/d/1Gv0pGj7OIFBkixNpkGoPet-DgjTCL8xa/view?usp=sharing)

Center paper: [Neural Architectures for Named Entity Recognition](https://arxiv.org/abs/1603.01360)(ID: 6042994)

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|3  | 4803 |   40737  | 8.48 |      138   |    4559       |    97       |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 5 [CNN_BiLSTM](https://drive.google.com/file/d/1ngVrxAmWyebsGC1jM0_anWV40SuwFVjZ/view?usp=sharing)

Center paper: [End-to-end Sequence Labeling via Bi-directional LSTM-CNNs-CRF](https://arxiv.org/abs/1603.01354)(ID: 10489017)

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3 |   12481  | 96552 | 7.74  | 157  |      4984    |     90      |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 6 [BiLSTM_CRF + CNN_BiLSTM](https://drive.google.com/file/d/1gFC_OWQ0yNTNakBlnujxgs8KAy-qpVqv/view?usp=sharing)

Center paper: 
[Neural Architectures for Named Entity Recognition](https://arxiv.org/abs/1603.01360)(ID: 6042994)
[End-to-end Sequence Labeling via Bi-directional LSTM-CNNs-CRF](https://arxiv.org/abs/1603.01354)(ID: 10489017)

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 2 |  5473   | 48169 |  8.80 |      137     |     4534      |      97     |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 7 [SeqAttention](https://drive.google.com/file/d/1d4cUN8X6zl-eRwpORUFUyZ-qilPmH1Ue/view?usp=sharing)

Center paper: 

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  |     |  |   |           |           |           |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 8 [CopyNet](https://drive.google.com/file/d/1I720Kspz6KkrsOOtrHXabHioaECyBzDZ/view?usp=sharing)

Center paper: TODO

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  |     |  |   |           |           |           |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 9 [SeqAttention+CopyNet](https://drive.google.com/file/d/1zcdnyZrfSqPSN2IPrsVbd2Jo3gRdxZmO/view?usp=sharing)

Center paper: TODO

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  |     |  |   |           |           |           |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 10 [Transformer](https://drive.google.com/file/d/1egSADe4CHG7G-Wp9NYYQqj402Ttzh9h7/view?usp=sharing)

Center paper: TODO

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  |     |  |   |           |           |           |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 11 [CANLM](https://drive.google.com/file/d/1dDwScfp0Lig3aop3EnicDzClJ8fSL4aG/view?usp=sharing)

Center paper: TODO

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  |     |  |   |           |           |           |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 12 [Transformer+CANLM](https://drive.google.com/file/d/182fp8NKaFqznKw4AmitSANvD5NmaHOix/view?usp=sharing)

Center paper: TODO

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  |     |  |   |           |           |           |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 13 [GAN](https://drive.google.com/file/d/1qMCgQoRNjdO3l-UiwaGhpmO34iIhr0xO/view?usp=sharing)

Center paper: TODO

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  |     |  |   |           |           |           |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 14 [VAE](https://drive.google.com/file/d/1hchidClLUVVvgWYRfuiNgzKd84YOBcjM/view?usp=sharing)

Center paper: TODO

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
|  |     |  |   |           |           |           |

Performance on citation link prediction:
TODO: A table.

Performance on citation contextual text generation:
TODO: A table.

### Dataset 15 [GAN+VAE](https://drive.google.com/file/d/1GgGfb8FPNBYHdl5PTfh1p8PV5G_RXORC/view?usp=sharing)

### Dataset 16 [NeuralCF](https://drive.google.com/file/d/1mwyOgh2Fp-owm5HdJTsPBJMqGtoEVS03/view?usp=sharing)

### Dataset 17 [GCMC](https://drive.google.com/file/d/1M26aD2Si_fTVmG__OgdyoqwvBqODqKKl/view?usp=sharing)

### Dataset 18 [NeuralCF+GCMC](https://drive.google.com/file/d/10_cyNo7l39Dkk1auZNOzNwkZz1Ef-AOR/view?usp=sharing)

Contributors: [Mengxia Yu](myu2@nd.edu), [Wenhao Yu](wyu1@nd.edu), and [Meng Jiang](mjiang2@nd.edu) ([DM2 Lab](http://www.meng-jiang.com/lab.html), University of Notre Dame)

## Motivation

Both **graph learning** and **text generation** are important research fields. On one hand, recent work shows that texts play an important role in graph representation learning. For example, on the citation graph dataset [CORA](https://github.com/tkipf/pygcn/tree/master/data/cora), using paper abstract as node attribute improves the performance of node classification and link prediction. On the other hand, graph structural information enhances text generation. For example, knowledge graphs have been used to improve question answering (e.g., [KBQA](https://github.com/svakulenk0/KBQA)), dialog system, and summarization. However, very little research has been performed to explore the mutual enhancement **between** predicting links **and** generating textual attributes of links. The text on linkage can be considered as the **explanation to link formation**, which sheds insight on novel explanable link prediction approaches -- **explaining link formation with natural language**.

We introduce a collection of **19** benchmark datasets for performing and evaluating **text-based link prediction** and **graph-based text generation**. These **citation graph** datasets are generated from [S2ORC](https://github.com/allenai/s2orc). The components of each benchmark dataset include:
- **Nodes:** papers;
- **Links:** "PaperA-cites-PaperB" directed edges -- there can be multiple edges between a pair of nodes when paperA cites paperB in multiple places;
- **Node attribute:** abstract or full text of the paper node -- the **full text** includes **abstract** and **body text**;
- **Link attribute:** PaperA's text that cites PaperB, called **citation context** on the link.

The principles of building the benchmark datasets are as follows:
- **Relatedness to a central topic.** Each benchmark graph is built by expanding from a specific paper of a popular topic, such as [node2vec](https://dl.acm.org/doi/10.1145/2939672.2939754) or [GCN](https://arxiv.org/abs/1609.02907) in graph learning, [Transformer](https://arxiv.org/abs/1706.03762) in language model, and [NeuralCF](https://arxiv.org/abs/1708.05031) in recommender system.
- **Graph connectivity and text richness.** Each benchmark graph must be a connected component. Any two nodes are connected to each other by paths. The attribute of every paper node is text-rich, with not only abstract text but also full text. Every citation edge has textual attribute, i.e., the citation contextual text.
- **Good size for graph learning and text generation on a single GPU.** The number of nodes in each benchmark graph is usually ranged between 1000 to 10000. The largest number must be smaller than 20000 and the smallest must be bigger than 500.

![graph example](./resources/graph_example_3.png)

## The Two Tasks: Validation, Evaluation, and Preliminary Models

### Graph Learning (Link Prediction): Predicting whether A cites B

**Validation setting**: Each data has a training set, a validation set, and a test set. The test set contains 10% of observed citation links as positive examples and the same number of non-existent links as negative examples. The validation set contains 10% of the links from the training set (i.e., 9% of the entire dataset) as positive examples and the same number of non-existent links as negative examples.

**Evaluation methods**: Area Under the Curve (AUC) and Average Precision (AP).

**Preliminary models**: We use two algorithms, [Variational Graph Auto-Encoders (VGAE)](https://arxiv.org/abs/1611.07308) [1] and [Graph Convolutional Networks (GCN)](https://arxiv.org/abs/1609.02907) [2]. Because we are curious about whether text-based raw node features make a positive impact, for each algorithm, we train two models: one uses the text-based features, the other doesn't. So we have **four** models: **VGAE-w/o-text**, **VGAE-with-text**, **GCN-w/o-text**, and **GCN-with-text**. In detail, we use a two-layer GCN. We select 1000 words of the highest TF-IDF as the nodes' raw features. Given a node and a word, the feature value is the frequency of the word in the node's textual attribute (e.g., abstract or full text).

[1] Kipf and Welling. "Variational graph auto-encoders." NeurIPS 2016 Bayesian Deep Learning Workshop.

[2] Kipf and Welling. "Semi-supervised classification with graph convolutional networks." ICML 2017.

### Text Generation (Link Formation Explanation): Generating the context A cites B

**Validation setting**: It uses the same training, validation, and test sets as in the task of Graph Learning.

**Evaluation methods**: BiLingual Evaluation Understudy (BLEU), Recall-Oriented Understudy for Gisting Evaluation (ROUGE), Metric for Evaluation of Translation with Explicit ORdering (METEOR), and Consensus-based Image Description Evaluation (CIDEr). In detail, <span style="color:red">[TODO: BLEU-4?]</span>.

**Preliminary models**: We use six algorithms, [Seq2Seq](https://arxiv.org/abs/1409.3215) [3], [SeqAtten](https://arxiv.org/abs/1409.0473) [4], [PGN](https://arxiv.org/abs/1704.04368) [5], [Transformer](https://arxiv.org/abs/1706.03762) [6], [BART](https://arxiv.org/abs/1910.13461) [7], and [T5](https://arxiv.org/abs/1910.10683) [8]. Because we are curious about whether graph structural information make a positive impact, for each algorithm, we train two models: one uses the full citation graph, the other only uses one citation link and its nodes (i.e., the texts on the pair of nodes). So we have **twelve** models: **Seq2Seq-w/o-graph**, **Seq2Seq-with-graph**, **SeqAtten-w/o-graph**, **SeqAtten-with-graph**, **PGN-w/o-graph**, **PGN-with-graph**, **Transformer-w/o-graph**, **Transformer-with-graph**, **BART-w/o-graph**, **BART-with-graph**, **T5-w/o-graph**, and **T5-with-graph**. In detail, <span style="color:red">[TODO: Hyperparameters?]</span>.

[3] Sutskever, Vinyals, and Le. "Sequence to sequence learning with neural networks." NeurIPS 2014.

[4] Bahdanau, Cho, and Bengio. "Neural machine translation by jointly learning to align and translate." ICLR 2015.

[5] See, Liu, and Manning. "Get to the point: Summarization with pointer-generator networks." ACL 2017.

[6] Vaswani, Shazeer, Parmar, Uszkoreit, Jones, Gomez, Kaiser, and Polosukhin. "Attention is all you need." NeurIPS 2017.

[7] Lewis, Liu, Goyal, Ghazvininejad, Mohamed, Levy, Stoyanov, and Zettlemoyer. "Bart: Denoising sequence-to-sequence pre-training for natural language generation, translation, and comprehension." arXiv 2019.

[8] Raffel, Shazeer, Roberts, Lee, Narang, Matena, Zhou, Li, and Liu. "Exploring the limits of transfer learning with a unified text-to-text transformer." JMLR 2020.

## Nineteen Benchmark Citation Graph Datasets

The **19 citation graphs** are categorized into **six themes** based on their papers' research topics: A) Graph learning (**4 graphs**), B) Named entity recognition (**3 graphs**), C) Text generation (**3 graphs**), D) Language model (**3 graphs**), E) Generative model (**3 graphs**), and F) Deep RecSys (**3 graphs**).

### Symbol Description
- C: Center paper node(s);
- k: Number of hops expanded from the center paper node(s);
- \|V\|: Number of nodes;
- \|E\|: Number of links;
- d<sub>avg</sub>: Average node degree (\|E\|/\|V\|);
- w<sub>abst</sub>: Average number of words in **abstract** (node attribute);
- w<sub>body</sub>: Average number of words in **body text** (node attribute);
- w<sub>cite</sub>: Average number of words in **citation context** (link attribute).

### Theme A: Graph learning (4 datasets: Dataset 1-4)

#### Dataset 1: "CiteExplainer-node2vec"

Center paper node: [node2vec](https://dl.acm.org/doi/10.1145/2939672.2939754) [9] (S2ORC ID: 26988)

[9] Grover and Leskovec. "node2vec: Scalable feature learning for networks." KDD 2016.

[Download data "CiteExplainer-node2vec"](https://drive.google.com/file/d/12zfP1UhFEaVJysCpP8EqmfwJLLTNJ0Y_/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| 3 | 6491 | 44477 | 6.85 | 159 | 5452 | 96 |

- Results on citation link prediction:

| | AUC (valid) | AP (valid) | AUC (test) | AP(test) |
|-|-|-|-|-|
| VGAE-w/o-text | 87.94 | 84.59 | 80.74 | 84.34 |
| VGAE-with-text | 90.93 | 92.42 | 90.96 | 92.54 |
| GCN-w/o-text | 86.01 | 89.46 | 85.83 | 89.27 |
| GCN-with-text | **94.22** | **95.30** | **94.19** | **95.14** |

[Download trained link prediction models "CiteExplainer-node2vec"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-node2vec"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

#### Dataset 2: "CiteExplainer-GCN-small"

Center paper node: [GCN](https://arxiv.org/abs/1609.02907) [2] (S2ORC ID: 3144218)

[Download "CiteExplainer-GCN-small"](https://github.com/dmsquare/CiteExplainer/tree/master/CGCT-GCN-small)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| **2** | 862 | 6482 | 7.52 | 172 | 5777 | 94 |

- Results on citation link prediction:

| | AUC (valid) | AP (valid) | AUC (test) | AP(test) |
|-|-|-|-|-|
| VGAE-w/o-text | 86.16 | 88.77 | 85.17 | 87.36 |
| VGAE-with-text | **92.13** | **93.20** | **92.66** | **93.86** | 
| GCN-w/o-text | 90.52 | 92.43 | 90.91 | 91.40 |
| GCN-with-text | 90.94 | 92.09 | 90.41 | 91.86 |

[Download trained link prediction models "CiteExplainer-GCN-small"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-GCN-small"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

#### Dataset 3: "CiteExplainer-GCN"

Center paper node: [GCN](https://arxiv.org/abs/1609.02907) [2] (S2ORC ID: 3144218)

[Download "CiteExplainer-GCN"](https://drive.google.com/file/d/1ZQiOn0aUdwB699e6yl5dEr__YXBrxbby/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| **3** | 16366 | 159353 | 9.74 | 164 | 5120 | 88 |

- Results on citation link prediction:

| | AUC (valid) | AP (valid) | AUC (test) | AP(test) |
|-|-|-|-|-|
| VGAE-w/o-text | 87.03 | 89.78 | 87.15 | 89.87 |
| VGAE-with-text | 93.47 | 94.81 | 93.47 | 94.83 |
| GCN-w/o-text | 91.19 | 92.61 | 90.99 | 92.55 |
| GCN-with-text | **95.72** | **96.51** | **95.64** | **96.54** |

[Download trained link prediction models "CiteExplainer-GCN"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-GCN"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

#### Dataset 4: "CiteExplainer-node2vec-GCN"

Center paper nodes: [node2vec](https://dl.acm.org/doi/10.1145/2939672.2939754) [9] (S2ORC ID: 26988) and [GCN](https://arxiv.org/abs/1609.02907) [2] (S2ORC ID: 3144218)

[Download "CiteExplainer-node2vec-GCN"](https://drive.google.com/file/d/1VNJUUlJhw-ndi5VfuTNNJw2zS4kAVGTf/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| 3 | 1152 | 8760 | 7.60 | 173 | 5801 | 94 |

- Results on citation link prediction:

| | AUC (valid) | AP (valid) | AUC (test) | AP(test) |
|-|-|-|-|-|
| VGAE-w/o-text | 87.85 | 90.44 | 86.94 | 89.37 |   
| VGAE-with-text | 87.74 | 90.49 | 87.17 | 89.57 |   
| GCN-w/o-text | 89.05 | 91.97 | 88.06 | 90.73 |
| GCN-with-text | **91.03** | **92.68** | **90.44** | **92.32** |

[Download trained link prediction models "CiteExplainer-node2vec-GCN"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-node2vec-GCN"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

### Theme B: Named entity recognition (3 datasets: Dataset 5-7)

#### Dataset 5: "CiteExplainer-BiLSTMCRF"

Center paper node: [BiLSTMCRF](https://arxiv.org/abs/1603.01360) [10] (S2ORC ID: 6042994)

[10] Lample, Ballesteros, Subramanian, Kawakami, and Dyer. "Neural architectures for named entity recognition." NAACL 2016.

[Download data "CiteExplainer-BiLSTMCRF"](https://drive.google.com/file/d/1Gv0pGj7OIFBkixNpkGoPet-DgjTCL8xa/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| 3 | 4803 | 40737 | 8.48 | 138 | 4559 | 97 |

- Results on citation link prediction:

| | AUC (valid) | AP (valid) | AUC (test) | AP(test) |
|-|-|-|-|-|
| VGAE-w/o-text | 77.52 | 81.42 | 77.83 | 81.63 |
| VGAE-with-text | 91.13 | 92.39 | 90.78 | 92.02 |
| GCN-w/o-text | 86.89 | 88.49 | 86.65 | 88.51 |
| GCN-with-text | **92.39** | **93.39** | **92.12** | **93.22** | 
 
[Download trained link prediction models "CiteExplainer-BiLSTMCRF"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-BiLSTMCRF"](#) <span style="color:red">[TODO: Insert a valid link.]</span>


#### Dataset 6: "CiteExplainer-CNNBiLSTM"

Center paper: 
[CNNBiLSTM](https://arxiv.org/abs/1603.01354) [11] (S2ORC ID: 10489017)

[11] Ma, and Hovy. "End-to-end sequence labeling via bi-directional LSTM-CNNs-CRF." ACL 2016.

[Download "CiteExplainer-node2vec-GCN"](https://drive.google.com/file/d/1ngVrxAmWyebsGC1jM0_anWV40SuwFVjZ/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| 3 | 12481 | 96552 | 7.74 | 157 | 4984 | 90 |

- Results on citation link prediction:

| | AUC (valid) | AP (valid) | AUC (test) | AP(test) |
|-|-|-|-|-|
| VGAE-w/o-text | 85.09 | 87.94 | 84.91 | 87.77 |
| VGAE-with-text | 94.52 | 95.55 | 94.60 | 95.54 |
| GCN-w/o-text | 88.44 | 90.66 |88.55 | 90.66 |
| GCN-with-text | **95.47** | **96.31** | **95.38** | **96.21** | 
 
[Download trained link prediction models "CiteExplainer-CNNBiLSTM"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-CNNBiLSTM"](#) <span style="color:red">[TODO: Insert a valid link.]</span>



#### Dataset 7 "CiteExplainer-BiLSTMCRF-CNNBiLSTM".

Center paper: 
[BiLSTMCRF](https://arxiv.org/abs/1603.01360) [10] (S2ORC ID: 6042994) and [CNNBiLSTM](https://arxiv.org/abs/1603.01354) [11] (S2ORC ID: 10489017)

[Download "CiteExplainer-node2vec-GCN"](https://drive.google.com/file/d/1gFC_OWQ0yNTNakBlnujxgs8KAy-qpVqv/view?usp=sharing)

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 2 |  5473   | 48169 |  8.80 |      137     |     4534      |      97     |

- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text | 81.42  |   83.94     |    82.28     |   84.79    |
| VGAE-with-text | 91.68  | 92.73 | 91.87    |   92.95      | 
| GCN-w/o-text |   86.56  |    88.00   |    86.84    | 88.22 |
| GCN-with-text| **92.37** |     **93.45**     |    **92.60**     | **93.60**     | 


[Download trained link prediction models "CiteExplainer-BiLSTMCRF-CNNBiLSTM"](https://drive.google.com/drive/folders/1ZrB0NN09Ukd4uH5jakzpDTBB7UfWhFy2?usp=sharing)

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-BiLSTMCRF-CNNBiLSTM"](#) <span style="color:red">[TODO: Insert a valid link.]</span>



### Theme C: Text generation (3 datasets: Dataset 8-10)

#### Dataset 8: "CiteExplainer-SeqAttention"

Center paper node: [SeqAttention](https://arxiv.org/abs/1603.01360) [4] (S2ORC ID: 11212020)

[Download data "CiteExplainer-BiLSTMCRF"](https://drive.google.com/file/d/1d4cUN8X6zl-eRwpORUFUyZ-qilPmH1Ue/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| 3 | 4803 | 40737 | 8.48 | 138 | 4559 | 97 |

- Results on citation link prediction:

| | AUC (valid) | AP (valid) | AUC (test) | AP(test) |
|-|-|-|-|-|
| VGAE-w/o-text |   80.36   |    84.35   |   80.01    |    84.31     |
| VGAE-with-text |   89.37   |     90.82  |   89.32    |     90.45    |
| GCN-w/o-text |  84.65   |   87.07      |   85.72   |  88.63    |
| GCN-with-text | **91.86** | **92.92** | **91.79** | **92.71** | 
 
[Download trained link prediction models "CiteExplainer-SeqAttention"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-SeqAttention"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

#### Dataset 9: "CiteExplainer-CopyNet"

Center paper node: [CopyNet](https://arxiv.org/abs/1603.06393) [12] (S2ORC ID: 8174613)

[12] Gu, Lu, Li, and Li. "Incorporating copying mechanism in sequence-to-sequence learning." ACL 2016. 

[Download data "CiteExplainer-CopyNet"](https://drive.google.com/file/d/1I720Kspz6KkrsOOtrHXabHioaECyBzDZ/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| 3 |   2651  | 27904 |  10.53 |      140     |      4826     |     98     |

- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text|   82.27   |   83.92  |    81.81   |     83.88     |   
| VGAE-with-text |    89.10  |     90.05    |    89.26   |    90.54      |   
| GCN-w/o-text  |   84.99   |     86.03    |   84.62   |    86.25   |
| GCN-with-text  |   **91.36**   |   **92.38**  |  **91.14**  |   **92.11**    |   

 
[Download trained link prediction models "CiteExplainer-CopyNet"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-CopyNet"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

#### Dataset 10: "CiteExplainer-SeqAttention-CopyNet"

Center paper nodes:  [SeqAttention](https://arxiv.org/abs/1603.01360) [4] (S2ORC ID: 11212020) and [CopyNet](https://arxiv.org/abs/1603.06393) [12] (S2ORC ID: 8174613)

[Download "CiteExplainer-node2vec-GCN"](https://drive.google.com/file/d/1zcdnyZrfSqPSN2IPrsVbd2Jo3gRdxZmO/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|-|-|-|-|-|-|-|
| 3 | 1152 | 8760 | 7.60 | 173 | 5801 | 94 |

- Results on citation link prediction:

| | AUC (valid) | AP (valid) | AUC (test) | AP(test) |
|-|-|-|-|-|
| VGAE-w/o-text |    82.27  |     83.92      |      81.81    |     83.88     |
| VGAE-with-text |   89.10 |  90.52  |   89.26    |     90.55     | 
| GCN-w/o-text |  84.99 |     86.03    |  84.62    |      86.25   |
| GCN-with-text  |    **91.35**   |     **92.38**      |     **91.14**   | **92.11**        | 


[Download trained link prediction models "CiteExplainer-SeqAttention-CopyNet"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-SeqAttention-CopyNet""](#) <span style="color:red">[TODO: Insert a valid link.]</span>


### Theme D: Language model (3 datasets: Dataset 11-13)

#### Dataset 11: "CiteExplainer-Transformer"

Center paper node: [Transformer](http://papers.nips.cc/paper/7181-attention-is-all-you-need) [6] (S2ORC ID: 13756489) 

[Download "CiteExplainer-Transformer"](https://drive.google.com/file/d/1dDwScfp0Lig3aop3EnicDzClJ8fSL4aG/view?usp=sharing)

- Staticstics: 

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3 |  1684   | 8725 |  5.18 |     149      |     4604      |     93     

- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text |   85.40   |    88.80   |    85.67   |    89.08      |   
| VGAE-with-text | 88.59   |    90.64   |    87.46   |    90.46      |   
| GCN-w/o-text   |   90.11   |    92.43     |   89.85   |   92.60    |
| GCN-with-text  |   **90.76**   |  **92.50**   | **91.63**   |   **93.45**    |   

[Download trained link prediction models "CiteExplainer-Transformer"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-Transformer"](#) <span style="color:red">[TODO: Insert a valid link.]</span>


#### Dataset 12: "CiteExplainer-CANLM"

Center paper node: [CANLM](https://arxiv.org/abs/1508.06615) [13] (S2ORC ID: 686481)

[13] Kim, Jernite, Sontag, and Rush. “Character-Aware neural language models”. AAAI 2016.

[Download "CiteExplainer-CANLM"](https://drive.google.com/file/d/1dDwScfp0Lig3aop3EnicDzClJ8fSL4aG/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3 |  6683   | 62812 | 9.40  |    146       |    4798       |     96      |

- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text |   83.04   |    85.79   |    82.95   |      85.55    |   
| VGAE-with-text |   90.43   |     92.03  |    90.88   |      **92.48**    |  
| GCN-w/o-text   |   84.91   |     87.24    |   85.13   |    87.25   |
| GCN-with-text |    **91.85**  |   **93.29**  |  **92.02**  |   93.47    |   
 
[Download trained link prediction models "CiteExplainer-CANLM"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-CANLM"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

#### Dataset 13: "CiteExplainer-Transformer-CANLM"
Center paper: [Transformer](http://papers.nips.cc/paper/7181-attention-is-all-you-need) [6] (ID: 13756489) and [CANLM](https://arxiv.org/abs/1508.06615) [13] (ID: 686481)

[Download "CiteExplainer-Transformer-CANLM"](https://drive.google.com/file/d/182fp8NKaFqznKw4AmitSANvD5NmaHOix/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 2 |   2039  | 11020 | 9.98  |     146      |     4535      |    94       |

- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text |  84.72    |   88.25    |    84.90   |    88.61      |   
| VGAE-with-text |   89.07   |    91.86   |     89.99  |      92.26    |   
| GCN-w/o-text   |   87.98   |     90.85    |  89.36    |  91.77     |
| GCN-with-text |   **90.85**  |   **93.08**  |  **92.13**  |    **93.98**   |   


[Download trained link prediction models "CiteExplainer-Transformer-CANLM"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-Transformer-CANLM"](#) <span style="color:red">[TODO: Insert a valid link.]</span>

### Theme E: Generative model (3 datasets: Dataset 14-16)

#### Dataset 14: "CiteExplainer-GAN":

Center paper node: [GAN](http://papers.nips.cc/paper/5423-generative-adversarial-nets) [14] (S2ORC ID: 12209503)

[14] Goodfellow, Pouget-Abadie, Mirza, Xu, Warde-Farley, Ozair, Courville, and Bengio. "Generative adversarial nets." NIPS 2014.

[Download "CiteExplainer-GAN"](https://drive.google.com/file/d/1qMCgQoRNjdO3l-UiwaGhpmO34iIhr0xO/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3 |   10586  | 102380 | 9.67  |     170    |  5473  |     90   |


- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text|   86.88   |    89.56   |    86.19   |     89.05     |   
| VGAE-with-text |   92.93   |    94.37   |     92.62  |     94.12     |   
| GCN-w/o-text   |   89.71   |    91.59     |   88.94   |   91.05    |
| GCN-with-text |   **94.51**   |   **95.63**  |  **94.55**  |    **95.57**   |   



[Download trained link prediction models “CiteExplainer-GAN”](xx)  <span style="color:red">[TODO: Insert a valid link.]
 
- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-GAN"](#) <span style="color:red">[TODO: Insert a valid link.]</span>



#### Dataset 15: "CiteExplainer-VAE":

Center paper node: [VAE](https://arxiv.org/abs/1312.6114) [15] (S2ORC ID: 15789289)

[15] Kingma and Welling. "Auto-encoding variational bayes." ICLR 2014.

[Download "CiteExplainer-VAE"](https://drive.google.com/file/d/1hchidClLUVVvgWYRfuiNgzKd84YOBcjM/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3 |    2292 | 15267  |       13.38    |       160    |     5741  |  97 |



- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text|   81.43   |   85.75    |    81.80   |     86.24     |   
| VGAE-with-text |   90.02   |    91.65   |   90.41    |      91.85    | 
| GCN-w/o-text|   87.06   |     89.69    |   87.42   |  92.02     |
| GCN-with-text |    **91.22**  |   **92.44**  |  **92.21**  |    **93.21**   |   


[Download trained link prediction models "CiteExplainer-VAE"](xx)  <span style="color:red">[TODO: Insert a valid link.]
 
- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-VAE"](#) <span style="color:red">[TODO: Insert a valid link.]</span>



#### Dataset 16: "CiteExplainer-GAN-VAE":

Center paper node: [GAN](http://papers.nips.cc/paper/5423-generative-adversarial-nets) [14] (S2ORC ID: 12209503) [VAE](https://arxiv.org/abs/1312.6114) [15] (S2ORC ID: 15789289)

[Download "CiteExplainer-GAN-VAE"](https://drive.google.com/file/d/1GgGfb8FPNBYHdl5PTfh1p8PV5G_RXORC/view?usp=sharing)

- Statistics:


| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 2 |   2440  | 16399 | 13.40 |  160    |   5712     |  97        |

- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text|    81.43  |    87.66   |   85.24    |   88.23     |   
| VGAE-with-text| 87.58    |   89.42   |   88.94    |  90.83     |   
| GCN-w/o-text |    89.17  |     90.58    |     90.26 |   91.98    |
| GCN-with-text |   **91.58**   |  **92.61**   |  **93.00**  |    **94.17**   |   



[Download trained link prediction models "CiteExplainer-GAN-VAE"](xx)  <span style="color:red">[TODO: Insert a valid link.]
 
- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-GAN-VAE"](#) <span style="color:red">[TODO: Insert a valid link.]</span>



### Theme F: Deep RecSys (3 datasets: Dataset 17-19)

#### Dataset 17: "CiteExplainer-NeuralCF":

Center paper node: [NeuralCF](https://dl.acm.org/doi/abs/10.1145/3038912.3052569) [15] (S2ORC ID: 13907106)

[15] He, Liao, Zhang, Nie, Hu, and Chua. "Neural collaborative filtering." WWW 2017.

[Download "CiteExplainer-NeuralCF"](https://drive.google.com/file/d/1mwyOgh2Fp-owm5HdJTsPBJMqGtoEVS03/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3 |   17554  | 150737 |  8.59 |    167       |       5123    |       87    |

- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text |   84.57  |  87.53  | 85.26 |    88.04   |   
| VGAE-with-text | 91.26   |  88.71 |   90.81  | 89.82     |  
| GCN-w/o-text   |    90.43   |   92.30    |  90.42   |     92.26      |
| GCN-with-text | **95.48**    |    **96.28**   |    **95.34**   |     **96.27**      |   


[Download trained link prediction models "CiteExplainer-NeuralCF"](xx)  <span style="color:red">[TODO: Insert a valid link.]
 
- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-NeuralCF"](#) <span style="color:red">[TODO: Insert a valid link.]</span>


#### Dataset 18: "CiteExplainer-GCMC":

Center paper node: [GCMC](https://arxiv.org/abs/1706.02263) [16] (S2ORC ID: 36809545)

[16] Berg, Rianne van den, Thomas N. Kipf, and Max Welling. "Graph convolutional matrix completion." KDD 2018.

[Download "CiteExplainer-GCMC"](https://drive.google.com/file/d/1M26aD2Si_fTVmG__OgdyoqwvBqODqKKl/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 3 |  4338   | 31991 | 7.37  |      151     |      4905     |      97  |

- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text |    84.85  |    87.91   |    84.54   |      87.74    |   
| VGAE-with-text |    91.26  |     92.73  |   90.20    |   91.82       | 
| GCN-w/o-text  |   89.59   |    91.34     |    88.68  |   90.79    |
| GCN-with-text |    94.13  |   95.26  |  94.07  |   95.29    |   


[Download trained link prediction models "CiteExplainer-GCMC"](xx)  <span style="color:red">[TODO: Insert a valid link.]
 
- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models "CiteExplainer-GCMC"](#) <span style="color:red">[TODO: Insert a valid link.]</span>


#### Dataset 19: "CiteExplainer-NeuralCF-GCMC":

Center paper nodes: Center paper node: [NeuralCF](https://dl.acm.org/doi/abs/10.1145/3038912.3052569) [15] (S2ORC ID: 13907106) and 
Center paper node: [GCMC](https://arxiv.org/abs/1706.02263) [16] (S2ORC ID: 36809545)

[Download "CiteExplainer-NeuralCF-GCMC"](https://drive.google.com/file/d/10_cyNo7l39Dkk1auZNOzNwkZz1Ef-AOR/view?usp=sharing)

- Statistics:

| k | \|V\| | \|E\| | d<sub>avg</sub> | w<sub>abst</sub> | w<sub>body</sub> | w<sub>cite</sub> |
|---|-------|-------|-------|-----------|------------|------------|
| 2 |   18045  | 157990 | 8.76  |    167       |     5152      |      87     |


- Results on citation link prediction:

|              | AUC (valid) | AP (valid)| AUC (test)| AP(test)|
|--------------|-----|-----------|----------|----------|
| VGAE-w/o-text   |   89.59   |     91.34    |   88.68   |   90.76    |
| VGAE-with-text |   94.50   |  95.32   |  93.91  |   94.92    |   
| GCN-w/o-text |    84.57  |    87.53   |    85.26   |      88.04    |   
| GCN-with-text  |    88.71  |   90.81    |    89.07   |    91.04      |   


[Download trained link prediction models ""CiteExplainer-NeuralCF-GCMC""](xx)  <span style="color:red">[TODO: Insert a valid link.]
 
- Results on citation contextual text generation:

<span style="color:red">[TODO: Insert a table.]</span>

[Download trained text generation models ""CiteExplainer-NeuralCF-GCMC""](#) <span style="color:red">[TODO: Insert a valid link.]</span>





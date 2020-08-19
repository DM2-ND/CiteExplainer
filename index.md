# CGCT Datasets
Main contributors: [Mengxia Yu](myu2@nd.edu), [Wenhao Yu](wyu1@nd.edu), and [Meng Jiang](mjiang2@nd.edu)

## Motivation
Citation networks of scientific papers have been getting much attention. However, existing datasets cannot meet the requirements of scientists. 

In this project, we release 19 theme-related, infomation-rich, and appropriate-sized datasets for research of citation network of scientific papers. All the datsets are generated from [S2ORC](https://github.com/allenai/s2orc). We extract and clean the datasets following the principles below:

- For each dataset, we take a typical paper in a specific domain as a source and get its k-hop neighbours (mostly k = 3). So that the datasets are theme-related. 
- A dataset is a conntected component if viewed as an undirected graph, which makes sure there are no isolated nodes and each node can always find a path to another node.
- The size of most datasets is 1000 to 10000 nodes, the largest is no more than 20000 nodes, and the smallest is no less than 500 nodes.

### Dataset 1: node2vec. Community: Graph learning. Center: node2vec.
TODO: ...

### Dataset 2: [GCN-small](https://github.com/dmsquare/CiteExplainer/tree/master/CGCT-GCN-small). Community: Graph learning. Center: GCN.

TODO: Text or table to present the [statistics](https://github.com/dmsquare/CiteExplainer/blob/master/CGCT-GCN-small/ReadMe.txt).

======

You can use the [editor on GitHub](https://github.com/dmsquare/CiteExplainer/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/dmsquare/CiteExplainer/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

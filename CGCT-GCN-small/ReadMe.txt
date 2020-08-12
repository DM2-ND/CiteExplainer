# Desctription
	This is a citation network dataset collected from S2ORC.
	Center paper id: 3144218
	Center paper title: "Semi-Supervised Classification with Graph Convolutional Networks"
	Source: ICLR'17
	Number of nodes: 862
	Number of nodes that have at least one edge: 862
	Number of edge weights: 14880
	Number of edges (node pairs): 6482
	Avg edge weight (in+out): 17.262180974477957
	Avg degree (in+out): 7.5197215777262185
	Avg #word in abstract (node attr): 172.1450116009281
	Avg #word in body_text (node attr): 5776.6682134570765
	Avg #word in title (node attr): 8.140371229698376
	Avg #word in context (edge attr): 93.63245967741935
	K: 2
	Min deg: 2
	Number of authors: 2577
	Number of journals: 42
	Number of years: 11

# graph.txt
	Each line represents an edge.
	Format:
		citing paper id 	 cited paper id

# node_attr.json
	Each line presents infomation of a node.
	Format:
		{
			node_paper_id: {
			"title": "",
			"journal": "",
			"year": "",
			"authors": [],
			"abstract": "",
			"body_text": []
		}

# edge_attr.txt
	Each line contains the citation context of an edge.
	Format:
		citing_paper_id cited_paper_id  citing_paper_title===CITES===cited_paper_title  citation_span::citation_context


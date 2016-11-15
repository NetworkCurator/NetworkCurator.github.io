---
layout: doc
title: Analyses
---

# Analyses

The primary goal of the NetworkCurator platform is to facilitate building heterogeneous networks (through node and link [ontologies](ontologies.html)) and to help annotate their components (through [custom content pages](content.html)). After network construction, however, a natural next step is analysis. This section outlines a few possibilities.


## Node-centered properties

As explained in the docs on [content pages](content.html), the NetworkCurator platform supports `makealive` components that generate dynamic and interactive content. 





## Graph neighborhoods

The graph page has a 'local neighborhood' feature that displays a sub-network of a neighborhood (nearest neighbors, next-nearest neighbors, etc.) of a set of query nodes. This can form the beginning of an enrichment analysis along the following lines:

- **Generation of a background set.** Display the whole network. Save the node list - this is a background set.
- **Generation of a query set.** Enter a set of query nodes into the search box and display a local neighborhood around these nodes. Save the node list - this is a query set.
- **Enrichment analysis.** Use the query and background sets in an enrichment test. 

This scheme is closely related to procedures already outlines in the literature, for example through [local enrichment analysis](http://bioinformatics.oxfordjournals.org/content/early/2016/10/25/bioinformatics.btw676.abstract). A more sophisticated version of this approach might involve weighting nodes by their distance to the query nodes, for example as in [network-based stratification](http://www.nature.com/nmeth/journal/v10/n11/full/nmeth.2651.html). 


## Third-party software

Although the above approaches provide some ideas, many other analyses are possible with graph structures. Such analyses depend on null hypotheses or assumptions about the underlying graph connectivity and are thus domain-specific. Several types of analyses are also computationally hard. To perform such analyses, data can be  exported from NetworkCurator and then imported into specialized network analysis software. Established packages in this domain include [igraph](http://www.igraph.org/) or [cytoscape](http://www.cytoscape.org/). 



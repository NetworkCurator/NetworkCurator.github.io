---
layout: doc
title: Data export
---

# Data export

At various stages of a project you may want to export data from the NetworkCurator database to use locally or deposit into a data archive such as [Figshare](https://figshare.com/) or [Zenodo](https://zenodo.org/). 

On the navigation tab, select the 'Data' tab. The export section should be at the top. 

![Data export](img/export.jpg)

There are several download options which provide different detail of the data.

<table class="table">
<tr><th>Download type</th><th>Description</th></tr>
<tr><td>Network data</td><td>Current state<sup>1</sup> of the network; includes network summary, ontology, nodes, and links</td></tr>
<tr><td>Complete<sup>2</sup> annotation history</td><td>Complete export of all network database records</td></tr>
</table>

 <sup>1</sup> The current state of the network includes objects with active and inactive status.

 <sup>1</sup> The current state of the network includes objects with active and inactive status.


The output from the data export is a file in json format. The first option provides a file that can be re-[imported](dataimport.html) into a NetworkCurator instance. The second file is meant for archiving or manual processing.

{:.p-warning}
The network data export includes some fields that are not strictly required for data import. 

{:.p-warning}
The NetworkCurator database keeps track of object ownership, and the output files contain fields to convey this information. Note, however, that object ownership is not preserved when a network is re-imported.

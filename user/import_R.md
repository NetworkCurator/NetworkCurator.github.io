## Importing data from R



```r
netdata = list()
## table for general network info
netdata$network = data.frame(name="test_network",
	title="Simple network for testing",
	abstract="Simple network from the networkcurator documentation.",
	stringsAsFactors=F
)
## definition for network node and network link types
netdata$ontology = data.frame(
	name=c("NODE_A", "NODE_Z", "LINK_1", "LINK_2"),
	connector=c(0,0,1,1),
	directional=c(0,0,0,0)
)
## enumeration of all nodes in the network
netdata$nodes = data.frame(
	name = c("aa", "bb", "yy", "zz"),
	title = c("aa title", "bb title", "yy title", "zz title"),
	class = c("NODE_A", "NODE_A", "NODE_Z", "NODE_Z"),
	stringsAsFactors=F
)
## enumeration of all links in the network
netdata$links = data.frame(
	name=c("aa_yy", "aa_zz", "bb_zz"),
	title=c("aa_yy title", "aa_zz title", "bb_zz title"), 
	class=c("LINK_1", "LINK_1", "LINK_2"),
	"source"=c("aa", "aa", "bb"),
	"target"=c("yy", "zz", "zz"),
	stringsAsFactors=F
)
```






##
## script to make lab-demo network

library("jsonlite")
library("shrt")


## define inputs
basedir = "/science/share/TomaszKonopka/Dropbox/Manuscripts/NetworkCuration/examples/"
node.file = p0(basedir, "demo.lab.nodes.csv")
link.file = p0(basedir, "demo.lab.links.csv")
onto.file = p0(basedir, "demo.lab.ontology.csv")


## load data
netdata = list()
netdata$network = data.frame(name="demo-lab",
    title="demo lab example",
    abstract="demo lab abstract",
    stringsAsFactors=F)
netdata$ontology = rtht(onto.file)
netdata$nodes = rtht(node.file)
netdata$links = rtht(link.file)
netdata$ontology = rtht(onto.file)



write(prettify(toJSON(netdata)), file=p0(basedir, "demo.lab.network.json"))





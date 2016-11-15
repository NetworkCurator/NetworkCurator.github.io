---
layout: doc
title: Data input
---

# Network import


Whereas the web interface provides tools for editing individual objects, it is sometimes useful to make several changes at once. These actions can be performed through data imports. 



## Network definitions

A network definition file is a JSON object with the following structure.

```
{
  "network":  [...], 
  "ontology": [...],
  "nodes":    [...],
  "links":    [...]
}
```

The rest of this section describes each of these blocks in turn. It is worth skimming this documentation as the format is quite flexible and not all elements are required. The section ends with a complete working example.
 

### Summary attributes

The first block called `network` is **required**. It identifies the target network and sets its summary attributes.

```
"network": [
  {
    "name":     "net-example",
    "title":    "Import tutorial network",
    "abstract": "Tutorial abstract",
    "content":  "Tutorial text"
  }
]
```

The first attribute `name` is **required** and its value should match the name of the existing network. 

The other attributes are optional. If they are present, they are interpreted as updates for the existing values. (If they are present and match existing values, they are ignored).

**Note:** It is important that the `network` block is a JSON array with one element. That is, it is important that the key/value pairs are enclosed by brackets as well as braces, `[{ ... }]`. Definitions beyond the first position in the array are ignored.


### Ontology definitions

Ontology definitions are optional. They are used to define new ontology classes or update existing definitions. 

```
"ontology": [
  {
    "name":        "NODE_A",
    "connector":   0,
    "directional": 0,
    "parent":      "",
    "status":      1
  },
  {
    "name":        "LINK_X",
    "connector":   1,
    "directional": 1,
    "parent":      "",
    "status":      1
  }
]
```

The JSON array can contain multiple entries. Each entry describes either a node or a link class. 

- `name`, string. Sets the name identifier for the class.
- `connector`, 0/1 value. Determines whether the class is a node or link.
- `directional`, 0/1 value. Determines if a link is two-way or one-way.
- `parent`, string. Identifies the parent class in the hierarchy. Defaults to the empty string (root level in the hierarchy).
- `status`, 0/1 value. Determines if a class is deprecated or active.

The `name` attribute in each entry is **required**. When the named class does not exist in the network, it is created. When the named class already exists, the definitions are used to change its properties. Definitions that match existing values are ignored.

**Note:** Attributes other than `name` are not required. However, they default to the values shown for nodes and links, respectively. Thus, a missing attribute for an existing ontology class can trigger an update. 

**Warning:** Updating ontology classes is tricky, especially when there is a nontrivial hierarchy structure involved. In most cases it is best to use the import features only to define new root-level classes. Adjustments/updates are more easily made through the web interface. 



### Node definitions


```
"nodes": [
  {
    "name":  "n001",
    "title": "test node 001",
    "class": "NODE_A",
    "status": 1
  },
  {
    "name":  "n002",
    "title": "test node 002",
    "class": "NODE_A", 
    "status": 1
  }
]
```

- `name`, string.
- `title`, string.
- `class`, string.
- `status`, 0/1 value.



### Link definitions

```
"links": [
  {
    "name":   "link001",
    "title":  "test link 001",
    "class":  "LINK_X",
    "source": "n001",
    "target": "n002",
    "status": 1
  }
]
```


- `name`, string.
- `title`, string.
- `class`, string.
- `source`, string.
- `target`, string.
- `status`, 0/1 value.



### Example

The elements above can be put altogether to produce a complete network definition. A complete example can be found [here](import_example.md). Just copy/paste the code into a text file, adjust the network name to match a target network, and the test data will be ready for importing.



## Batch voting 



## Final comments

We conclude with some observations on network versioning.

As explained earlier, each project tracked by the network curator contains a complete history of edits and prior states. Furthermore, the curator does not provide features to "delete" content, only to "deprecate" content. This means that data imports can only update or add to the existing state and are guaranteed to preserve existing data. 

The only way to "clean up" a network and completely remove content is as follows:

- export only active elements from the existing network 
- create a new empty network with a new name
- adjust the exported data file to match the new network name
- import the data into the new network





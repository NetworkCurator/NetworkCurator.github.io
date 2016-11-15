---
layout: doc
title: Content
---

# Managing content

Content pages hold descritions and comments associated with graph elements. Each of these content 'objects' - titles, abstracts, descriptions, comments - is created by a site user and can be edited in-browser using markdown and markdown-alive. 

This section explains how to use these two technologies to produce rich, dynamic, and information-rich content pages.


## Markdown

Markdown is a markup language designed to augment plain-text documents with simple styling, for example headers or web-links. The implementation used in NetworkCurator is based on [showdown](https://github.com/showdownjs/showdown) and provides the following features

- paragraph structure
- text styling (bold, italic, strikethrough text)
- links
- headers
- lists
- checklists
- tables
- code blocks

See the showdown [documentation](https://github.com/showdownjs/showdown/wiki/Showdown's-Markdown-syntax) or online tutorials for details on these features.

TO DO - explain sanitizing steps.


## Markdown-alive

While markdown is well-suited for preparing text-based information, some data are better presented in graphical or interactive ways. To provide such capabilities NetworkCurator pages also support [markdown-alive](https://github.com/tkonopka/mdalive.js). 

Suppose we have a dataset linking category names to numeric scores. Whereas in plain markdown we would be constrained to display this data in a table, we can instead prepare a bar chart using markdown-alive. To do this, we begin by preparing the data into a json object, for example

```
{
  "title": "My first chart",
  "ylab":  "Score (unit)",
  "xlab":  "",
  "data":  [{"name": "a", "value": 4, "fill": "#0000dd"},
            {"name": "b", "value": 6, "fill": "#3399cc"}, 
            {"name": "c", "value": 7, "fill": "#dd3300"}]
}
```

Such an object is a useful resource in itself as it contains raw data as well as semantic descriptors in clearly defined fields. To turn it into a bar plot, we enter this information into a markdown code block.

<pre><code>
```mdalive barplot001
{
  "title": "My first chart",
  "ylab":  "Score (unit)",
  "xlab":  "",
  "data":  [{"name": "a", "value": 4, "fill": "#0000dd"},
            {"name": "b", "value": 6, "fill": "#3399cc"}, 
            {"name": "c", "value": 7, "fill": "#dd3300"}]
}
```
</code></pre>

Note how the json object is now enclosed by three backticks (\`\`\`). In plain markdown this would be interpreted as an instruction to display the json data directly on the page. In this case, however, the code block is decorated with labels `mdalive` and `barplot001`. The first label, `mdalive` is an instruction to interpret the pass the json data to a javascript function. The second label, here `barplot001`, specifies the target function. 

In this case the mdalive conversion results in a complete bar chart with some interactive components. 

TO DO - image.

### Visualization library

NetworkCurator provides a library of mdalive functions that generate a variety of data visualizations:

- barplot001 (as in the example above)
- scatterplot001

Each of these visualization functions requires json-prepared data in a specific format. See the documentation for each function for details.  

Local installations of the NetworkCurator can achieve different visualization capabilities, see the documentation on interface themes for details.



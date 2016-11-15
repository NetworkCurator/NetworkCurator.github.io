---
layout: doc
title: Ontologies
---

# Ontologies

The graph ontology page defines the types of the nodes and links that can be represented in a given network. The page also provides tools to adjust the visual appearance of these objects when displayed on the graph page.

This chapter is composed of two parts:

- [Ontology class structure](#browsing) one-line description
- [Managing an ontology](#managing) one-line description
- [Styling ontology classes](#styling) one-line description


<a name="browsing"></a>
## Ontology class structure

- [ ] To do, describe how to interpret the ontology trees (as a normal user)



<a name="managing"></a>
## Managing ontologies 

- [ ] To do: describe how to manipulate the ontology structure as a curator


### Adding new ontology classes

### Ajusting ontology classes

Moving. Hierarchies. 

Mention adjusting class names. (Avoid it, but if necessary, see section on adjusting styling as well)

### Activating and inactivating classes




<a name="styling"></a>
## Styling ontology classes

**Curators**

The ontology page allows curators determine how objects are displayed on a graph. This is a powerful feature as visual styling can provides users immediate cues as to how to interpret various nodes and links.

Styling of ontology classes is achieved through a combination of scalable vector graphics (SVG) and cascading style sheets (CSS). Defining these styles can be fiddly. However, styles usually do not require frequent adjustments and the examples below provide code snippets that are ready for cut-and-paste.


### Background

Networks in the NetworkCurator are rendered using scalable vector graphics objects (SVG). Each svg object is set up with a leading set of `defs` followed by data. Styling of nodes and links is achieved by placing custom definitions in the `defs` component.

To adjust style definitions on the ontology page, click on the `Edit` button next to a class name. This should display a form where you can change the class name in a text box and adjust styling in a larger text area. The preview on the left should provide immediate feedback as to how a style definition is actually rendered.



### Styling nodes

Nodes are positioned in the network with `use` tags that refer to shapes. In the styling text area for each node we thus have to input a definition for a shape. 

Let's assume that our node class is callled `NODE_X`. A minimal declaration for a circular shape is 

```
<circle id="NODE_X" cx=0 cy=0 r=10></circle>
```

A similar declaration for a rectangular node with round corners is 

```
<rect id="NODE_X" x=-9 y=-9 width=18 height=18 rx=3 ry=3></rect>
```

There are a few points to take note of.

- The shape definition **must contain an `id` tag that matches the ontology class name**. This tag is required because network elements use the id to determine their shape. If the id is miss-specified, node elements will not display.

  Unfortunately, the `id` tag must be set and updated manually. If you update the name of the class, you will have to manually adjust the `id` tag to match. 

- The shape should be **centered around the origin, `(0, 0)`**. For circular shapes, this is easy to achieve by setting `cx=0 cy=0`. For rectangles, it is necessary to manually adjust the position of the top-left corner and the height/width properties. If the shape center is miss-specified, node elements can become invisible in the preview and appear offset on the network page. 

- It is also possible to define more complex shapes using `path` elements.

<br/>
Thus far, both the circle and the rectangle appear in the default style and color. The recommended approach is to define custom CSS rules to match each class. 

A complete definition for a circular node with a slight border might be

```
<style type="text/css">
use.NODE_X {
  fill: #daa;
  stroke: #d22;
  stroke-width: 1;
}
</style>
<circle id="NODE_X" cx=0 cy=0 r=10></circle>
```

For a rectangular shape, we would instead enter

```
<style type="text/css">
use.Pathway {
  fill: #eee;
  stroke: #00d;
  stroke-width: 2;
}
</style>
<rect id="Pathway" x=-9 y=-9 width=18 height=18></rect>
```

Again, there are a few points to highlight.

- The CSS definitions must be within a `use` block decorated by a dot and the ontology class name (here `NODE_X`).

- The CSS block must be enclosed in a `<style>` tag.

- The class name must match the `id` as well as `use` elements. 


<small>Another way of styling involves writing rules directly inside the shape definitions. This works in principle, but causes problems during selections. Therefore, please use the approach using style tags as described above.</small>

<br/>
### Styling links

Links are always rendered using `line` elements. Thus to style a link we do not need to specify a shape, only the css style. 

Let's assume a link class is called `LINK_Y`. A style definition might be

```
<style type="text/css">
line.LINK_Y {
  stroke: #09d;
  stroke-width: 5;
}
</style>
```

Another example with a dashed line

```
<style type="text/css">
line.LINK_Y {
  stroke: #d9d;
  stroke-width: 5;
  stroke-dasharray: 5 4;
}
</style>
```


- The CSS definitions must be **within a `line` bock** decorated by a dot and the name of the ontology class**. The block should be enclosed in a `<style>` tag.

- The ontology **class name must be specified after `line`**. As for nodes, this name must be updated manually.


<br/>
Thus far, the links are rendered as plain lines. However, in some cases it useful to encode directional relationships. For this purpose we can use line markers (e.g. arrowheads). To achieve this the line style should include two things: a definition for a marker, and a CSS instruction for how to apply the marker to the line. 

An example with a simple arrowhead is

```
<marker id="mLINK_Y" 
        markerWidth="4" markerHeight="4" 
        refX="8" orient="auto" refY="2">
    <path d="M0,0 L4,2 0,4" stroke="#d9d" fill="none"></path>
</marker>
<style type="text/css">
line.LINK_Y {
  stroke: #d9d;
  stroke-width: 4;
  marker-end: url(#mLINK_Y)
}
</style>
```

Again, a few points to note

- The marker object **must have an `id` tag**. This `id` must be referenced from the CSS block. The `id` must be a unique identifier but can otherwise be chosen freely. A simple way to chose an id is to use the ontology class name with a prefix or postfix.

- Markers in CSS are styled separately from lines. Color matching between marker and line must be applied manually. 

- The **position of the marker** along the line might appear strange in the preview diagram. In particular, the marker might appear near the middle of the line and not at the end. This is because the marker is offset slightly from the terminus. This is a trick so that the arrowhead is not hidden by a large node on the graph page. 



That's it, more or less. Maybe needs some editing.




### Examples

<style type="text/css">
use.STIMULUS {
  fill: #8a8;
  stroke: #242;
  stroke-width: 1;
}
</style>
<g id="STIMULUS" transform="rotate(-30)">
<rect x="-16" y="-8" width="32" height="16" rx=8></rect>
<rect x="-10" y="-5" width="10" height="10" fill="#ffffff" stroke-width=0></rect>
<circle cx=-8 cy=0 r=5 fill="#fff" stroke-width=0 ></circle>
</g>




<style type="text/css">
use.CELL {
  fill: #eee;
  stroke: #222;
  stroke-width: 1.5;
}
</style>
<g id="CELL" transform="translate(-18,-18)scale(1.2)">
    <path d="m 30.215521,24.283492 c -2.87712,5.01705 -8.564919,8.18014 -14.298109,8.35704 -3.38356,-0.10338 -6.7045503,-1.57121 -9.1959803,-3.83069 -2.38147,-2.45266 -4.2370304,-5.43965 -5.4487704,-8.62961 -0.85646002,-2.92501 -0.73355002,-6.06951 -0.18194,-9.0369 0.80104,-2.7994201 2.62221,-5.1660201 4.4070004,-7.4110697 1.59682,-1.83048 3.96391,-2.98401002 6.4167903,-2.85764002 3.36197,-0.0232 6.88335,-0.23323 10.03578,1.15361002 3.110239,1.3451 5.967609,3.4651796 7.917359,6.2559696 1.5752,2.3371301 1.94325,5.2249001 1.74046,7.9784501 -0.0208,2.71371 -0.0206,5.58623 -1.39259,8.02084 z"></path>
    <circle cx="19" cy="18" r="8.5" fill="#777" stroke-width="0.5"></circle>
  </g>


<style type="text/css">
use.Pathway {
  fill: #f4f408;
  stroke: #222;
  stroke-width: 1.2;
}
</style>
<g id="Pathway" transform=translate(-10,-18)>
    <path d="m 11.992,0.989 c -6.208,0 -11.244,4.601 -11.244,10.273 0,1.660 0.452,3.226 1.218,4.614 0.215,0.389 0.444,0.776 0.710,1.136 l 5.178,8.53 0.304,0 7.640,0 0.329,0 5.178,-8.534 c 0.103,-0.139 0.183,-0.296 0.279,-0.440 l 0.279,-0.417 c 0.054,-0.091 0.100,-0.184 0.152,-0.278 0.765,-1.387 1.218,-2.954 1.218,-4.614 0,-5.672 -5.036,-10.273 -11.244,-10.273 z"  />
    <g>
      <path d="m 8.0361,27.893 8.1355,0" stroke-width=1.4/>
      <path d="m 8.0361,30.036 8.1355,0" stroke-width=1.4/>
      <path d="m 8.0361,32.180 8.1355,0" stroke-width=1.4/>
      <path d="m 9.2386,34.324 5.7304,0" stroke-width=1.4/>
    </g>
  </g>




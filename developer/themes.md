---
layout: doc
title: User Interface
---

# User Interface

The NetworkCurator app can function as a stand-alone website or can form a component of a larger service. In both cases, it may be desirable to adjust the look-and-feel of the user interface for a local installation instance. The project is thus organized to enable customization of the user-interface. 

This section describes the integration of the core and user interface components and outlines the possibilities to adjust the look-and-feel.



## Background

The application is split into two repositories, which roughly correspond to the [core code base](https://github.com/NetworkCurator/NetworkCurator) and the [user interface](https://github.com/NetworkCurator/NetworkCurator-ui). This separation enables a local installation to replace or customize the default look-and-feel and still receive updates and bug fixes to the core code base.

The separation between core and user-interface is only rough. The core repository actually carries several components that determine the visual appearance of the application. These components are

 - third party dependencies, including [bootstrap](http://getbootstrap.com/)
 - cascading style sheets that build upon bootstrap css
 - javascript functions, including custom functions that create html widgets 

These components are included in the core repository in order to maximize consistency with the application javascript code. 

The core repository also contains an `index.php` file at the repository root directory. This script is the gateway to the application and is run when a user first encounters the web application. Internally, the script parses URL options and performs some simple processing, but defers page generation to other scripts in a directory called `nc-ui`. For example, a url `?page=about` triggers a script `nc-ui/nc-ui-about.php`. 

Importantly, the directory `nc-ui` itself is not part of the core repository. It must be created separately during [installation](../user/install.html) and populated with the relevant content. 



## Default user interface

The [default user interface](https://github.com/NetworkCurator/NetworkCurator-ui) contains a set of files that can be cloned into the `nc-ui` directory. The repository aims to provide a complete, working, set of scripts that is compatible with the core.

Several of the files in the user interface repo are required. These required files are named with a prefix `nc`. For example, the about page mentioned earlier is named `nc-ui-about.php`. You can think of these as 'public' in the object oriented programming (OOP) mindset.

Other files in the user interface repo are present for convenience. These files are named without the `nc` prefix. For example, the repo contains a directory `ui-components`. This contains a number of scripts that are used within the user interface repo, but are not referred to is not referred to from the `index.php` file in the core repo. You can think of these scripts as 'private' in a OOP mindset.

The scripts within the user-interface repo build pages using php. These pages interact with the core repo through objects with `nc` prefixes. For example, the header in `nc-ui-header.php` defines a number of javascript objects such as `nc.userid` and `nc.network`. The variables are used throughout the javascript during communication between the browser and the server. As another example, the script that generates the graph view page defines an html component `<svg id="nc-graph-svg"></svg>` that triggers display of the interactive network graph.

Some scripts also create html objects with `nc` as a prefix for class names. In particular, the class `nc-curator` distinguishes content that is aimed at curators; when a page is viewed by a non-curator user, the content becomes invisible. 



## Designing a custom interface

The default user interface is intended as a template. You can clone or fork the repo from github, then and edit it to suit your needs. 

In general, components labeled with a 'nc' prefix are required. This is particularly important for components where the prefix appears in an `id`. Therefore, modify these components with care (javascript functions may refer to these objects and certain function may break if they are not present).

A powerful approach to customize the user interface might be to modify cascading style sheets in the `nc-ui/css/nc-ui.css` file. Changing fonts, text sizes, and colors can make a strong impression.






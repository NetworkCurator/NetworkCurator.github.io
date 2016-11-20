---
layout: doc
title: Server code
---

# Server code file structure

The main code is located in github repository [NetworkCurator](https://github.com/NetworkCurator/NetworkCurator). This section outlines the structure of the root directory.


## Directories

<table class="table">
<tr><th>Directory</th><th>Description</th></tr>
<tr><td><code>nc-api</code></td>
    <td>Implements an [application programming interface](api.html) that provides access to the MySQL database.</td>
</tr>
<tr><td><code>nc-admin</code></td>
    <td>Holds files and scripts relevant for server-side administration. Scripts in this folder is required for installation. Post installation, it holds some site configuration definitions that are used throughout the server-side code base.</td>
</tr>
<tr><td><code>nc-data</code></td>
    <td>Holds user-generated files from a local site. The directory is divided into subdirectories for `networks` and `users`. The first stores network-specific data files such as uploaded json network definitions. The latter stores user-specific data such as identicon images.</td>
</tr>
<tr><td><code>nc-core</code></td>
    <td>Holds code for the core web application, including cascading style sheets, javascript functions, helper php scripts, and [dependencies](dependencies.html). </td>
</tr>
<tr><td><code>nc-ui</code><sup>1</sup></td>
    <td>Holds files implementing a [user interface theme](themes.html).</td>
</tr>
</table>

<sup>1</sup> The 'nc-ui' is not present in the core repository. It must be created manually, for example by cloning the [default interface](https://github.com/NetworkCurator/NetworkCurator-ui). 



## Files

<table class="table">
<tr><th>Directory</th><th>Description</th></tr>
<tr><td><code>.gitignore</code></td>
    <td>Standard git configuration file that determines files tracked in version control. In the NetworkCurator, this file is set up to that repository clones can manage private files (e.g. urls and passwords for a local installation) while maintaing an unbroken connection with the parent repo.</td>
</tr>
<tr><td><code>index.php</code></td>
    <td>Landing page for the web site. This file performs basic processing of a url request and builds the page structure, but refers to scripts in the 'nc-ui' folder to actually generate content.</td>
</tr>
<tr><td><code>pull-update</code></td>
    <td></td>
</tr>
<tr><td><code>README.md</code></td>
    <td>This is the intro page for the github repo. It does not affect funcioning of the web application.</td>
</tr>
<tr><td><code>LICENSE</code></td>
    <td>The code is licensed under the MIT License.</td>
</tr>
</table>




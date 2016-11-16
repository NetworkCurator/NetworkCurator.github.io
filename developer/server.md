---
layout: doc
title: Server code
---

# Server code file structure

The main code is located in github repository [NetworkCurator](https://github.com/NetworkCurator/NetworkCurator).
This section outlines the directories and important files in the root directory of 
that repository. 

{:.p-note}
**Note:** [Another repository](https://github.com/NetworkCurator/NetworkCurator-ui) 
contains code for the user interface. That code is explained [here](themes.html).




## Directories

#### nc-admin

TO DO

#### nc-api

The [API page](api.html) explains the organization in more detail.

#### nc-core

TO DO

#### nc-data

This directory is meant to hold user-generated files from a local site. The directory is divided into subdirectories for `networks` and `users`. 

The `networks` directory is a location for network-specific data files (for example json files used during data imports). 

The `users` directory is a location for user-specific files (for example, identicon images).

#### nc-ui

The `nc-ui` directory is not part of the main repo. The directory is rather created during the [installation](../user/install.html) of a user interface. 



## Files

Severl files in the root directory are standard items in a github repo (e.g. `README.md` and `LICENSE`). 


#### gitignore

The file `.gitignore` is a standard git configuration file. It determines the files that are tracked in version control. 

This files is important for NetworkCurator because it provides a means for clones of the repository to manage private files (for example, with passwords) and maintain unbroken connections with the parent repo. 

In particular, this file contains the lines

```
nc-admin/*/*local*
```

This means that files containing the string `local` will never be saved into the git archive. On a local installation, these files can store site-specific settings such as the site url or adminstrator passwords.


#### index.php

TO DO

#### pull-update

TO DO




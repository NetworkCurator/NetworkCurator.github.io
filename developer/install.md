---
layout: doc
title: Installation
---


The folder `nc-admin` holds pre-installation settings, install scripts, and post-installation settings. 

## Pre-installation configuration

The `install` folder should contain two files. 

`install-settings.php` holds a set of php definitions and default values that are used during installation. Although it holds 'settings' and describes all the features that can be tuned on a local installation, this file itself should never be edited by end-users.

Tuning a local installation should instead be done in a another file called `install-settings-local.php`. See the installation tutorial for examples.

`install.php` is an installation script. It is meant to be run on the command line. It creates connections to a database, then creates the appropriate tables and indexes.

## Installation



## Post-installation settings

The `nc-admin` folder also holds a sub-folder called `config`. This sub-folder holds files that are accessed by php scripts. The `nc-constants.php` should never be edited by end-users, especially not after installation. A file `nc-config-local.php` is generated during installation and holds site-specific settings.




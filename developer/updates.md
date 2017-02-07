---
layout: doc
title: Administration and Updates
---

# Administration and Updates

This document instead outlines the organization of the `nc-admin` directory and explains how to fine-tune a NetworkCurator website pre- and post- installation.

{:.p-note}
A basic installation procedure is outlined in the [user's installation guide](../user/install.html). 



## File structure

The `nc-admin` directory has the following sub-structure. 

<table class="table">
<tr><th>Directory</th><th>Description</th></tr>
<tr><td><code>config</code></td>
    <td>Contains settings associated with the NetworkCurator instance. Files in this directory are read by various server-side scripts; they should not be edited manually.</td>
</tr>
<tr><td><code>install</code></td>
    <td>Holds files and scripts relevant for installation and configuration tuning.</td>
</tr>
<tr><td><code>tests</code></td>
    <td>Holds scripts for testing/debugging. </td>
</tr>
<tr><td><code>tools</code></td>
    <td>Holds miscellaneous scripts that can help an administrator manage the database from the command line. </td>
</tr>
</table>



## Site configuration

All the configuration options are declared and documented in file `nc-admin/install/install-settings.php`. This file is tracked in version control and should not be changed in a local copy. 

To change any of the settings to suit a local instance of the NetworkCurator, define a file `nc-admin/install/install-settings-local.php` with the desired values. Definitions in this 'local' file override the defaults.

After installation, all settings are written automatically into a file `nc-admin/config/nc-config-local.php`. This file is not tracked in version control, so does not appear in the github repo. It only appears after running the install script and is read by run-time php scripts. 

After installation, you can update any of the settings as follows. Edit the `nc-admin/install/install-settings-local.php` file that holds the local settings. Then, execute a configuration update by running 

```
php configure.php
```

This command should re-create the `nc-admin/config/nc-config-local.php` file and thus implement the new settings.


{:.p-warning}
The `install` directory also contains another script called `install.php`. Do **not** execute this script unless you want to destroy the database and recreate it from scratch.




## Updates

The root directory of the NetworkCurator repository contains a script `pull-updates`. The script assumes that the core software and the user interface have been installed by cloning from a git repo. The script attempts to pull new versions of the software, thereby providing a software update. It also builds single javascript and css files from smaller components in the development repo.



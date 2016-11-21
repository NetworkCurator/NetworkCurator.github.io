---
layout: doc
title: Installation and Updates
---

# Installation and Updates

A basic installation procedure is outlined in the [user's installation guide](../user/install.html). This document instead focuses on some fine-tuning that can be achieved through the installation configuration file.


## Configuration

All the configuration options are declared and documented in file `nc-admin/install/install-settings.php`. This file is tracked in version control and should not be changed in a local copy.

To change any of the settings before installation, define a file `nc-admin/install/install-settings-local.php` with the desired values. Definitions in the local file will override the defaults.

After installation, settings are written out into a file `nc-admin/config/nc-config-local.php`. This file is not tracked in version control, so does not appear in the github repo. It only appears after running the install script and is read by run-time php scripts. To change any settings after installation, edit this file. 

{:.p-note}
**Note:** Changing the settings after installation is not likely to destroy the database, but can cause problems nonetheless. So, be careful!


## Updates

The root directory of the repository contains a script `pull-updates`. The script assumes that the core software and the user interface have been installed by cloning from a git repo. The script thus attempts to pull new versions of the software. It also builds single javascript and css files from smaller components in the development repo.

{:.p-note}
Javascript code in the core repo is split up into multiple files, but the default user-interface only loads a single javascript dependency. The update procedure thus creates this single file. In principle, the single file could be minified for download performance. However, to avoid a dependency on minifying software, the update script only concatenates the individual files together without minification.






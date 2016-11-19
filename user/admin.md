---
layout: doc
title: Administration
---

# Site Administration

After installation, the site is empty: there are no networks. However, the installation script creates one user with user name `admin`, the administrator user. 

The role of the administrator is to monitor user accounts and networks. To perform these tasks, navigate to the administrator account page by clicking on the username in the top-right corner of a page.

![Admin user account](img/admin.jpg)

On the admin account page, a section at the bottom displays site management options.

![Admin user account](img/admincreate.jpg)


## User accounts

To create a user account, fill in the registration form with a user's details and password. After submitting the form, you should see a confirmation message. 

After registration, users can change their password at any time through their own [account page](accounts.html). 


## Networks

There are two mechanisms to create a new network. 

 - The simplest way is 'From scratch'. This procedure creates a blank network without any ontology or graph structure. Just enter a network name, network title, and brief description in the form and submit the form. 

 - The second procedure is 'From file'. Use this approach to create a new network and at once define several network details. Just select the file containing the network definition and submit the form. 

In both approaches, the new network becomes immediately active and should appear on the administrator's front page upon refresh. The new network, however, is not be visible or accessible to any of the other registered user or site visitors. To change the visibility, you must edit the network [permissions](permissions.html).

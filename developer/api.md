---
layout: doc
title: API
---


# NetworkCurator API

Transactions with a MySQL database are managed through an application programming interface (API) whose code is in the `nc-api` folder. This sections outlines the organization of the API and the main components of `nc-api` folder.



## API gateway  

The file `nc-api.php` is the main gateway to the NetworkCurator API. This script
receives request, decrypts it, determines how to forward the request to the individual controllers (see below), collects and sends back the output. 

**Note:** The script is set up to decrypt requests using a fixed key that is generated during installation. This means that the API only accepts requests from a single source. That source is the `networkcurator.php` file (the script that processes AJAX calls from a user's browser). 

The API expects to receive a request with at least the following fields 

- **user_id** - the id of the requesting user
- **controller** - determines the genre of request (see below)
- **action** - the API function within the controller's scope to execute (see below)

Other fields may be required for various combinations of controller and action. 

The output of this script should be an object with a field `success` and one of `data` or `errormsg`. 


## Controllers

The directory `controllers` contains php classes that support parts of the API. They are:

- **NCAnnotations** - updates of annotations such as titles, abstracts, 
content pages, or comments
- **NCData** - data imports and data exports
- **NCGraphs** - queries and updates on graph structures
- **NCNetworks** - updates involving networks
- **NCOntology** - updates of node and link type ontologies
- **NCUsers** - updates of user accounts

The public functions within these classes define the `action` fields required by the `nc-api.php`. See the in-code documentation regarding all the available actions and their required input fields.



## Helpers

Directory `helpers` contains miscellaneous classes and functions that are used within the controllers. They are set separately in the `helpers` directory so that the `nc-api.php` script does not confuse them with controllers/actions that can be called by the users. 

## Tests

The `tests` directory contains some test scripts that can be run on the command line. These tests make changes to the local database - drop tables, create new users and network objects - so should not be run on a production system.




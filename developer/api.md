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

The API expects to receive a request with several fields 

<table>
<tr><th>Field</th><th>Description</th></tr>
<tr><td>user_id</td><td> the id of the requesting user</td></tr>
<tr><td>controller</td><td> the controller handling the request (see below)</td></tr>
<tr><td>action</td><td> API function within the controller's scope (see below)</td></tr>
<tr><td></td><td>[Other fields may be required for each combination of controller and action]</td></tr>
</table>

The output of this script should be an object with a field `success` and one of `data` or `errormsg`. 


## Controllers

The directory `controllers` contains php classes that support parts of the API. 

<table>
<tr><th>Controller</th><th>Description</th></tr>
<tr><td>NCAnnotations</td><td>management of annotations such as title, abstracts, comments, etc.</td></tr>
<tr><td>NCData</td><td>data imports and exports</td></tr>
<tr><td>NCGraphs</td><td>queries and updates on graph structures</td></tr>
<tr><td>NCNetworks</td><td>management of networks (e.g. creating networks)</td></tr>
<tr><td>NCOntology</td><td>management of node and link type ontologies</td></tr>
<tr><td>NCUsers</td><td>management of user accounts</td></tr>
</table>

Public functions within these classes define the `action` fields required by the API. See the in-code documentation regarding all the available actions and their required input fields.



## Helpers

Directory `helpers` contains miscellaneous classes and functions that are used within the controllers. They are set separately in the `helpers` directory so that the `nc-api.php` script does not confuse them with controllers/actions that can be called by the users. 

## Tests

The `tests` directory contains some test scripts that can be run on the command line. These tests make changes to the local database - drop tables, create new users and network objects - so should not be run on a production system.




---
layout: doc
title: Database
---

# Database

The MySQL database is organized into tables that start with a prefix (default is 'nc_') and a name for its function

<table class="table">
  <tr><th>Table<sup>1</sup></th><th>Description</th></tr>
  <tr>	<td><code>nc_activity</code></td>
	<td>Tracks change events in networks performed by registered users. Contains entries for the log page (networks navigation bar)</td></tr>
  <tr>	<td><code>nc_anno_text</code></td>
	<td>Holds text-based annotations for networks, nodes, links, ontology classes, and associated comments. Annotation versions are preserved as dated rows with a status field.</td></tr>
  <tr>	<td><code>nc_classes</code></td>
	<td>Holds all ontology classes and their hierarchy. </td></tr>
  <tr>	<td><code>nc_datafiles</code></td>
	<td>Holds metadata for any files uploaded by a user. </td></tr>
  <tr>	<td><code>nc_links</code></td>
	<td>Holds all defined links and their associated ontology classes. Active/inactive links are determined by a status field. Note that annotations such as link name are stored in the 'nc_anno_text' table.</td></tr>
  <tr>	<td><code>nc_log</code></td>
	<td>Tracks a minimal level of site activity: creation/deletion of networks/users, and login events by registered users. </td></tr>
  <tr>	<td><code>nc_networks</code></td>
	<td>Holds ids for networks</td></tr>
  <tr>	<td><code>nc_nodes</code></td>
	<td>Holds all defined nodes and their associated ontology classes. Active/inactive nodes are determined by a status field. Note that annotations such as node name are stored in the 'nc_anno_text' table.</td></tr>
  <tr>	<td><code>nc_permissions</code></td>
	<td>Holds the current permission associations between users and networks.</td></tr>
  <tr>	<td><code>nc_users</code></td>
	<td>Holds the current personal details for registered users. Login events by users requires matching the 'user_pwd' field. Session users confirm loging through another field 'user_extpwd'. </td></tr>
</table>

<sup>1</sup> Each table is indexed on one or more columns. 

It is noteworthy that in addition to identifiers set by user (e.g. network name, node name, link name), the database creates internal ids for all network elements. These consist of one letter prefix (e.g. 'W' for networks and 'N' for nodes) followed by a few random characters. Matching across tables is often performed using these internal identifiers.



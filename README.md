# PHP 8.4 Fixes fo Evo 1.437


### ManagerManager plugin
Fixed “Undefined array key” in
assets/plugins/managermanager/widgets/tags/tags.php
(mm_widget_tags 1.1.4: the tag counter key is now initialized before it’s incremented, and empty tags are skipped.)
### DocManager module
Fixed fatal error “Call to undefined function each()” and a bug in processRange() in
assets/modules/docmanager/classes/dm_backend.class.php
(Line 99: while (list() = each()) replaced with foreach. processRange() rewritten:
	• A range now returns every id in it, not the first id repeated (3-5 gave 3,3,3).
	• A single id after a range is no longer offset (1-5,10 updated document 15 instead of 10).
	• ** no longer reprocesses the ids from earlier values.
	• Ids are cast to integers and duplicates removed.
This affected batch TV editing and document groups. Both problems are also in the official 1.4.37 package.)
### Backup Manager
Fixed “Undefined variable $limit” in
manager/actions/bkmanager.static.php
($limit = 0; is now set before the loop that deletes old snapshots.)
### QuickManager+ plugin
Fixed “Creation of dynamic property” deprecations (PHP 8.2+) in
assets/plugins/qm/qm.inc.php
(1.5.13: all class properties are now declared. Also fixed a fatal error with ?logout and tightened the checks on frontend TV editing.)
### DocInfo snippet
Fixed “Trying to access array offset on false” in
assets/snippets/docinfo/snippet.docinfo.php
(0.4.2: the snippet now handles false from getPageInfo() and from the TV functions, and returns an empty string when docid is empty or 0.)

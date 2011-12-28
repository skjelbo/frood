Installing The Frood
====================

*Author* [Jens Riisom Schultz](mailto:jers@fynskemedier.dk)
*Since*  2011-06-21

To set a module up for The Frood, you need to create an `.htaccess`-file and add The Frood as an external to the module.


Add The Frood as an external
----------------------------

From the command line:

	cd /the/root/of/the/module
	mkdir lib
	svn add lib
	svn propedit svn:externals lib

Add the following line:

	frood svn://develop.fyens.dk/frood/tags/whinyantelope/src

Save, quit and...


Throw on a `.htaccess` file
---------------------------

Edit `.htaccess` in the root of the module (Change `module_name` to the actual dirname of the module):

*THERE ARE TWO PLACES YOU NEED TO EDIT HERE!!!*
*One is the module name, and the other is to read the comments with !!!'s and take approriate action.*

	RewriteEngine on

	# !!! You need to change this to the correct module name.
	RewriteBase /modules/module_name/

	# This rule excludes real files from the rewriting and lets them pass through unaffected.
	RewriteCond %{REQUEST_FILENAME} !-f

	# !!! This rule excludes real folders from the rewriting and lets them pass through unaffected.
	# !!! This line should ONLY be included in current modules which use index.php in the root of
	# !!! the module, or, possibly, in the root of another folder.
	RewriteCond %{REQUEST_FILENAME} !-d

	# Direct all requests to lib/frood/run/run.php, except specified file types.
	RewriteRule !\.(js|ico|txt|gif|jpg|png|css)$ lib/frood/run/run.php

Now add the `.htaccess`:

	svn add .htaccess

Edit the CHANGELOG - type something clever like, "Added the potential to make this module awesome.

Commit.

	svn ci -m "Soon The Frood will rule the world\!"

Update

	svn up


*That's it.*
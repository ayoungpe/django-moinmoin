# Introduction #

Here is an example apache configuration for hosting Django and Moinmoin on the same virtual machine. It took me a while to sort it all out, so I'm copying it here too.

# Details #
```
<VirtualHost *:80>
	ServerAdmin webmaster@localhost
	DocumentRoot "/home/tom/website"

	Alias /admin-media /usr/lib/python2.5/site-packages/django/contrib/admin/media
	Alias /media /home/tom/website/media
	Alias /moin_static181 /usr/share/moin/htdocs

	WSGIScriptAlias /wiki /home/tom/moin/moin.wsgi	
	
	<Location "/">
		SetHandler python-program
		PythonHandler django.core.handlers.modpython
		SetEnv DJANGO_SETTINGS_MODULE website.settings
		PythonDebug On
		PythonPath "['/home/tom'] + sys.path"
	</Location>	

	<Location /media>
		SetHandler None
	</Location>

	<Location /admin-media>
		SetHandler None
	</Location>

	<Location /wiki>
		SetHandler None
	</Location>

	<Location /moin_static181>
		SetHandler None
	</Location>

	<Directory /usr/share/moin/htdocs>
		Order allow,deny
		Allow from all
	</Directory>

	<Directory /home/tom/website/media>
		Order allow,deny
		Allow from all
	</Directory>

	<Directory /usr/share/moin/htdocs>
		Order allow,deny
		Allow from all
	</Directory>
	
	ErrorLog /var/log/apache2/error.log

	# Possible values include: debug, info, notice, warn, error, crit,
	# alert, emerg.
	
	LogLevel warn

	CustomLog /var/log/apache2/access.log combined

</VirtualHost>
```
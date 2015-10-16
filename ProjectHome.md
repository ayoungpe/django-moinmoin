### A Django authentication module for moinmoin. ###

Integrate a Moinmoin wiki into a Django website, complete with single sign on and everything!

The module links into Django's session and authentication systems to automatically authenticate using Django's session cookie.

Tested with django 1.0.2 and moinmoin 181.

This is a bastardisation of the ExternalCookie Moinmoin authentication system described here: http://moinmo.in/HelpOnAuthentication/ExternalCookie

I knocked it up in a hour or two, so use at your own risk. It seems to works well, though.

## Assumptions ##

1 - You have Django installed and working and you can login to the /admin site for example.

2 - Django and Moinmoin are installed on the same host. The cookie won't work otherwise.

> Have a look at the wiki for an apache config example.

3 - You're using something unix-y i.e. Not Windows.

## Installation ##

1 - Put djangoAuth.py next to your wikiconfig.py in your moinmoin installation.

2 - Copy the required parts of your django settings file into djangoAuth.py

3 - Put this line at the top of your wikiconfig.py

> `from djangoAuth import DjangoAuth`

4 - Put something like this in class Config() in your wikiconfig.py:

> `auth = [ DjangoAuth(autocreate=True) ]`

5 - Follow the instructions here: http://moinmo.in/HelpOnAuthentication/ExternalCookie for altering your moinmoin themes to update your login and logout links.

## Testing ##

1 - Login to your django admin site to set the cookie.

2 - Navigate to your moinmoin site - you should magically be logged in.

3 - Logout of your django admin site

2 - Navigate to your moinmoin site - you should magically be logged out.

There are some very basic logs in /tmp/cookie.log that might help here.

Good Luck.
Update: We are now on Weblate 2.1. Totally need to update the docs sometime ...

This is a quick doc dump from installing Weblate and needs to be prettified some :-)

* Create Droplet (used CentOS 6.5 32bit with 512mb memory) + matching DNS entry translate.terasology.org
* Make email forward translate@terasology.org
* `yum install wget`
* `cd /opt`
*  `wget https://bitnami.com/redirect/to/41289/bitnami-weblate-1.9-2-linux-installer.run`
* `chmod u+x bitnami-weblate-1.9-2-linux-installer.run`
* `./bitnami-weblate-1.9-2-linux-installer.run --mode text`
* Follow prompts - don't start the app yet (although it seemed like it started anyway)
* Create an OAuth application on GitHub
* Edit config at `/opt/weblate-1.9-2/apps/weblate/weblate/settings.py`
 * Enable GitHub OAuth at `AUTHENTICATION_BACKENDS`
 * Copy in the client ID and secret from GitHub app
 * Add "Terasology" to `SITE_TITLE`
 * `URL_PREFIX = ''` instead of having 'weblate' in there
* Edit config at `/opt/weblate-1.9-2/apps/weblate/conf/httpd-app.conf` for short URLs (avoids serving a bitnami placeholder)
 * Remove one `WSGIScriptAlias`
 * Set the other to plain / instead of /weblate
 * Remove weblate from the media and static Aliases
* Create SSH key
 * `mkdir /sbin/.ssh`
 * `chown daemon:daemon /sbin/.ssh`
 * `sudo -u daemon ssh-keygen -t rsa`
 * update the email associated with the key (edit `id_rsa.pub`)
* Add public key to the robot user account on GitHub
 * verify on host: `sudo -u daemon ssh -T git@github.com`
* Add email if needed to the robot user account
* `/opt/weblate-1.9-2/ctlscript.sh restart`
* Go to admin console ssh section (http://translate.terasology.org/admin/ssh/) and test host "github.com"
* Supposedly change the site entry from example.com to translate.terasology.org ... but trying that (adding a new entry then later renaming the default and deleting the extra) broke the site once, had to rebuild :D Goes with also setting the site in settings.py but doesn't seem to matter much?
* Add projects & sub projects. BE SURE TO USE THE SSH URLS (starts with git@github.com)

Note: With this setup the involved services do not auto-start after a server restart.

Thanks to Weblate for the great product, including the nice bitnami installer, and to Minetest for having published a helpful page detailing their installation :-)

* https://weblate.org
* https://bitnami.com/stack/weblate
* http://dev.minetest.net/Installing_Weblate


# Installing Weblate 2.4

2015-12-13
msteiger
CentOS 7.1

yum install git

yum install mariadb mariadb-server

CREATE USER 'weblate'@'%' IDENTIFIED BY 'weblatePassword';
GRANT SELECT ON weblate.* TO 'weblate'@'%';


sudo systemctl start mariadb.service
--> Launch now
sudo systemctl enable mariadb.service
--> Launch at boot time

yum install epel-release

--> python-django is 1.6.11 -> Weblate 2.4 needs 1.7

yum install python-pip
pip install django

django-admin --version

--> 1.9+

pip install translate-toolkit

pip install python-social-auth

pip install Whoosh==2.5.7

pip install Pillow

--> already exists

yum install python-lxml

yum install python-dateutil

pip install django-compressor


pip install django-crispy-forms

pip install pyuca

pip install weblate

--> Maybe pip install weblate automatically installs the right things?


--> Install webserver

yum install httpd mod_wsgi

yum install memcached

pip install python-memcached
--> manage.py --> Error 'module' object has no attribute 'PY2'
pip install --upgrade six


--> Configure apache2

 /etc/httpd/conf.d/weblate.conf from examples/apache.conf


--> Weblate with MySQL support:

yum install MySQL-python

--> manage.py is a runnable 'weblate' command for the pip installer and stored in usr/bin 
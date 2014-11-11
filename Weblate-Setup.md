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
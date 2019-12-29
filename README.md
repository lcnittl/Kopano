# Kopano
Scripts for Kopano.

`get-kopano-community.sh`: This script pull the community files for your OS and setup a repo so you can use apt-get to install.

Currently tested on Debian 9 but should work for Debian 8/Ubuntu 16/18 .04 also.
This eliminates the use of `dpkg -i *.deb on kopano-community files.`

It setups a local file repo, which is easy to adapt for a webserver repo, examples are provided in the files.
It also adds the z-push repo and libreoffice-online repo for you.
I've also added an autobackup function, so you can revert to a previous version if needed.

For the quick and unpatient, keep the defaults and run:
```
wget -O - https://raw.githubusercontent.com/thctlo/Kopano/master/get-kopano-community.sh | bash
apt install kopano-server-packages
```

And too see the new versions you can use/install:
```
apt-cache policy kopano-server-packages kopano-webapp z-push-kopano libreoffice-online
```

Note, when you are upgrading and you might see packages are "kept back".
This is why:
Kopano is fast moving at the moment, if new packages are added then these are not installed,
when you just run apt update, in these cases you must use `apt dist-upgrade`.
So make sure you always check for "kept back" packages.

The script its defaults will do following for you:
- create a folder `/home/kopano`
- create a subfolder `apt`
- create a subfolder `backups`
- pulls the files from the Kopano community site
- make a backup of the previous version to `/home/kopano/backups/OS-ARCH-Date`
- cleanup leftovers in `apt`
- add z-push repo ( `/etc/apt/sources.list.d/kopano-z-push.list` )
- add libreoffice repo  ( `/etc/apt/sources.list.d/kopano-libreoffice-online.list` )
- setup the local-file repo ( `/etc/apt/sources.list.d/kopano-community.list` )
the repo example file:
  - File setup for Kopano Community: `deb [trusted=yes] file:/home/kopano/apt/ amd64/`
  - Webserver setup for Kopano Community: `deb [trusted=yes] http://localhost/apt amd64/`
  To enable the webserver, install a webserver ( apache/nginx )
  Now symlink `/home/kopano/apt/` to `/var/www/html/apt`
  And dont forget to change localhost to you hostname of ip of you server.


## Donations
If you like my work, support me a bit, even with 1 $ you are helping me.
I dont ask for hunderds, a (few) buck(s) is/are a great gift also.
- [Donate via Paypal](https://www.paypal.me/LouisVanBelle) (my paypal email is louis at van-belle .nl)
- Donate via Bitcoin: 3BMEXFUrncjVKByryNU1fcVLBLKE8i9TpX

## Thanks

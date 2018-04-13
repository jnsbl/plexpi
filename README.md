# plexpi

Ansible playbook for setting up Raspberry Pi as media server with [Plex Media Server](https://www.plex.tv/) and
[PlexConnect](https://github.com/iBaa/PlexConnect) so that it can be [connected](https://github.com/iBaa/PlexConnect/wiki/Install-Guide-AppleTV-Ethernet) with Apple TV (2nd generation).

## Features

Ansible roles and their features:

* **raspbian**
  * Disable GUI at boot time
  * Update APT, upgrade all packages (tag: `upgrade_packages`)
  * Update hostname
  * Add ansible to sudoers
  * Set static IP address
* **vim**
  * Install Vim
  * Use `.vimrc` with sensible defaults
* **htop**
  * Install [htop](https://hisham.hm/htop/)
* **win2utf8**
  * Install `win2utf8` (`iconv` wrapper for converting Cp1250-encoded subtitles to UTF-8)
* **plexmediaserver**
  * Install latest [Plex Media Server for Raspberry Pi](https://dev2day.de/plex-media-server-arm/)
  * Configure PMS to use `pi` user instead of `plex`
  * Install [csfd-plex](https://github.com/misko/csfd-plex) to get metadata from [csfd.cz](www.csfd.cz)
* **plexconnect**
  * Install [PlexConnect](https://github.com/iBaa/PlexConnect/wiki/Install-Guide)
  * Generate [certificate](https://github.com/iBaa/PlexConnect/wiki/Install-Guide-Mac-Certificates)
  * Set up PlexConnect as service for automatic startup

# How to use

## Prerequisites

* [Install Ansible](http://docs.ansible.com/intro_installation.html) on the computer which you want to control your Raspberry Pi from (the _host computer_)
* [Install Git](https://help.github.com/articles/set-up-git/) on the _host computer_
* [Install Raspbian](https://www.raspberrypi.org/documentation/installation/) on the Raspberry Pi you want to set up
* [Set up SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) on the Raspberry Pi you want to set up

## Installation

1. Clone this repository to the _host computer_

```
git clone https://github.com/jnsbl/plexpi.git
```

2. Edit `inventory` inside this directory as necessary

3. _(optional)_ Edit `host_vars/plexpi.yml` as necessary

4. Run `ansible-playbook main.yml -i inventory` inside this directory to provision everything

5. [Install PlexConnect certificate](https://github.com/iBaa/PlexConnect/wiki/Install-Guide-Certificate-via-Ethernet) to AppleTV

## Running a specific set of tagged tasks

You can filter which part of the provisioning process to run by specifying a set of tags using `ansible-playbook`'s `--tags` flag. The tags available are `raspbian`, `boot_options`, `upgrade_packages`, `vim`, `htop`, `win2utf8`, `plexmediaserver` and `plexconnect`.

```
ansible-playbook main.yml -i inventory --tags "plexmediaserver,plexconnect"
```

## Running without doing any changes

You can run the playbook and see what changes would be done without actually changing anything.

```
ansible-playbook main.yml -i inventory --check --diff
```

# Resources

The following links helped me to build the playbook:

* [Raspberry Pi Plex Server: Setup Your Very Own Media Server](https://pimylifeup.com/raspberry-pi-plex-server/)
* [A more powerful Plex media server using Raspberry Pi 3](https://www.element14.com/community/community/raspberry-pi/raspberrypi_projects/blog/2016/03/11/a-more-powerful-plex-media-server-using-raspberry-pi-3)
* [Turn a Raspberry Pi into a Plex Media Server](https://www.codedonut.com/raspberry-pi/raspberry-pi-plex-media-server/)
* [PlexConnect Wiki](https://github.com/iBaa/PlexConnect/wiki)
* [AppleTV + SSL + PlexConnect](https://langui.sh/2013/08/27/appletv-ssl-plexconnect/)

# License

[MIT](LICENSE)

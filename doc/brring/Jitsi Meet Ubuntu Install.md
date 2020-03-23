# Jitsi Meet Ubuntu Install

First install the Jitsi repository key onto your system:

    wget -qO - https://download.jitsi.org/jitsi-key.gpg.key | sudo apt-key add -

Create a sources.list.d file with the repository:

    sudo sh -c "echo 'deb https://download.jitsi.org unstable/' > /etc/apt/sources.list.d/jitsi-unstable.list"

Update your package list:

    sudo apt-get -y update

Install nginx

    apt -y install nginx

Install Jitsi-Meet

	sudo apt-get -y install jitsi-meet

Say yes to Generate self-signed

Install Let's Encrypt:

    /usr/share/jitsi-meet/scripts/install-letsencrypt-cert.sh

## Building

### Install Node

    curl -sL https://deb.nodesource.com/setup_13.x | sudo -E bash -
    sudo apt-get install -y nodejs

[Source](https://github.com/nodesource/distributions/blob/master/README.md)

### Make Jitsi

    npm install

    make

### Build Debian Packages

Easy way to compile package from source is using `dpkg-buildpackage`. 

Install:

    apt-get install build-essential fakeroot debhelper

Then inside the package directory there should be a debian/ subdirectory, containing debian/control and debian/rules (and probably more stuff, too).

Run below and install any missing dependencies:

    dpkg-checkbuilddeps

Edit `debian/changelog` to add a new changelog entry, with a new version. Otherwise apt will be annoyed. Alternatively, install `devscripts` and use `dch -l`.

Build binary packages only:

    dpkg-buildpackage -rfakeroot -b -uc

Build binary and source packages:

    dpkg-buildpackage -rfakeroot -us -uc

You should now have some new .deb files in the parent directory, ready to be installed with dpkg -i

[Source](https://unix.stackexchange.com/questions/117503/how-to-compile-a-debian-package-from-source)

### Install deb packages

    cd ../
    dpkg -i jitsi-meet-web-config_1.0.1-1_all.deb
    dpkg -i jitsi-meet-web_1.0.1-1_all.deb
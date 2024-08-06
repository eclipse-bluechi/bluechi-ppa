# PPA for Eclipse BlueChi

This is the PPA repository for [Eclipse BlueChi](https://github.com/eclipse-bluechi/bluechi)'s .deb packages.

## Installation

```bash
# Add BlueChi PPA
$ curl -s --compressed "https://raw.githubusercontent.com/eclipse-bluechi/bluechi-ppa/main/deb/KEY.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/bluechi.gpg >/dev/null
$ curl -s --compressed -o /etc/apt/sources.list.d/bluechi.list "https://raw.githubusercontent.com/eclipse-bluechi/bluechi-ppa/main/deb/bluechi.list"
$ sudo apt update

# Install BlueChi packages
$ sudo apt install bluechi-controller bluechi-agent bluechictl
```

## Adding new package versions

First, follow the instructions to [build .deb packages for Eclipse BlueChi](https://github.com/eclipse-bluechi/bluechi/tree/main/debian).
Add the resulting .deb packages to this repository and run:

```bash
# Packages & Packages.gz
dpkg-scanpackages --multiversion . > Packages
gzip -k -f Packages

# Release, Release.gpg & InRelease
apt-ftparchive release . > Release
gpg --default-key "${EMAIL}" -abs -o - Release > Release.gpg
gpg --default-key "${EMAIL}" --clearsign -o - Release > InRelease

# Finally, commit & push
```

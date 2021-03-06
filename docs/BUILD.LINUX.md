# Build Instructions using GCC

Linux binaries can be built for LOOT, and these instructions are for doing so on
Ubuntu 12.04, though they may also apply to other versions and
distributions.

## Building

Most of the procedure for building the API, tests and metadata validator can be
found in the `.travis.yml` file, which is the configuration file for LOOT's
Travis CI instance. However, Travis instances have a few more libraries and
utilities by default than Ubuntu 12.04 does, and the procedure does not
cover building the GUI application, so these differences will be covered here.

Linux builds of the GUI application should be considered officially
**unsupported and unmaintained**, though contributions are welcome.

## Installing Missing Dependencies

### Base Dependencies

```
sudo apt-get install python-software-properties git build-essential libcurl4-openssl-dev
```

### UI Dependencies

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 68576280
sudo apt-add-repository 'deb https://deb.nodesource.com/node_4.x precise main'
sudo apt-get update
sudo apt-get install nodejs libx11-dev libgtk2.0-dev libnss3-dev libgconf2-dev libxss-dev libasound2-dev libxtst-dev
```

## Pre-built Boost Packages Workaround

The pre-built Boost packages for Boost 1.55 and below in Ubuntu were built without C++11 support, which causes an error when linking with a C++11-built LOOT binary. While it's better to use a build of Boost with C++11 support when building LOOT, the error can be worked around by running the following before running CMake:

```
export TRAVIS=1
```

## Runtime Differences

Not all LOOT's features have been implemented for Linux builds. Issues labelled
`linux` on LOOT's issue tracker cover such missing features where they can be
implemented. Unavoidable platform differences are documented here:

* On Windows, LOOT can detect game installs using their Registry entries. On
  Linux this is obviously not possible, so either game paths will have to be
  entered manually in LOOT's settings dialog when it is run, or LOOT will need
  to be installed beside a game's Data folder for that game to be detected.

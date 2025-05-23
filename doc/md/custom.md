# Building Quenva Linux from Source

The build process for Quenva Linux uses a Makefile to automate maintenance, build, and release procedures. This includes downloading components, running tests, generating documentation, building the ISO image, and generating checksums.

## Build Requirements

- Ubuntu-based system (recommended: latest LTS version)
- Essential build tools and live-build package
- At least 10GB of free disk space
- Good internet connection for package downloads

## Build Process

1. Install the required packages:
```bash
sudo apt update
sudo apt install live-build make git
```

2. Clone the repository:
```bash
git clone https://github.com/quenva/quenva-config.git
cd quenva-config
```

3. Start the build:
```bash
make build
```

The build process will:
- Set up the live-build environment
- Download and configure all required packages
- Set up KDE Plasma desktop environment
- Configure system settings and branding
- Create the bootable ISO image

## Changing the default build configuration

`live-build` is configured through files under the `auto/` and `config/` directories.

```
.
├── auto                        #main live-build configuration
├── config
│   ├── archives                #package mirrors/repositories
│   ├── hooks                   #extra scripts to run during build stages
│   ├── includes.binary         #files to include on the ISO filesystem
│   ├── includes.chroot         #files to include in the live system's filesystem
│   ├── includes.installer      #files to include in the installer's filesystem
│   ├── package-lists
│   │   └── *.list.chroot		#packages to install on the live system
│   │   └── *.list.binary		#packages to place in the APT repository on the ISO image
│   ├── packages.chroot         #standalone .deb packages to install on the live system
│   └── task-lists              #tasksel tasks to install on the live system
├── doc			#user documentation
├── Makefile	#main automation, dependencies management, ...
└── scripts		#extra automation scripts

```

### auto/

* `auto/config` sets basic configuration settings for the build (architecture, boot configuration, installer...), see [`man lb config`](https://manpages.debian.org/bookworm/live-build/lb_config.1.en.html)
* `auto/clean` is run automatically before each build to ensure the build directory is free of any artifacts from previous builds (download caches are kept). See [`man lb clean`](https://manpages.debian.org/bookworm/live-build/lb_clean.1.en.html)
* `auto/build` contains the command used for the build, and basic logging settings


### config/includes.chroot/

Files to copy to the resulting live system (eg. modified configuration or data files under `etc/, opt/, usr/, ...`)

Scripts and data that do not belong to an existing Debian package _should_ be distributed as [custom packages](http://wiki.debian.org/Packaging), and not stashed directly into this directory. Debian packages can also handle custom configuration files (see [`man dpkg-divert`](https://manpages.debian.org/bookworm/dpkg/dpkg-divert.1.en.html)).

For example, to add custom files/unpackaged programs inside your live system:

```bash
git clone https://gitlab.com/nodiscc/toolbox config/includes.chroot/opt/toolbox
git clone https://gitlab.com/nodiscc/debian-live-config config/includes.chroot/opt/dlc
echo "blacklist nouveau" > config/includes.chroot/etc/modprobe.d/
```

### config/package-lists/

* `*.chroot`: lists of packages to install on the resulting image/system
* `*.binary`: lists of additional packages to add to the ISO image `pool/` directory (to use as an offline repository/mirror) (not required for the live system to work)

Simply use the `.list` extension to install packages in the live system and include them in the `pool/` directory in the ISO image as well.


### config/packages.chroot/

`.deb` packages placed here will be installed to the live system. May be useful when:

- You need a package that is not available in Debian (see [requests for packaging](http://wnpp.debian.net/))
- The package can be downloaded as a standalone `.deb` on the original project website OR you want to build a package yourself
- You don't want to add a third-party repository to your APT sources list (see below).

Caveats:

 - Packages placed here will _not_ receive upgrades through APT (unless they are someday added to official Debian repositories)
 - Packages placed here are not GPG-signed. Ensure you download/build the package over a secure channel.

See [Makefile.extra](https://gitlab.com/nodiscc/debian-live-config/-/blob/master/Makefile.extra) for examples.


### config/includes.installer/

`preseed.cfg` is used to preconfigure the _installer_ using [preseeding](https://wiki.debian.org/Preseed).


### config/preseed/

`*.chroot.cfg` used to preseed debconf values inside the _resulting live system_.


### config/hooks/

Scripts used to run arbitrary commands at different stages of the build (`*.hook.chroot` or `.*chroot.binary`). See `/usr/share/doc/live-build/examples/hooks/` for examples.


### config/archives/

This directory contains lists of APT repositories from which packages will be downloaded during the build [[1]](https://live-team.pages.debian.net/live-manual/html/live-manual/customizing-package-installation.en.html#380). It uses the [sources.list](https://wiki.debian.org/SourcesList) format.


### config/includes.binary/

Additional files to place at the root of the ISO image filesystem (these files will be directly accessible when mounting the ISO).

## Other

### Setting the locale/language

Currently only 2 locales (english and french) are pre-generated, other languages have to be manually added to the build configuration, and the ISO rebuilt.


### Release process

- [ ] `git tag $new_version`
- [ ] `make bump_version`, update version indicators, `git add` changes
- [ ] Update release date in CHANGELOG.md, `git add CHANGELOG.md`
- [ ] `make doc && git add doc/md && git commit -m "release v$new_version"`
- [ ] `git tag -f --sign $new_version && git push && git push --tags`
- [ ] `make && make checksums sign_checksums test_imagesize`
- [ ] `make tests`
  - BIOS mode: test live mode in all languages
  - BIOS mode: test offline installation
  - UEFI mode: test offline installation
  - During installation, test the following disk partitioning schemes:
    - [ ] Automatic whole disk encrypted LVM
    - [ ] Automated whole disk LVM
    - [ ] Automated whole disk partitioning
    - [ ] Manual
- [ ] Copy latest CHANGELOG.md entry to a new [Github](https://github.com/nodiscc/debian-live-config/releases)/[Gitlab](https://gitlab.com/nodiscc/debian-live-config/-/releases) release
- [ ] attach `debian-live-config-X.Y.Z-debian-bookworm-amd64.iso debian-live-config-release.key SHA512SUMS SHA512SUMS.sign` to the releases
- `Publish release`
 


## See also

 - <https://stdout.root.sx/links/?searchtags=debian>

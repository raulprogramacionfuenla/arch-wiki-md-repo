## Contents

*   [1 Current setup](#Current_setup)
    *   [1.1 luna.archlinux.org](#luna.archlinux.org)
    *   [1.2 nymeria.archlinux.org](#nymeria.archlinux.org)
    *   [1.3 dragon.archlinux.org](#dragon.archlinux.org)
    *   [1.4 alberich.archlinux.org](#alberich.archlinux.org)
    *   [1.5 gudrun.archlinux.org](#gudrun.archlinux.org)
    *   [1.6 gerolde.archlinux.org](#gerolde.archlinux.org)
    *   [1.7 celestia.archlinux.org](#celestia.archlinux.org)
*   [2 Desired setup](#Desired_setup)
    *   [2.1 vostok.archlinux.org (old name, new box, Intel Xeon E3-1245 2 x 3 TB 16GB ECC RAM)](#vostok.archlinux.org_.28old_name.2C_new_box.2C_Intel_Xeon_E3-1245_2_x_3_TB_16GB_ECC_RAM.29)
    *   [2.2 apollo.archlinux.org ([1])](#apollo.archlinux.org_.28.5B1.5D.29)
    *   [2.3 soyuz.archlinux.org ([2])](#soyuz.archlinux.org_.28.5B2.5D.29)
    *   [2.4 orion.archlinux.org (Intel Xeon E3-1245V2 32GB ECC 2x3TB)](#orion.archlinux.org_.28Intel_Xeon_E3-1245V2_32GB_ECC_2x3TB.29)
*   [3 Plan of attack](#Plan_of_attack)
*   [4 misc TODO](#misc_TODO)

# Current setup

## luna.archlinux.org

*   bbs
*   wiki
*   aur
*   mailman

## nymeria.archlinux.org

*   mail
*   repos/rsync

## dragon.archlinux.org

*   backups

## alberich.archlinux.org

*   releng stuff. no idea
*   tracker

## gudrun.archlinux.org

*   planet
*   bugs
*   archweb
*   patchwork
*   projects

## gerolde.archlinux.org

## celestia.archlinux.org

*   pkgbuild.com

# Desired setup

## vostok.archlinux.org (old name, new box, Intel Xeon E3-1245 2 x 3 TB 16GB ECC RAM)

*   backups

## apollo.archlinux.org ([[1]](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))

*   bbs
*   wiki
*   aur
*   mailman
*   planet
*   bugs
*   archweb
*   patchwork
*   projects

## soyuz.archlinux.org ([[2]](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))

*   pkgbuild.com
*   releng stuff. no idea
*   tracker

## orion.archlinux.org (Intel Xeon E3-1245V2 32GB ECC 2x3TB)

*   repos/rsync
*   sources
*   archive

# Plan of attack

*   Get new servers (2 [px61-ssd](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))
*   Write ansible scripts for all services
*   Services are to be split into 2 servers so that one is the webhost with outside-facing stuff and one is for internal stuff
*   Delete all old stuff in the wiki about old setups

# misc TODO

*   Run local resolving nameserver on mail server to make sure blacklist/whitelist checks are not blocked because the hetzner ns has hit some limits (install local unbound + change DNS in networkd file)

*   Set up email on vostok
*   Set up status backup checking script (ask Florian, simple find command) on vostok

*   Set up orion
    *   Set up sources and repos
        *   sources are a part of the repos (currently split to a different box for space and bandwidth reasons)
        *   repos need dbscripts
            *   needs ssh keys for all users
            *   Try to avoid changing any paths from the current setup on nymeria to make migration easy for users
            *   Use a generic hostname when telling people the new ssh address for svn. Don't have them set up svn to orion.archlinux.org
    *   Set up rsync/web access to repos (and sources)
        *   Limit access to the repos to the lastsync file only
    *   Migrate archive from seblu's server
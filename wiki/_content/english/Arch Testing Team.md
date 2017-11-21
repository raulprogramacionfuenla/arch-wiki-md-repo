The Arch Testing Team is a group within the Arch community in charge of making sure that packages submitted to the testing repositories are functional. This includes, making sure that the package installs correctly, that it doesn't cause breakage with packages of which it depends on, among others.

Arch Testers sign off packages after vouching for their correctness so that they can be moved from the testing repositories into the core, community, or extra repositories.

## Contributing

You can apply to be an official Arch tester by contacting [Florian Pritz](https://www.archlinux.org/people/developers/#bluewind) via [email](mailto:bluewind@xinu.at) and requesting a tester account.

If you're given a tester account, you should be able to log in into archweb and see a *signoffs* tab on it. The *signoffs* tab will contain a list of packages that are currently in the testing repositories and need at least two *signoffs* (i.e., a rubber-stamp vouching for the correctness of a package).

You may then test the listed packages locally and signing them off if they are correct by clicking on the *signoff* button for each package.

## Guidelines

In order to test an arch package, keep the following aspects in mind:

*   If you're testing a kernel or a package that relies on kernel modules, you **should restart the machine and ensure that it boots correctly**
*   Although testing on virtualization software is not prohibited, it may not be as useful as testing a package in a bare-metal installation. This applies specially to packages that are susceptible to different types of hardware, such as kernel packages.
*   Is you're testing a library, you may want to execute a binary that uses such library. Make sure the shared object file is loaded using ldd.
*   Likewise, if there is a package that ships executable packages, testing their basic functionality is encouraged.
*   If you notice an error when testing a package, contact the maintainer listed for that package with a detailed bug report including information such as:
    *   Package name, version and pkgrel
    *   Which component of the package was the one to error (e.g., one of the binaries, or a config file)
    *   Root of the error (e.g., during installation, or usage, etc.)
    *   Any relevant error messages/logs

## Coordination

You can coordinate with other testers on the [#archlinux-testing](ircs://chat.freenode.net/archlinux-testing) IRC channel.

You can follow updates by packager activity on the [arch-commits](https://list.archlinux.org/pipermail/arch-commits) mailing list (high traffic).
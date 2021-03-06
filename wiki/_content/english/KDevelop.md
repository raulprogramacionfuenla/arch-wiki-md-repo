*"[KDevelop](http://kdevelop.org/) is a free, open source IDE (Integrated Development Environment) for MS Windows, Mac OS X, Linux, Solaris and FreeBSD. It is a feature-full, plugin extensible IDE for C/C++ and other programming languages. It is based on KDevPlatform, and the [KDE](/index.php/KDE "KDE") and [Qt](/index.php/Qt "Qt") libraries and is under development since 1998."*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Plugins](#Plugins)
*   [2 Building additional plugins](#Building_additional_plugins)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 KDevCMakeManager](#KDevCMakeManager)

## Installation

[Install](/index.php/Install "Install") the [kdevelop](https://www.archlinux.org/packages/?name=kdevelop) package.

### Plugins

Install plugins to provide autocompletion and other language-specific features:

*   For PHP, install the [kdevelop-php](https://www.archlinux.org/packages/?name=kdevelop-php) package
*   For Python, install the [kdevelop-python](https://www.archlinux.org/packages/?name=kdevelop-python) package

## Building additional plugins

The KDevelop Parser Generator ([kdevelop-pg-qt](https://www.archlinux.org/packages/?name=kdevelop-pg-qt) package) is required to build additional plugins. Plugins will not compile if this package is not installed beforehand.

## Troubleshooting

### KDevCMakeManager

Make sure [cmake](https://www.archlinux.org/packages/?name=cmake) is installed if you get this error: "*Could not load project management plugin KDevCMakeManager*".
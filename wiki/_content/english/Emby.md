[Emby](https://emby.media/) is a personal media server, which has clients for many platforms. It is used to organize personal home media, as well as play back on other devices. There are a large amount of channels that are supported by the community, and can even be used with PVR and Tuner cards to provide TV streaming remotely.

## Installation

[Install](/index.php/Install "Install") the [emby-server](https://www.archlinux.org/packages/?name=emby-server) package.

## Usage

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `emby-server.service`.

Access Emby through the browser by navigating to [http://localhost:8096/](http://localhost:8096/)

Emby runs under the [user](/index.php/User "User") and [user group](/index.php/User_group "User group") `emby`. To provide Emby access to you media library, either add user emby to the group that owns your files:

```
sudo gpasswd -a emby audio

```

or [change their owner](/index.php/File_permissions_and_attributes#Changing_ownership "File permissions and attributes") to user emby.
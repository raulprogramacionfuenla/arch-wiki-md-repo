**Subsonic** is a music server that lets you store your music on one machine and play it from other machines, cell phones, via a web interface, or various other applications. It can be installed using the [subsonic](https://aur.archlinux.org/packages/subsonic/) package on [AUR](/index.php/AUR "AUR").

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Install transcoders](#Install_transcoders)
    *   [1.2 HTTPS Setup](#HTTPS_Setup)
        *   [1.2.1 With Subsonic](#With_Subsonic)
        *   [1.2.2 With Nginx](#With_Nginx)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 FLAC playback](#FLAC_playback)
    *   [2.2 UTF-8 file names not added to the database](#UTF-8_file_names_not_added_to_the_database)
    *   [2.3 Accessing the database](#Accessing_the_database)
*   [3 Madsonic](#Madsonic)
*   [4 External links](#External_links)

## Configuration

After performing any configuration, remember to [restart](/index.php/Restart "Restart") `subsonic.service`.

### Install transcoders

By default, Subsonic uses FFmpeg to transcode videos and songs to an appropriate format and bitrate on-the-fly. After installation, you can change these defaults so that, for example, Subsonic will transcode FLAC files using FLAC and LAME instead of FFmpeg. You should therefore [Install](/index.php/Install "Install") the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg), and you may also want to install [flac](https://www.archlinux.org/packages/?name=flac) and [lame](https://www.archlinux.org/packages/?name=lame).

For security reasons, Subsonic will not search the system for any transcoders. Instead, the user must create symlinks to the transcoders in the `/var/lib/subsonic/transcode` folder. Create the symlinks like so:

```
$ cd /var/lib/subsonic/transcode
# for transcoder in ffmpeg flac lame; do ln -s "$(which $transcoder)"; done

```

### HTTPS Setup

#### With Subsonic

To enable HTTPS browsing and streaming, edit `/var/lib/subsonic/subsonic.sh` and change this line:

```
SUBSONIC_HTTPS_PORT=0

```

To this:

```
SUBSONIC_HTTPS_PORT=8443

```

**Note:** port 8443 seems hard-coded somewhere. When attempting to change it to port 8080 it will automatically redirect the browser to port 8443 after manually accepting the invalid HTTPS certificate. You will still be able to re-navigate to port 8080 after the warning page and have it work on that port.

#### With Nginx

If you already have multiple web services running, it might be easier to use a single SSL configuration everywhere. The following Nginx configuration runs Subsonic under [https://example.com/subsonic](https://example.com/subsonic) :

```
server {
    listen              443 default ssl;
    server_name         example.com;
    ssl_certificate     cert.pem
    ssl_certificate_key key.pem

    location /subsonic {
      proxy_set_header X-Real-IP         $remote_addr;
      proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto https;
      proxy_set_header Host              $http_host;
      proxy_max_temp_file_size           0;
      proxy_pass                         [http://127.0.0.1:4040](http://127.0.0.1:4040);
      proxy_redirect                     http:// https://;
    }
} 
```

To run Subsonic under a different path, you have to set the following options in `/var/lib/subsonic/subsonic.sh` :

```
SUBSONIC_CONTEXT_PATH=/subsonic
SUBSONIC_HOST=127.0.0.1
SUBSONIC_PORT=4040
SUBSONIC_HTTPS_PORT=0
```

## Troubleshooting

### FLAC playback

The FFmpeg transcoder doesn't handle FLAC files well, and clients will often fail to play the resultant streams. (at least, on [my](/index.php?title=User:Ichimonji10&action=edit&redlink=1 "User:Ichimonji10 (page does not exist)") machine) Using FLAC and LAME instead of FFmpeg solves this issue. This workaround requires that the FLAC and LAME transcoders have been installed, as explained in [#Install transcoders](#Install_transcoders).

Start Subsonic and go to `settings > transcoding`. Ensure that the default FFmpeg transcoder does not get used on files with a "flac" extension, then add a new entry. You'll end up with something like this:

| Name | Convert from | Convert to | Step 1 | Step 2 |
| mp3 default | ... NOT flac ... | mp3 | ffmpeg ... |
| mp3 flac | flac | mp3 | flac --silent --decode --stdout %s | lame --silent -h -b %b - |

### UTF-8 file names not added to the database

You must have at least one UTF-8 [locale](/index.php/Locale "Locale") installed.

If you start subsonic using `/etc/rc.d/subsonic`, and your /etc/[rc.conf](/index.php/Rc.conf "Rc.conf") has `DAEMON_LOCALE="no"`, then the subsonic daemon will be started with the C locale, and Java will skip any folders with "international characters" (e.g. ßðþøæå etc.). Either set `DAEMON_LOCALE` to `"yes"` (but this will affect **all** rc.daemons), or add a line to the beginning of `/var/subsonic/subsonic.sh` which sets `LANG` to an installed UTF-8 locale, e.g. `LANG=nn_NO.utf8`.

### Accessing the database

Subsonic stores all its data inside a [HyperSQL](http://hsqldb.org/) database in `/var/lib/subsonic/db`. You can access it with a simple web interface by going to [http://localhost:4040/db.view](http://localhost:4040/db.view) (replace with your Subsonic URL).

You can also use the SQLTool command-line tool from the HyperSQL distribution, found in [hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/). Note that this tool cannot be run concurrently with your Subsonic instance, so you will have to either shut it down or copy the database directory.

SQLTool first needs a `~/sqltool.rc` file with the following contents :

```
urlid subsonic
url jdbc:hsqldb:/var/lib/subsonic/db/subsonic
username sa
password
```

Then, you can for example export all the contents in the `MEDIA_FILE` table :

```
$ java -jar /usr/share/java/sqltool.jar subsonic - <<< '\xq MEDIA_FILE'
8074 row(s) fetched from database.
Wrote 3252295 characters to file 'MEDIA_FILE.csv'.
```

## Madsonic

Madsonic is a fork of Subsonic with extra features, does not require a registration fee (read completely free) and is available in AUR.

Once you start the server, pay close attention to the Transcoding options, as you will probably have to change the command from "Audioffmpeg" to "ffmpeg".

## External links

*   [Official web site](http://www.subsonic.org)
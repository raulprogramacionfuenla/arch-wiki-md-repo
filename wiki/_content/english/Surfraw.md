[Surfraw](https://en.wikipedia.org/wiki/Surfraw "wikipedia:Surfraw") provides a fast UNIX command line interface to a variety of popular WWW search engines. Surfraw was originally created by Julian Assange.

## Installation

[Install](/index.php/Install "Install") the [surfraw](https://www.archlinux.org/packages/?name=surfraw) package.

## Configuration

Surfraw uses the default browser to open the successful query. If none of the standard browsers are installed, Surfraw will call $BROWSER. If that variable is empty, you will get an error message as Surfraw has no way to open the query. You can configure your browser, and any other options, via `~/.config/surfraw/conf`:

```
SURFRAW_graphical_browser=/usr/bin/chromium
#SURFRAW_text_browser=/usr/bin/elinks
SURFRAW_graphical=yes

```

There is a default config file installed at `/etc/xdg/surfraw/conf` that contains all of the configurable options.

## Usage

Surfraw consists of a collection of shell scripts, called elvi, each of which searches a specific web site.

To see the list of elvi type:

```
$ surfraw -elvi

```

You can call surfraw in full, or the shortened form:

```
$ sr duckduckgo *topic_name*

```

You can also add `/usr/lib/surfraw` to your `$PATH` to call the elvi directly.

There are over 100 elvi available for searching the web, e.g. from amazon:

```
$ surfraw amazon -search=books -country=en -q Stanislaw Lem 

```

To search the [AUR](/index.php/AUR "AUR"):

```
sr aur *package_name*

```

To search this wiki:

```
sr archwiki *article_name*

```

For a full list of web site search scripts see: [List of Elvi](https://gitlab.com/surfraw/Surfraw/wikis/current-elvi)
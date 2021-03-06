[Prey](https://www.preyproject.com/) is a set of scripts that helps you track your computer when it is stolen.

This guide shows you how to install Prey.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Plugins](#Plugins)
    *   [2.2 GUI config](#GUI_config)
    *   [2.3 Standalone Mode](#Standalone_Mode)
    *   [2.4 Troubleshooting](#Troubleshooting)
        *   [2.4.1 Beeping](#Beeping)
    *   [2.5 Bugs](#Bugs)

## Installation

Install [prey-node-client](https://aur.archlinux.org/packages/prey-node-client/) from the [AUR](/index.php/AUR "AUR").

## Configuration

**Note:** It is [no longer possible](http://answers.preyproject.com/topics/add-new-device-manually#message-53178b9f27af477ee7000492) to add new devices using the control panel on Prey's website. Use [the Node.js client](https://github.com/prey/prey-node-client) or [the GUI](#GUI_config).

First you must to have a Prey's account, if you don't have it, you can create it on the [website](https://panel.preyproject.com/signup/). To add your device, run `prey_project config account setup` and type your email account and password. Or use the [the GUI](#GUI_config) to set your account.

Run `prey_project config activate` as prey user to ensure that the configuration is correct. One way to accomplish this is with `sudo -u prey prey_project config activate`.

The installer enable automatically the [systemd](/index.php/Systemd "Systemd") service **prey-agent** to start Prey at boot. You can check if it's loaded and running with `systemctl status prey-agent`

### Plugins

To enable/disable plugins, you must run `prey_project config plugins` and read the usage to enable/disable and list the available plugins.

### GUI config

You can use a GUI to configure prey using the `prey_project config gui` command:

```
# prey_project config gui

```

### Standalone Mode

By enabling **url-trigger** and **report-to-inbox** plugins you can set a standalone prey client, triggering emailed reports whenever a URL returns a specific status code.

### Troubleshooting

To troubleshoot, run

 `$ prey_project config check` 

Ensure you have enabled [systemd](/index.php/Systemd "Systemd") service **prey-agent.service** to start Prey at boot.

If you're not receiving webcam images in you reports, install [xawtv](https://www.archlinux.org/packages/?name=xawtv) from the official repositories.

#### Beeping

If [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot") is installed, prey will use it to take a screenshot if the `session` module is enabled. Unfortunately, scrot emits an annoying beep everytime it is run. To disable beeping, append `xset -b` to the beginning of `/usr/share/prey/modules/session/core/run`.

### Bugs

There seems to be a bug in version 0.5.3 which gives an error if the SMTP password is set when using "email" post_method, which returns an error, but works fine when executed normally without the --check option.
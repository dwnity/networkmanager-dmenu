# Networkmanager-dmenu

Manage NetworkManager connections with dmenu, [Rofi][1] or [Bemenu][2] instead of nm-applet

**WARNING** _Two breaking changes 2021-12-08_

1. _ALL_ menu configuration moved to `dmenu_command`, including `-i`. Note
   options changed in config.ini.example
2. Minimum Python version now 3.7

## Features

- Connect to existing NetworkManager wifi or wired connections
- Connect to new wifi connections. Requests passphrase if required
- Connect to _existing_ VPN, Wireguard, GSM/WWAN and Bluetooth connections
- Enable/Disable wifi, WWAN, bluetooth and networking
- Launch nm-connection-editor GUI
- Support for multiple wifi adapters
- Optional Pinentry support for secure passphrase entry
- Delete existing connections
- Rescan wifi networks
- Uses notify-send for notifications if available

## Installation

- Copy script somewhere into $PATH OR

  - Archlinux: [AUR package][3] OR
  - Gentoo: [Woomy Overlay][4]

## Requirements

1. Python 3.7+
2. NetworkManager
3. Dmenu, Rofi or bemenu
4. Python gobject (PyGObject, python-gobject, etc.)
5. (Debian/Ubuntu based distros) libnm-util-dev and gir1.2-nm-1.0 (you have to
   explicitly install the latter on Debian Sid)
6. (optional) The network-manager-applet package (in order to launch the GUI
   connection editor, if desired. The nm-applet does _not_ need to be started.)
7. (optional) Pinentry. Make sure to set which flavor of pinentry command to use
   in the config file.
8. (optional) ModemManager for WWAN support.
9. (optional) notify-send for notifications (connected, disconnected, etc.)

## Configuration 

- To customize behavior, copy config.ini.example to
  ~/.config/networkmanager-dmenu/config.ini and edit.
- All theming is done through the respective menu programs. Set `dmenu_command`
  with the desired options, including things like `-i` for case insensitivity.
  See config.ini.example for examples.
- If using dmenu for passphrase entry (pinentry not set), dmenu options in the
  `[dmenu_passphrase]` section of config.ini will set the normal foreground and
  background colors to be the same to obscure the passphrase. The [Suckless
  password patch][6] `-P` option is supported if that patch is installed. Rofi and
  bemenu will use their respective flags for passphrase entry.
- Set default terminal (xterm, urxvtc, etc.) command in config.ini if desired.
- Saved connections can be listed if desired. Set `list_saved = True` under
  `[dmenu]` in config.ini. If set to `False`, saved connections are still
  accessible under a "Saved connections" sub-menu.
- If desired, copy the networkmanager_dmenu.desktop to /usr/share/applications
  or ~/.local/share/applications.
- If you want to run the script as $USER instead of ROOT, set [PolicyKit
  permissions][5]. The script is usable for connecting to pre-existing
  connections without setting these, but you won't be able to enable/disable
  networking or add new connections.

### Config.ini values

| Section              | Key                | Default   | Notes                          |
|----------------------|--------------------|-----------|--------------------------------|
| `[dmenu]`            | `compact`          | `False`   |                                |
|                      | `dmenu_command`    | `dmenu`   | Command can include arguments  |
|                      | `list_saved`       | `False`   |                                |
|                      | `pinentry`         | None      |                                |
|                      | `rofi_highlight`   | `False`   |                                |
|                      | `wifi_chars`       | None      | String of 4 unicode characters |
| `[dmenu_passphrase]` | `obscure`          | `False`   |                                |
|                      | `obscure_color`    | `#222222` | Only applicable to dmenu       |
| `[editor]`           | `gui_if_available` | `True`    |                                |
|                      | `terminal`         | `xterm`   |                                |

## Usage

`networkmanager_dmenu [-h] <menu args>`

- Run script or bind to keystroke combination
- If desired, menu options can be passed on the command line instead of or in
  addition to the config file. These will override options in the config file.

## MIT License

[1]: https://davedavenport.github.io/rofi/ "Rofi"
[2]: https://github.com/Cloudef/bemenu "Bemenu" 
[3]: https://aur.archlinux.org/packages/networkmanager-dmenu-git/ "AUR Package" 
[4]: https://github.com/Woomy4680-exe/Woomy-overlay "Woomy Overlay" 
[5]: https://wiki.archlinux.org/index.php/NetworkManager#Set_up_PolicyKit_permissions "PolicyKit permissions"
[6]: https://tools.suckless.org/dmenu/patches/password/ "Suckless password patch" 

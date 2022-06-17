# cfiles
`cfiles` is a terminal file manager with vim like keybindings, written in C using the ncurses
library. It aims to provide an interface like [ranger](https://github.com/ranger/ranger) while being lightweight, fast and minimal.

## Dependencies
- `ncurses`
- `cp` and `mv` for copying and moving
- `fzf` for searching
- `ueberzug` for image previews
- `mediainfo` for viewing media info and file sizes
- `atool` for archive previews
- `poppler`(specifically `pdftoppm`) for pdf previews

## Installing
### Arch Linux
Arch Linux users can install a binary package by adding the following to `/etc/pacman.conf`:
```
[swindles-arch-packages]
SigLevel = Optional DatabaseOptional
Server = https://git.cbps.xyz/swindlesmccoop/$repo/raw/branch/master/$arch
```
### Other distributions and MacOS
`make && sudo make install`

## Keybindings
| Key | Function |
|:---:| --- |
| <kbd>h j k l</kbd> | Navigation keys |
| <kbd>G</kbd> | Go to end |
| <kbd>g</kbd> | Go to top |
| <kbd>H</kbd> | Go to top of current view |
| <kbd>M</kbd> | Go to middle of current view |
| <kbd>L</kbd> | Go to bottom of current view |
| <kbd>pgup</kbd> | Scroll Up One Page |
| <kbd>pgdn</kbd> | Scroll Down One Page |
| <kbd>f</kbd> | Search using fzf |
| <kbd>F</kbd> | Search using fzf in the present directory |
| <kbd>S</kbd> | Open Shell in present directory |
| <kbd>space</kbd> | Add/Remove to/from selection list |
| <kbd>tab</kbd> | View selection list |
| <kbd>e</kbd> | Edit selection list |
| <kbd>u</kbd> | Empty selection list |
| <kbd>y</kbd> | Copy files from selection list |
| <kbd>v</kbd> | Move files from selection list |
| <kbd>a</kbd> | Rename Files in selection list |
| <kbd>dd</kbd> | Move files from selection list to trash |
| <kbd>dD</kbd> | Remove selected files |
| <kbd>i</kbd> | View mediainfo and general info |
| <kbd>I</kbd> | View preview |
| <kbd>.</kbd> | Toggle hidden files |
| <kbd>b</kbd> | Toggle borders |
| <kbd>'</kbd> | View/Goto bookmarks |
| <kbd>m</kbd> | Add bookmark |
| <kbd>E</kbd> | Edit bookmarks |
| <kbd>p</kbd> | Run external script |
| <kbd>r</kbd> | Reload |
| <kbd>q</kbd> | Quit |

## Directories Used
`cfiles` uses `$XDG_CONFIG_HOME/cfiles` directory to store the clipboard file. This is used so that the clipboard
can be shared between multiple instances of `cfiles`. That's why I won't be adding tabs in `cfiles` because multiple
instances can be openend and managed by any terminal multiplexer or your window manager.
Note that this also means the selection list will persist even if all instances are closed.

`cfiles` also uses `$HOME/.local/share/Trash/files` as the Trash Directory, so make sure this directory exists before you try to delete a file.

For storing bookmarks, `cfiles` uses `$XDG_CONFIG_HOME/cfiles/bookmarks` file. Bookmarks are stored in the form `<key>:<path>`. You can either edit this file directly
or press `m` in `cfiles` to add new bookmarks.

`cfiles` looks for external scripts in the `$XDG_CONFIG_HOME/cfiles/scripts` directory. Make sure the scripts are executable before moving them to the scripts directory.

If `$XDG_CONFIG_HOME` is not set, then `$HOME/.config` is used.

## Opening Files
You can set `FILE_OPENER` in `config.h` to specify your file opening program. It is set to use my  `filehandler` script [here](https://git.cbps.xyz/swindlesmccoop/not-just-dotfiles/src/branch/master/.local/bin/filehandler) by default but you can change it to anything like `xdg-open` or `thunar`. macOS users need to set it to `open` for `xdg-open`-like functionality.

## Image Previews
We use Ueberzug for image previews because images will scale with different terminal sizes, even if it is a bit slower (working on optimizations).

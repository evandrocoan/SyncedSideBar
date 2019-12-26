SyncedSideBar
=============

[Sublime Text](http://www.sublimetext.com/) plugin to sync project sidebar
(folder view) with the currently active file.

As you switch tabs Sublime highlights only files in folders that are already expanded. This plugin makes that work for all files. It accomplishes this through use of the "reveal in side bar" command from the default context menu.


## Installation

### By Package Control

1. Download & Install **`Sublime Text 3`** (https://www.sublimetext.com/3)
1. Go to the menu **`Tools -> Install Package Control`**, then,
    wait few seconds until the installation finishes up
1. Now,
    Go to the menu **`Preferences -> Package Control`**
1. Type **`Add Channel`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
    input the following address and press <kbd>Enter</kbd>
    ```
    https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json
    ```
1. Go to the menu **`Tools -> Command Palette...
    (Ctrl+Shift+P)`**
1. Type **`Preferences:
    Package Control Settings – User`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
    find the following setting on your **`Package Control.sublime-settings`** file:
    ```js
    "channels":
    [
        "https://packagecontrol.io/channel_v3.json",
        "https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json",
    ],
    ```
1. And,
    change it to the following, i.e.,
    put the **`https://raw.githubusercontent...`** line as first:
    ```js
    "channels":
    [
        "https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json",
        "https://packagecontrol.io/channel_v3.json",
    ],
    ```
    * The **`https://raw.githubusercontent...`** line must to be added before the **`https://packagecontrol.io...`** one, otherwise,
      you will not install this forked version of the package,
      but the original available on the Package Control default channel **`https://packagecontrol.io...`**
1. Now,
    go to the menu **`Preferences -> Package Control`**
1. Type **`Install Package`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
    search for **`SyncedSideBar`** and press <kbd>Enter</kbd>

See also:

1. [ITE - Integrated Toolset Environment](https://github.com/evandrocoan/ITE)
1. [Package control docs](https://packagecontrol.io/docs/usage) for details.


Usage
-----

As you move between tabs in a sublime window, the plugin will automatically trigger Sublime to reveal it in the sidebar. If the sidebar is hidden, the plugin will attempt to detect this and disable automatic syncing (see sublime versions note below).

### Reveal all tabs

When re-opening a project Sublime collapses the sidebar folders regardless of which tabs are open. To fix this, when a window opens the plugin will cycle through all open tabs causing each one to be revealed in the sidebar.

You can turn this behaviour off through the `reveal-all-tabs` configuration setting.

Command palette features
------------------------

This plugin adds some useful features to the Command Palette (Command+Shift+P on Mac, Ctrl+Shift+P on Linux/Windows).

#### Enable/Disable

Helper commands for enabling/disabling automatic syncing are available as `Side Bar: Enable Sync` and `Side Bar: Disable Sync`. This modifies the _global_ `reveal-on-activate` configuration.

#### Reveal File

If automatic syncing is disabled, files can be manually revealed via the command `Side Bar: Reveal File`. This is literally equivalent to using the context menu.

Configuration
-------------

Settings can be overridden on a per-project basis by adding them to the `settings` block in the project file rather than the global Sublime configuration.

* `reveal-on-activate` controls the automatic reveal as the active tab changes (true by default).
* `reveal-all-tabs` controls whether or not the plugin will cycle through all tabs when a window opens (true by default).


Sublime versions and sidebar visibility
---------------------------------------

This plugin works on both Sublime Text 2 and Sublime Text 3 beta. The new capabilities enabled by ST3 are designed to gracefully degrade to the old behaviour on ST2.

With ST3 build `3098` or above the plugin makes use of the new sidebar visibility API to disable automatic syncing when the sidebar is hidden.

With ST3 builds `3025`-`3097` the plugin _monitors_ sidebar visibility. It forces the sidebar to become visible the first time a window is opened in each Sublime session, and after that watches for the sidebar hide command to disable automatic syncing until it is shown again.

With ST2 and older ST3 builds the plugin has no means to track the sidebar visibility and will _always_ reveal the active file as it changes. This will show the sidebar if you try to hide it, so use the command palette features to disable sync manually.

Credits
-------

Original technique figured out by Mylith at sublimetext.com forum:
http://www.sublimetext.com/forum/viewtopic.php?f=2&t=4080

Created by [@sobstel](https://github.com/sobstel) in 2012, I took over development about a year later. Project migrated here in 2016.

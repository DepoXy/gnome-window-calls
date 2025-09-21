@@@@@@@@@@@@@@@@@@@@@@
``gnome-window-calls``
@@@@@@@@@@@@@@@@@@@@@@

.. |window-calls| replace:: ``window-calls``
.. _window-calls: https://extensions.gnome.org/extension/4724/window-calls/

Shell interface to |window-calls|_ GNOME Shell extension.

########
Features
########

Defines a handful of Bash functions used to find, raise, and
minimize desktop windows managed by Wayland.

- Think of this project as a replacement for ye-olde |wmctrl|_
  command; or, if you're familiar with the macOS ecosystem,
  think of it as something you might accomplish with
  |Hammerspoon|_ (or |KarabinerElements|_, or |skhdrc|_).

.. |wmctrl| replace:: ``wmctrl``
.. _wmctrl: https://en.wikipedia.org/wiki/Wmctrl

.. |Hammerspoon| replace:: Hammerspoon
.. _Hammerspoon: https://www.hammerspoon.org/

.. |KarabinerElements| replace:: Karabiner Elements
.. _KarabinerElements: https://karabiner-elements.pqrs.org/

.. |skhdrc| replace:: ``skhd``
.. _skhdrc: https://github.com/koekeishiya/skhd

#####
Usage
#####

- Get a list of window IDs
  (using method ``org.gnome.Shell.Extensions.Windows.List``)::

    $ . lib/gnome-window-calls.sh

    $ get_window_ids_Wayland

- Get the window ID for the active window::

    $ get_window_ids_Wayland_focused

- Get a list of window IDs matching a specific criteria,
  e.g., find all terminal windows::

    $ get_window_ids_Wayland_filtered 'select(
      .wm_class == "gnome-terminal-server" or
      .wm_class == "Alacritty"
    )'

- Raise the window with the specified ID
  (using method ``org.gnome.Shell.Extensions.Windows.Activate``)::

    $ raise_window_Wayland_titled "nvim"

- Minimize the window with the specified ID
  (using method ``org.gnome.Shell.Extensions.Windows.Minimize``).

  E.g., minimize the active window::

    $ minimize_window_Wayland "$(get_window_ids_Wayland_focused)"

############
Dependencies
############

This library requires the |window-calls|_ GNOME Shell extension:

https://extensions.gnome.org/extension/4724/window-calls/

https://github.com/ickyicky/window-calls

- The ``window-calls`` extension exposes a D-Bus interface.

  - E.g., if you want to list window details, try::

      $ gdbus call --session --dest org.gnome.Shell \
        --object-path /org/gnome/Shell/Extensions/Windows \
        --method org.gnome.Shell.Extensions.Windows.List

This project (``gnome-window-calls``) simply wraps the D-Bus
interface to provide easy shell access for common operations.

################
Related Projects
################

This project is used by two of the author's other projects:

https://github.com/DepoXy/sh-humble-prompt 🙇

https://github.com/DepoXy/gvim-open-kindness 🐬

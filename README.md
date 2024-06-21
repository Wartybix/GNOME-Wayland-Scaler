# Oschowa's Original README
## gnome-randr

This tries to reimplement the some of the functionality of 'xrandr' for the gnome desktop using mutter's dbus-api.
It currently has not been tested with fractional scaling support.

# Wartybix's Modifications
## Additions

Implemented a quick fix that prevents `gnome-randr.py` from crashing when using
VRR.

This fork mostly just adds some simple scripts to change the scaling between different
modes (i.e., 'native' and 'scaled') and an installer. These 'mode' scripts can 
be helpful to call if you have issues like an incorrect detected resolution 
running fullscreen applications (like games) using Wayland with a scaling factor 
other than 1.

If this is something that might be helpful to you, you can clone this repo with
`git clone https://github.com/Wartybix/GNOME-Wayland-Scaler` in your terminal,
and edit the scripts in the `modes` directory to your liking. By default, the
values assume a scaling factor of 1.25 (or 125%) so you will need to adjust
these to your needs if you use a different scaling factor. The scripts also
assume an output of `DP-5`, so you may need to change this also. You can find
out your output name by simply running `gnome-randr.py` without any arguments 
and looking under 'associated physical monitors'.

In each of the scripts, the text-scaling factor is also adjusted. The idea
behind this is that, when in 'native' mode, the text size matches that of when
using display scaling (i.e. in 'scaled' mode), for ease of reading when using
desktop applications alongside the application you need to use the 'native' mode
for. Using text scaling alone is not optimal, as some other elements of the GUI
like icons don't scale correctly in all applications compared to using display scaling, but
it is better than nothing.

## Adding to Launch Arguments

Example of a Steam game's launch argument:
```
~/.local/share/gnome-randr/modes/native-res.sh && %command%; ~/.local/share/gnome-randr/modes/scaled-res.sh
```

This applies the 'native' mode before opening the game, to allow the game to use
the correct resolution. Then, once the game is closed, it re-applies the 
'scaled' mode.

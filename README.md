# lemonbar-empowered

A script for easy Powerline bars creation for LemonBar.

# Requirements

lemonbar-empowered is written in Python3.4, and should work since Python3.3.
Since Lemonbar-empowered is a wrapper around
[LemonBar](https://github.com/LemonBoy/bar), it is also a requirement.

Additional programs may be required for some plugins.

# Installation

    python setup.py install

# Usage

After installation, you just have to launch `lemonbar-empowered`, which will
search for a config file named `$(HOME)/.config/lemonbar-empowered/config.yaml`.
The syntax for the config file follows:

# Configuration file

A single file handles the bar contents and settings. It can be written in YAML
or JSON. Lemonbar-empowered can know the config type by the `-t yaml|json`
option, or by the file extension. Here is the basic syntax for a simple config
file (in YAML for this exemple):

    settings:
        font: -xos4-terminesspowerline-medium-r-normal--12-120-72-72-c-60-iso10646-1
        icon_font: -xos4-terminusicons2mono-medium-r-normal--12-120-72-72-m-60-iso8859-1
        default_tick: 10
        background_color: {background}
        foreground_color: {foreground}

    colors:
        foreground: #39496
        background: #002b36
        blue: #0000FF
        red:  #FF0000
        lightred: #AA0000
    chars:
        left_separator: 
        left_separator_light: 
        right_separator: 
        right_separator_light: 
        icon_clock: Õ
        icon_sound: Ô
    segments:
        hour:
            tick: 60
            icon: {icon_clock}
            command: date '%a %d %b %Y'
            background_color: {lightred}
        volume:
            tick: 3
            icon: {icon_sound}
            script: volume
            card: 0
        spacer:
            tick: 0
            text: My powered lemonbar
            type: spacer
        workspaces:
            type: conky



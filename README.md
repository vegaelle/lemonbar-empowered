# lemonbar-empowered

A plugin for easy Powerline bars creation for LemonBar.

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

    colors:
        black: #000000
        white: #FFFFFF
        grey: #DDDDDD
        blue: #0000FF
        red:  #FF0000
        lightred: #AA0000

    separators:
        left: 
        left_light: 
        right: 
        right_light: 

    icons:
        clock: Õ
        sound: Ô
        window: ß

    styles:
        default:
            background: black
            foreground: white
        classic:
            foreground: black
            background: blue
        urgent:
            foreground: black
            background: lightred
        disabled:
            foreground: grey
            background: black
        cpu:
            foreground: blue
            background: black

    plugins:

        left:
            workspaces:
                plugin: i3-workspaces

            window:
                plugin: window
                truncate: 20
                options:
                    icon: window

        right:
            hour:
                plugin: command
                tick: 60
                options:
                    command: date '%a %d %b %Y'
                    icon: clock
                    nice: 20
                    class: classic

            volume:
                plugin: volume
                signal: 1
                options:
                    icon: sound
                    card: 0

            spacer:
                plugin: spacer,
                tick: 0
                options:
                    class: classic
                    widescreen: true
                    text: My powered lemonbar

            conky:
                plugin: conky
                options:
                    eth: eth2
                    wlan: wlan0

## Plugins

Plugins can be used to generate one or more segments. Those have to be inside
the `$(HOME)/.config/lemonbar-empowered/plugins` directory, and be executable.

The plugins have to return JSON or YAML lists of segments, like this (for the
example, let’s say it’s a plugin which returns a list of CPU values):

    cpu0:
        icon: {icon_gear}
        text: 2%
        foreground: {white}
        background: {cyan}
        class: cpu
    cpu1:
        icon: {icon_gear}
        text: 81%
        foreground: {red}
        background: {cyan}
        class: cpu

## Signals

Sometimes, the refresh of a segment should be done by request, and not in a
given interval. You can define a signal number in a segment definition. This
number will be added to SIGRTMIN to catch incoming signals. For the previous
example, you can order a refresh of the volume segment with:

    pkill -SIGRTMIN+1 lemonbar-empowered


![wst](.media/wst.png)

## wst - wako's imple terminal <sup>st-0.9</sup>
st is a simple terminal emulator for X which sucks less.

wst basically is the same although it sucks a little more less. But don't
worry: It sucks enough less to be suckless. And it is carefully patched with
some usefull functions and options.

## Patches

### bold is not bright ([Source](https://st.suckless.org/patches/bold-is-not-bright))
In st, bold text is rendered with a bold font in the bright variant of the
current color. This patch makes bold text rendered simply as bold, leaving
the color unaffected.

### clipboard ([Source](https://st.suckless.org/patches/clipboard))
The Freedesktop standard requires you to remember which clipboard you are
keeping selections in. If you switch between a terminal and browser, you may
find this UX jarring.

Description: This trivial patch sets CLIPBOARD on selection, the same as
your browser. You may want to replace selpaste with clippaste in your
config.h bindings to complete the effect, or develop the habit to delete
config.h before and use config.def.h instead.

### delkey ([Source](https://st.suckless.org/patches/delkey))
Return BS on pressing backspace and DEL on pressing the delete key.

### disable bold italic fonts ([Source](https://st.suckless.org/patches/disable_bold_italic_fonts))
Some terminals allow disabling bold/italic fonts globally. So this patch
adds such option as well.

Set these options either in config.h, or develop the habit to delete
config.h before compiling and use config.def.h instead:

    int disablebold = 0; # change to 1 to disable bold style
    int disableitalic = 1; # change to 0 to enable italic style
    int disableroman = 0; # ...

Or choose the easy way and define them in .xresources. See below.

### scrollback ringbuffer ([Source](https://st.suckless.org/patches/scrollback))
Scroll back through terminal output using `Shift` + {`PageUp`, `PageDown`}
or if you don't like to leave home use `Alt` + {`k`, `j`}.

### w3m ([Source](https://st.suckless.org/patches/w3m))
Support w3m images hack. Similar to the patch at the FAQ, but it's simpler,
smaller, and doesn't disable double-buffering in st. Same as the FAQ patch,
the cursor line is deleted at the image, because st always renders full
lines, even when most of it is empty.

### xresources with signal reloading ([Source](https://st.suckless.org/patches/xresources-with-reload-signal))

This patch adds the ability to configure st via .xresources and signal
reloading. This patch is not based on [xresources patch](https://st.suckless.org/patches/xresources/xresourcese)
and is extended from xst's commit on github.

You can basically pass a USR1 signal to all st processes after updating* your
.xresources to reload the settings:

    # pidof st | xargs kill -s USR1

<sup>*)</sup> A good idea is to load your .xresources before running last
mentioned command:

    # xrdb -load .xresources

## Keybindings

| Key                    | Action                     |
| :----------------------| :--------------------------|
| `alt` + `k`            | Scroll up                  |
| `alt` + `j`            | Scroll down                |
| `alt` + `shift` + `K`  | Increase font size         |
| `alt` + `shift` + `J`  | Decrease font size         |
| `alt` + `shift` + `H`  | Reset to default font size |
| `ctrl` + `shift` + `C` | Copy                       |
| `ctrl` + `shift` + `V` | Paste                      |


## Sample .xresources

    st.font: Monospace-11;

    st.termname: st-256color

    st.borderpx: 2

    st.disablebold: 0
    st.disableitalic: 1
    st.disableroman: 0

    st.cwscale: 1.0
    st.chscale: 1.0

    st.cursorshape: 2

    ! one half dark
    *.foreground: #abb2bf
    *.background: #282c34
    *.cursorColor: #abb2bf

    *color0: #282c34
    *color1: #353b45
    *color2: #3e4451
    *color3: #545862
    *color4: #565c64
    *color5: #abb2bf
    *color6: #b6bdca
    *color7: #c8ccd4
    *color8: #e06c75
    *color9: #d19a66
    *color10: #e5c07b
    *color11: #98c379
    *color12: #56b6c2
    *color13: #61afef
    *color14: #c678dd
    *color15: #be5046

## Requirements

In order to build st you need the Xlib header files. To find some hints for
this sidequest use the hints described under "Installation".

## Installation

    # git clone https://github.com/wakodiwe/wst.git
    # cd wst

If you want to install st globally:

    # sudo make install
    # st

If your want to install it locally:

    # make install PREFIX=~/.local
    # st

## Uninstallation

Same as described under "Installation" but prefix "install" with "un".

## ...

Good luck!

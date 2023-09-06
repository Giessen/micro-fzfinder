# FZFinder plugin for micro editor

The plugin allows you to integrate **fzf** to select and search for your project files.

![recording-2021-11-04-231418.gif](Design/recording-2021-11-04-231418.gif)

## Information

Tested version: Micro 2.0.11; fzf 0.42.0

The advantages of my implementation:
- Ability to set the `fzf` parameters through the settings file
- Solved problem with a critical error when selecting a file
- I plan to support plugin

## Installation

This plugin for work requires `fzf`, install it in your system.

To install the plugin in `micro editor`, add to the `settings.json`:

~~~bash
micro ~/.config/micro/settings.json
~~~

~~~json
"pluginrepos": ["https://raw.githubusercontent.com/MuratovAS/micro-fzfinder/main/repo.json"],
~~~

Installing the plugin in micro editor

~~~bash
micro -plugin install fzfinder
~~~

## Settings

Fzf parameters can be set by means of `options` in the file `settings.json`:

NOTE: `bat` can be replaced with `cat`.

~~~json
"fzfcmd": "/usr/bin/fzf",
"fzfopen": "newtab",
"fzfpath": "relative",
"fzfarg": "--preview 'bat -f -p {}'",
~~~

We can also configure launch through `hot keys` in the file  `bindings.json`:

~~~json
"Alt-Tab": "command:fzfinder",
~~~

### Tips: get a colored output

The `fzfcmd` cannot be a chain of commands, like a command you pipe into fzf, but you can create a script doing that internally and set it as the command to run. To get for example a colored output, use [fd](https://github.com/sharkdp/fd): wrote a bash script for example /usr/local/bin/fzfcolored containing `fd . -t f -c always | fzf --ansi "$@"` and set `"fzfcmd": "fzfcolored"` in `settings.json`. The script receive its options from `fzfargs` ; some preview commands could bug, in this case, just set the fzf options directly in the script and disable `fzfargs`.

## Credits

A good example of the development of plugins: [micro-editor/updated-plugins](https://github.com/micro-editor/updated-plugins  )

The idea is inherited from the already unsupported expansion: [samdmarshall/micro-fzf-plugin](https://github.com/samdmarshall/micro-fzf-plugin )


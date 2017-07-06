+++
css = []
date = "2017-07-06T16:08:26+08:00"
description = ""
draft = false
highlight = true
scripts = []
tags = []
title = "Launchpad API"

+++

Launchpad provide a web service api for developer. The main area I use launchpad api on:

1. Grab/Edit bug information
2. Grab/Attach attachment

For full functionality, please refer to online document: https://api.launchpad.net/devel.html

There is a launchpadapi python client/library let you use launchpad web api easily.
The key concept is to get the launchpad object. And then manipulate the objects.

I recommended trying lp-shell in lptools packages. With lp-shell utility which provides an interactive python shell, developer could use launchpadlib python library interactively and explore functions and properties of launchpadlib.
Example:
```
b = lp.bugs[1]

print(b.title)
print(b.message_count)
```

Here is more sample scripts: https://help.launchpad.net/API/Examples



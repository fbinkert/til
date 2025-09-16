---
title: VS Code terminal has intelliSense
description: VS Code terminal now has intellisense autocomplete
pubDate: 2025-09-15
author: Fabian Binkert
tags:
  - VsCode
---
Did you know that VS Code added IntelliSense to its integrated Terminal?
It enables you to receive suggestions for files, folders, commands, command arguments, and options. 

Toggle these two flags in your `settings.json` to turn it on:
```
"terminal.integrated.shellIntegration.enabled": true, 
"terminal.integrated.suggest.enabled": true,
```

I don’t know yet if this is useful or if I’ll turn it off soon.

If it’s too annoying you can use `terminal.integrated.suggest.quickSuggestions` to prevent it from showing automatically, but let you manually bring it up via `ctrl+space`.


See also the [VS Code docs](https://code.visualstudio.com/docs/terminal/shell-integration#_intellisense-preview).

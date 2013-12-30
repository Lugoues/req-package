req-package
===========

##### Description

req-package is a macro wrapper on top of use-package.
It's goal is to simplify package dependencies management
when using use-package for your .emacs.

##### Usage

* load req-package:

```elisp
(require 'req-package)
```

* define required packages with dependencies using **:require** like this:

```elisp
   (req-package dired)
   (req-package dired-single
                :require dired
                :init (...))
   (req-package lua-mode
                :init (...))
   (req-package flymake)
   (req-package flymake-lua
                :require (flymake lua-mode)
                :init (...))
```
* to start loading packages in right order:

```elisp
   (req-package-finish)
```

##### Migrate from use-package

Just replace all `(use-package ...)` with `(req-package [:require DEPS] ...)` and add `(req-package-finish)` at the end of your configuration file.

##### Note

All use-package parameters are supported, see use-package manual
for additional info.

Also there are possible troubles with deferred loading provided by use-package.
If you want to use it, try defer all packages in one dependency tree.

More complex req-package usage example can be found at http://github.com/edvorg/emacs-configs.

##### Changelog:

* **v0.3-cycles**
    There are nice error messages about cycled dependencies now.
    Cycles printed in a way: `pkg1 -> [pkg2 -> ...] pkg1`.
    It means there're cycle around `pkg1`.
* **v0.2-auto-fetch:**
    There is no need of explicit `:ensure` in your code now.
    When you req-package it adds `:ensure` if package is available in your repos.
    Also package deps `:ensure`'d automatically too.
    Just write `(req-package pkg1 :require pkg2)` and all you need will be installed.

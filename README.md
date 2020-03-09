
# Table of Contents

1.  [Warning](#org4eadf75)
2.  [Description](#org02399c4)
    1.  [Features](#orgbf2f575)
3.  [Layer Installation](#orge06e84a)
4.  [Structurally Safe Editing](#org1c0fd7e)
5.  [Key Bindings](#org38d5a22)
    1.  [Working with Lisp files (slurpage, barfage, and more)](#org2d8a3c1)
    2.  [Help](#orgd3566e6)
    3.  [Compilation](#orgcead1c3)
    4.  [Evaluation](#orgbac53a5)
    5.  [Navigation](#org4e529d0)
    6.  [Macro-expansion](#org5cb20d1)
    7.  [REPL](#org9de0be2)
        1.  [REPL keybindings in the INSERT mode](#org120b3ad)
    8.  [Stickers](#org1c2e531)
    9.  [Tracing](#org0a2d254)

       _____    __   __  __
      / ___/   / /   \ \/ /               |\      _,,,---,,_
      \__ \   / /     \  /                /,`.-'`'    -.  ;-;;,_
     ___/ /  / /___   / /                |,4-  ) )-,_..;\ (  `'-'
    /____/  /_____/  /_/                '---''(_/--'  `-'\_)


<a id="org4eadf75"></a>

# Warning

This package is forked from [mfiano's](https://github.com/mfiano) Common Lisp Sly Layer, that is archived on
[GitHub](https://github.com/mfiano/common-lisp-sly) (i.e., it is not maintained anymore by the original author).

I am trying to revive it for my own use. I have placed it on GitHub to serve
as documentation for discussion and for help. It may dissapear at any time.

I am new to Spacemacs and Sly, so I may be doing things wrongly here I am new
to Spacemacs and Sly, so I may be doing things wrongly here.

Do not ask me on how to *help you*, as it is me that needs help. If you feel
that you can improve it, please clone it tfro the original source, implement
your improvements, and advertise so that the rest of us can benefit from your
work. 


<a id="org02399c4"></a>

# Description

This layer provides support for Common Lisp to Spacemacs using Sly. This layer should be used
instead of the `common-lisp` layer if you want to use Sly &#x2013; a more featureful Common Lisp
environment.


<a id="orgbf2f575"></a>

## Features

-   Syntax highlighting
-   Fuzzy auto-completion using `company`
-   REPL and introspection support via [Sly](https://github.com/joaotavora/sly)
-   Support for specific Lisp navigation styles via `common-lisp-mode`
-   Support for the [SBCL](http://www.sbcl.org/) backend or any other Common Lisp implementation
-   Ability to save a layout with a REPL and have it restored the next time that layout is loaded
-   Multiple REPL connections for the same or different Common Lisp images
-   REPLs have full ANSI color code support via [sly-repl-ansi-color](https://github.com/PuercoPop/sly-repl-ansi-color)
-   Stickers, a more advanced, non-intrusive alternative to print debugging, and a means for live code
    annotation.


<a id="orge06e84a"></a>

# Layer Installation

If you have previously installed SLIME in any other way, it is recommended that you uninstall it
before proceeding. You should clean up any configuration files tied to SLIME that are left behind as
well.

To use this configuration layer, add it to your `~/.spacemacs`. You will need to add `common-lisp-sly`
to the existing `dotspacemacs-configuration-layers` list in this file.

This layer defaults to using [SBCL](http://www.sbcl.org/). If you want to use a different implementation of Common Lisp, you
can specify it in your `~/.spacemacs`:

    (defun dotspacemacs/user-config ()
      (setq inferior-lisp-program "/path/to/your/lisp"))


<a id="org1c0fd7e"></a>

# Structurally Safe Editing

This layer adds support for `evil-cleverparens` which allows safe editing of lisp code by keeping the
s-expressions balanced.

By default this mode is not activated. You can turn it on locally on the active buffer with `SPC m T
s` (`s` for safe).

To turn it on automatically for all `common-lisp` buffers call the following function in your
`dotspacemacs/user-config` function:

    (spacemacs/toggle-evil-safe-lisp-structural-editing-on-register-hook-common-lisp-mode)

or to enable it for all supported modes:

    (spacemacs/toggle-evil-safe-lisp-structural-editing-on-register-hooks)

When enabled, the symbol `🆂` should be displayed in the mode line.


<a id="org38d5a22"></a>

# Key Bindings


<a id="org2d8a3c1"></a>

## Working with Lisp files (slurpage, barfage, and more)

Spacemacs comes with a special `lisp-state` for working with Lisp code that supports slurpage, barfage
and more tools you'll likely want when working with Lisp.

As this state works the same for all files, the documentation is in global [DOCUMENTATION.org](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#lisp-key-bindings). In
general, use `SPC k` to interact with `lisp-state`.


<a id="orgd3566e6"></a>

## Help

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`SPC m h a`</td>
<td class="org-left">Apropos - search for any symbol matching input (prompted)</td>
</tr>


<tr>
<td class="org-left">`SPC m h b`</td>
<td class="org-left">Show who binds the global variable at point</td>
</tr>


<tr>
<td class="org-left">`SPC m h d`</td>
<td class="org-left">Show disassembly of symbol at point</td>
</tr>


<tr>
<td class="org-left">`SPC m h h`</td>
<td class="org-left">Describe symbol at point</td>
</tr>


<tr>
<td class="org-left">`SPC m h H`</td>
<td class="org-left">Lookup symbol at point in the Common Lisp HyperSpec</td>
</tr>


<tr>
<td class="org-left">`SPC m h m`</td>
<td class="org-left">Show the usages of macro at point</td>
</tr>


<tr>
<td class="org-left">`SPC m h p`</td>
<td class="org-left">Browse package's exported symbols</td>
</tr>


<tr>
<td class="org-left">`SPC m h r`</td>
<td class="org-left">Show who refers to the global variable at point</td>
</tr>


<tr>
<td class="org-left">`SPC m h s`</td>
<td class="org-left">Show all methods specialized on class symbol at point</td>
</tr>


<tr>
<td class="org-left">`SPC m h S`</td>
<td class="org-left">Show who sets the global variable at point</td>
</tr>


<tr>
<td class="org-left">`SPC m h <`</td>
<td class="org-left">Show who calls the function symbol at point</td>
</tr>


<tr>
<td class="org-left">`SPC m h >`</td>
<td class="org-left">Show all functions called by function symbol at point</td>
</tr>
</tbody>
</table>


<a id="orgcead1c3"></a>

## Compilation

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`SPC m c c`</td>
<td class="org-left">Compile file</td>
</tr>


<tr>
<td class="org-left">`SPC m c C`</td>
<td class="org-left">Compile and load file</td>
</tr>


<tr>
<td class="org-left">`SPC m c f`</td>
<td class="org-left">Compile function</td>
</tr>


<tr>
<td class="org-left">`SPC m c l`</td>
<td class="org-left">Load file</td>
</tr>


<tr>
<td class="org-left">`SPC m c n`</td>
<td class="org-left">Remove compilation notes</td>
</tr>


<tr>
<td class="org-left">`SPC m c r`</td>
<td class="org-left">Compile region</td>
</tr>
</tbody>
</table>


<a id="orgbac53a5"></a>

## Evaluation

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`SPC m e b`</td>
<td class="org-left">Evaluate buffer</td>
</tr>


<tr>
<td class="org-left">`SPC m e e`</td>
<td class="org-left">Evaluate last s-expression</td>
</tr>


<tr>
<td class="org-left">`SPC m e E`</td>
<td class="org-left">Evaluate last s-expression and print result as a comment</td>
</tr>


<tr>
<td class="org-left">`SPC m e f`</td>
<td class="org-left">Evaluate top-level function s-expression</td>
</tr>


<tr>
<td class="org-left">`SPC m e F`</td>
<td class="org-left">Undefine the function at point</td>
</tr>


<tr>
<td class="org-left">`SPC m e r`</td>
<td class="org-left">Evaluate region</td>
</tr>
</tbody>
</table>


<a id="org4e529d0"></a>

## Navigation

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`SPC m g`</td>
<td class="org-left">Enter the navigation transient state</td>
</tr>
</tbody>
</table>


<a id="org5cb20d1"></a>

## Macro-expansion

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`SPC m m e`</td>
<td class="org-left">Macro-expand the form at point once</td>
</tr>


<tr>
<td class="org-left">`SPC m m E`</td>
<td class="org-left">Macro-expand the form at point completely</td>
</tr>


<tr>
<td class="org-left">`SPC m m s`</td>
<td class="org-left">Enter the macrostep transient state</td>
</tr>
</tbody>
</table>


<a id="org9de0be2"></a>

## REPL

Note: the following bindings are accessible via the , prefix and not `SPC m`

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`SPC m s c`</td>
<td class="org-left">Clear the REPL</td>
</tr>


<tr>
<td class="org-left">`SPC m s i`</td>
<td class="org-left">Start a new Common Lisp image</td>
</tr>


<tr>
<td class="org-left">`SPC m s I`</td>
<td class="org-left">Choose a new Common Lisp implementation and start a new image</td>
</tr>


<tr>
<td class="org-left">`SPC m s q`</td>
<td class="org-left">Quit the REPL, terminating the Common Lisp image</td>
</tr>


<tr>
<td class="org-left">`SPC m s r`</td>
<td class="org-left">Restart the Common Lisp image associated with the current REPL</td>
</tr>


<tr>
<td class="org-left">`SPC m s s`</td>
<td class="org-left">Sync the REPL with the current file buffer's package and directory</td>
</tr>
</tbody>
</table>


<a id="org120b3ad"></a>

### REPL keybindings in the INSERT mode

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`Ctrl-up`</td>
<td class="org-left">Recall previous command</td>
</tr>


<tr>
<td class="org-left">`Ctrl-down`</td>
<td class="org-left">Recall next command</td>
</tr>


<tr>
<td class="org-left">`Ctrl-r`</td>
<td class="org-left">Search for a previous command (not implemented)</td>
</tr>
</tbody>
</table>


<a id="org1c2e531"></a>

## Stickers

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`SPC m S b`</td>
<td class="org-left">Toggle breaking stickers, to have debugger come up when sticker is reached during execution</td>
</tr>


<tr>
<td class="org-left">`SPC m S c`</td>
<td class="org-left">Clear all stickers for function at point</td>
</tr>


<tr>
<td class="org-left">`SPC m S C`</td>
<td class="org-left">Clear all stickers for buffer</td>
</tr>


<tr>
<td class="org-left">`SPC m S f`</td>
<td class="org-left">Fetch recordings for sticker at point</td>
</tr>


<tr>
<td class="org-left">`SPC m S r`</td>
<td class="org-left">Cycle through the recordings of all stickers</td>
</tr>


<tr>
<td class="org-left">`SPC m S s`</td>
<td class="org-left">Add or remove (if one already exists) sticker at point</td>
</tr>
</tbody>
</table>


<a id="org0a2d254"></a>

## Tracing

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key Binding</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`SPC m t t`</td>
<td class="org-left">Toggle trace</td>
</tr>


<tr>
<td class="org-left">`SPC m t T`</td>
<td class="org-left">Toggle fancy trace</td>
</tr>


<tr>
<td class="org-left">`SPC m t u`</td>
<td class="org-left">Untrace all</td>
</tr>
</tbody>
</table>



# Table of Contents

1.  [Table of Contents](#org8b4ff96)
2.  [Warning](#orgf8097d5)
3.  [Unresolved Issues](#org9e93e66)
    1.  [Change inspector, db, xref, stickers mode from emacs to ???](#org0c47129)
    2.  [Assign `isearch-backward` to a key in repl](#org3dedb8f)
    3.  [Error highlighing and navigation](#orgcc38cfb)
    4.  [REPL key bindings](#org707e1e4)
4.  [Description](#org300d5e1)
    1.  [Features](#org58f1c18)
5.  [Layer Installation](#org699c832)
6.  [Structurally Safe Editing](#org3956aef)
7.  [Key Bindings](#orgc2e2a5e)
    1.  [Working with Lisp files (slurpage, barfage, and more)](#orga4dab4f)
    2.  [Help](#org674cfae)
    3.  [Compilation](#org0fda0e3)
    4.  [Evaluation](#orge87c730)
    5.  [Navigation](#org02d5a43)
    6.  [Macro-expansion](#org0d56514)
    7.  [REPL](#orge2ee1ea)
        1.  [REPL keybindings in the INSERT mode](#orgbb710ac)
    8.  [Stickers](#orgde4ea58)
    9.  [Tracing](#org39849c0)

       _____    __   __  __
      / ___/   / /   \ \/ /               |\      _,,,---,,_
      \__ \   / /     \  /                /,`.-'`'    -.  ;-;;,_
     ___/ /  / /___   / /                |,4-  ) )-,_..;\ (  `'-'
    /____/  /_____/  /_/                '---''(_/--'  `-'\_)


<a id="org8b4ff96"></a>

# Table of Contents

-   [2](#orgf8097d5)
-   [3](#org9e93e66)
-   [4](#org300d5e1)
    -   [4.1](#org58f1c18)
-   [Layer Installation](#org699c832)
-   [6](#org3956aef)
-   [7](#orgc2e2a5e)
    -   [7.2](#org674cfae)
    -   [7.3](#org0fda0e3)
    -   [7.4](#orge87c730)
    -   [7.5](#org02d5a43)
    -   [7.6](#org0d56514)
    -   [7.7](#orge2ee1ea)
    -   [7.8](#orgde4ea58)
    -   [7.9](#org39849c0)


<a id="orgf8097d5"></a>

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


<a id="org9e93e66"></a>

# Unresolved Issues

My list of issues that I was not able to make work


<a id="org0c47129"></a>

## Change inspector, db, xref, stickers mode from emacs to ???

Currently, these modes are in emacs mode. How to specify a vim type mode


<a id="org3dedb8f"></a>

## Assign `isearch-backward` to a key in repl

I can access `isearch-backward` functionality only by invoking the command
explicitly, using `M-x ...` or `S S ...`.

I tried assigning it to "C-r" in `common-lisp-sly/init-sly-mrepl ()...`, but
that did not work.


<a id="orgcc38cfb"></a>

## Error highlighing and navigation

-   When a function is compiled and issued an error, there is no visible
    overlay on the buffer


<a id="org707e1e4"></a>

## REPL key bindings

The key bindings listed in the [7.7](#orge2ee1ea) session to be bound to the `SPC m` key
combination do not work. Instead, they are accessible with the `,` key.


<a id="org300d5e1"></a>

# Description

This layer provides support for Common Lisp to Spacemacs using Sly. This layer should be used
instead of the `common-lisp` layer if you want to use Sly &#x2013; a more featureful Common Lisp
environment.


<a id="org58f1c18"></a>

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


<a id="org699c832"></a>

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


<a id="org3956aef"></a>

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


<a id="orgc2e2a5e"></a>

# Key Bindings


<a id="orga4dab4f"></a>

## Working with Lisp files (slurpage, barfage, and more)

Spacemacs comes with a special `lisp-state` for working with Lisp code that supports slurpage, barfage
and more tools you'll likely want when working with Lisp.

As this state works the same for all files, the documentation is in global [DOCUMENTATION.org](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#lisp-key-bindings). In
general, use `SPC k` to interact with `lisp-state`.


<a id="org674cfae"></a>

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


<a id="org0fda0e3"></a>

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


<a id="orge87c730"></a>

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


<a id="org02d5a43"></a>

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


<a id="org0d56514"></a>

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


<a id="orge2ee1ea"></a>

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


<a id="orgbb710ac"></a>

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


<a id="orgde4ea58"></a>

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


<a id="org39849c0"></a>

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


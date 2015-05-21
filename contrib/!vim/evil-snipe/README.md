# evil-snipe contribution layer for Spacemacs

![logo](img/Cat_With_Rifle.jpg)

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc/generate-toc again -->
**Table of Contents**

- [evil-snipe contribution layer for Spacemacs](#evil-snipe-contribution-layer-for-spacemacs)
    - [Description](#description)
        - [Improved f and t searches](#improved-f-and-t-searches)
        - [Improved precision search](#improved-precision-search)
    - [Install](#install)
    - [Key bindings](#key-bindings)

<!-- markdown-toc end -->

## Description
The package [evil-snipe](https://github.com/hlissner/evil-snipe)
- enables more efficient searches with `f/F/t/T`.
- adds a new, more precise search with `s/S`

Evil-snipe allows you to search more quickly and precisely in the buffer.
It does so by improving on the built in `f`/`F`/`t`/`T` searches and
adding another search command, namely `s`/`S`.

`evil-snipe` changes `s/S` behavior in order to search forward/backwards in the
buffer with two chars.

## Install

### Layer

To use this contribution add it to your `~/.spacemacs`

```elisp
(setq-default dotspacemacs-configuration-layers '(evil-snipe))
```

### Improved f and t search behavior

With evil-snipe you can define your own search scope for `f` and `t` searches
which means that you won't have to jump to the correct line before searching
with `f`/`t`/`F`/`T`. And after you have found a match, you can just press `f`
or `t` again afterwards to continue the search. No need to use `;`/`,`.

This alternate behavior is disabled by default, to enable it set the
layer variable `evil-snipe-enable-alternate-f-and-t-behaviors` to `t`:

```elisp
(setq-default dotspacemacs-configuration-layers
  '(evil-snipe :variables evil-snipe-enable-alternate-f-and-t-behaviors t ))
```

### Two-character search with s

With the `s`/`S` keys you can do a simple search like `f`/`t`, but instead
of searching for one character, you search for two. This makes the search a lot
more precise than regular `f`/`t` searches. While you can search
forward or backwards in the buffer with `/` and `?`, `s`/`S` are much easier
to reach, don't require you to press enter and they are precise enough for
many common purposes.

### More scopes

Evil-snipe also adds several scope options for searches (set
`evil-snipe-scope` and `evil-snipe-repeat-scope` to one of these, the default
value is `buffer`):

Value            | Description
-----------------|------------------------------------------------------------
buffer           | search in the rest of the buffer after the cursor (`vim-sneak` behavior)
line             | search in the current line after the cursor (`vim-seek` behavior)
visible          | search in the rest of the visible buffer only
whole-line       | same as `line`, but highlight matches on either side of cursor
whole-buffer     | same as `buffer`, but highlight *all* matches in buffer
whole-visible    | same as 'visible, but highlight *all* visible matches in buffer

If you do not want to replace the regular `f/F/t/T` behavior, just
remove this line from `evil-snipe/packages.el`:
`(evil-snipe-replace-evil)`

### Symbol groups

With symbol groups you can let a character stand for a regex, for example a
group of characters.  By adding a pair of `'(CHAR REGEX)` to the list
`'evil-snipe-symbol-groups` you can search for a regex very simply:

- Here we set the `[` character to mean `all characters "[({"` so a search
with `sa[` would find `a[`, `a{` or `a(`.

```elisp
;; Alias [ and ] to all types of brackets
(add-to-list 'evil-snipe-symbol-groups '(?\\[ \"[[{(]\"))
```

- Here we set the char `:` to mean `a regex matching python function
definitions` so by searching with `f:fff` you can quickly cycle through
all function definitions in a buffer!

```elisp
;; For python style functions
(add-to-list 'evil-snipe-symbol-groups '(?\\: \"def .+:\"\))
```

## Key bindings

TODO
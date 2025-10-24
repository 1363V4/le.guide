---
title: my micro editor config
layout: post
---

lately i had trouble with vs code server.

i tried notepad++ with a ftp configuration,
which is cool for file uploads
but not so much for live edits.

fortunately,
i find the `micro` editor
to be quite pleasant.

here is my config file
to feel at home:

## bindings.json

```json
{
    "Alt-/": "lua:comment.comment",
    "Alt-Ctrl-Up": "SpawnMultiCursorUp",
    "Alt-Ctrl-Down": "SpawnMultiCursorDown",
    "Alt-<": "NextTab",
    "CtrlUnderscore": "lua:comment.comment"
}
```

comment and multi-cursor kinda like vs code.

still using `alt-n` for FindNext because overriding `ctrl-d`
does not work for some reason.

i like the split view, still getting used to it,
but i cycle through tabs with `alt-<`
like i cycle views with `ctrl-w` (double view lol).

`ctrl-e` is very nice,
especially with the autocomplete.

## settings.json

very important to set the clipboard to terminal 
as i mostly use micro when ssh'ed.

```json
{
    "clipboard": "terminal",
    "colorscheme": "gruvbox",
    "rmtrailingws": true
}
```

---
title: cursor alternatives
layout: post
---

if you're like me
and your brain is feeling mushy lately,
you might consider an "ai detox".

and the first step is to **take back control of your editor**.

death to cursor!
we'll write our code by hand like our ancestors did!

well, yeah but... with what?

join me on my quest to leave cursor:

## first stop: micro

pros:
- works anywhere
- tabs and split view
- light and fast

cons:
- the embedded terminal is kinda annoying

settings.json:
```json
{
    "clipboard": "terminal",
    "colorscheme": "gruvbox",
    "mkparents": true,
    "rmtrailingws": true,
}
```

i just love micro's gruvbox:
the deep bleedy red is *chef's kiss*.

the best part is "clipboard": being able to copy/paste
from anywhere to anywhere is a lifesaver.

it inherits the font from oh-my-posh i think.

bindings.json:
```json
{
	"buffer": {
	   	"Alt-N": "FindNext",
	    "Alt-Ctrl-Up": "SpawnMultiCursorUp",
	    "Alt-Ctrl-Down": "SpawnMultiCursorDown",
	    "Alt-<": "NextTab|FirstTab",
	   	"Ctrl-W": "NextSplit|FirstSplit",
	},
	"terminal": {
	   	"Ctrl-W": "NextSplit|FirstSplit",
	},
}
```

i mostly use `vsplit` or `hsplit`:
you can resize panels with the mouse!

i miss the ability to zoom one split among many.
fonts scale on the terminal.
i could use a terminal splitter like tmux but hey,
it's not *that* urgent. 
`ctrl-+` and `ctrl-0` is fine for now.

an annoying part is the regex:
`ctrl-f`, `enter`, `alt-n`, `alt-p`...
takes a while to get used to.

if you're really in ai *withdrawal*,
i'd say micro is the best choice.
it's almost perfect with little to no friction.
help is baked in.
a fantastic tool.

however... you'd give up on modern niceties like
code completion (it's in micro if you press tab, but results may vary),
git integrations 
(granted, i mostly solve that with `alias gitup='git add . && git commit -m "dev" && git push'`)
or context-aware code ("i imported this library, link to its definition").

**conclusion:**
9/10. the perfect swiss knife where, unlike vi/emacs, i have low risk of cutting myself with it.

10/10 once you can fold stuff.

## back to the old school: notepad++

i decided to give old npp a try.
after all, what's better than a security breach to relaunch the hype.

so, you get back autocomplete. everywhere.
even on markdown. no you can't disable it for some languages.

i had to remap **a ton** of keys.
let's see:
- ctrl+b to "Afficher/fermer le dossier en tant qu’espace de travail"
- ctrl+shift+backspace to SCI_LINEDELETE
- ctrl+shift+: to "Commenter/décommenter (mode ligne)"
- ctrl+shift+s to "Enregistrer sous..." (wtf npp?)
- alt+shift+down to SCI_LINEDOWNRECTEXTEND but...

the last one isn't what i wanted.
this whole "npp is built on top of scintilla and you can customize both" is a nice idea,
but in practice it feels disjointed.

other than that,
select next to alt-n is kinda like micro 
(even if i'm more used to vscode's ctrl-d) and
i can't manage to duplicate a line up or down
(really liked that in vscode).

at least we get back folding
(and it's a better folding than vscode).
but it's still hard to map efficiently.

we can make it look quite modern and minimal!
mess around in the settings, minimize and disable stuff,
and apply 
[gruvbox dark hard](https://github.com/wburton95/Notepadpp-Gruvbox-Port).

more weirdities:
you need to toggle back character autocompletion (?!),
the auto indent will sometimes fail,
you don't get "smart quotes" (adding `()` or `**` around selected text)
and the extension ecosystem is quite dated and useless...

except for 
[npp ftp](https://ashkulz.github.io/NppFTP/).
now this one works as expected,
and it's time to talk about my biggest problem with cursor:

**cursor server.**

this thing will download wikipedia on your server,
mine some bitcoin 
and **then** allow you to edit files.
between two crashes.

this was the main reason i first started to move lol. it's that bad.

so, we were saying, notepad++.
it was too much pain for what it's worth.
it's fast, capable, but i feel it's designed for another kind of coder.

what now?

## have you tried rewriting in rust?

oh yeah, zed.

they're available on windows now!
so no more excuses not to test it.

the first new improvement?
control bars.

i got so used to `ctrl-p` (files) and `ctrl-shift-p` (commands)
that not only would i not imagine an editor without it,
but i wish it was present in every software too.

other than that, zed is very crisp
(love the gruvbox baby theme),
has annoying *ai* features everywhere with their
"login, connect, try now",
and is overall **very good**.

good stuff:
git integration,
seamless venv activation,
and excellent ssh workflow.

markdown has better autoclosing,
but can't fold for a weird reason.

.zedserver is 90M of storage + 430M in .local
and around 250M of RAM use,
which is... **still a lot**.
and you need to close all zed windows to free this.

> ps: cursor is 350M of junk and around 350M of RAM.

linting is opened on a different window,
which i think is a great idea but
i forgot how tedious linting could be. 
i think i'd prefer to run ruff from the cli.

that's it? zed wins?

## not so fast!

a viewer named `kimchiunagi`
suggested i use **sublime text**.

why didn't i think of it before???
it was my first text editor!
i'm coming back home `:')`

and let me tell you it is fucking 
`B L I S S`.

after an "install package" to get gruvbox,
and some adjustments:

```json
[
	{ "keys": ["ctrl+b"], "command": "toggle_side_bar" },
	{ "keys": ["alt+up"], "command": "swap_line_up" },		
	{ "keys": ["alt+down"], "command": "swap_line_down" },
	{ "keys": ["shift+tab"], "command": "unindent" },
]
```

it feels cozy.

except for the "build" thing,
doesn't interface with uv nicely,
don't know what to make of it.

i didn't find duplicate line up/down 
(it works on zed),
and the "escape to exit panel" is weird,
but you can enable close buttons like this:

```json
{
	"theme": "gruvbox.sublime-theme",
	"color_scheme": "Packages/gruvbox/gruvbox (Dark) (Hard).sublime-color-scheme",
	"gruvbox_statusbar_xxs": true,
	"gruvbox_tabs_xxs": true,
	"gruvbox_panel_xxs": true,
	"gruvbox_statusbar_button_xxs": true,
	"gruvbox_disable_panels_button": true,
	"gruvbox_enable_panel_close_button": true,
	"gruvbox_sidebar_indent_xs": true,
	"ignored_packages":
	[
		"Vintage",
	],
	"index_files": true,
}
```

sublime just feels so polished.
made with craft by caring people.
now that's what i call *vibe coding*.

btw, i also redefined "vibe coding" to mean
writing a lot of comments in your code
and sublime has **two** perfectly placed comment keybinds:

```json
[
	{ "keys": ["ctrl+/"], "command": "toggle_comment", "args": { "block": false } },
	{ "keys": ["ctrl+shift+/"], "command": "toggle_comment", "args": { "block": true } },
]
```

you have to pay for it (winrar style),
but i don't mind.
if i want it, i buy it.

so i'll try it. 
i'll stick with it and we'll see.

unfortunately, i can't try the sftp plugin
(30$, sublime is 170 with sublime merge, 200 total)
without paying for it,
so it will be mostly for local dev for now.

## conclusion

i'll roll with a 3-editor setup:
sublime on main,
zed on ssh,
micro for hard-to-reach corners and notepad replacement.

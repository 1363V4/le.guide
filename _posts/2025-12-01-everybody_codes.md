---
title: everybody codes 2025
layout: post
---

i enjoyed 
[everybody code](https://everybody.codes/events) 
a lot!

good problems and
[easter eggs](https://aoc.leg.ovh/),
what's not to like?

what's important for me in these code events:
- realize early what can and cannot work
- have fun
- read other people code
- re-read your solutions
- see your innefficiencies

it's very important to read other's code.
you already figured out the "what" by solving the problem,
so you're more efficient on the "how".

so here is my review of some shared python code:

## yldraw

[repo link](https://github.com/Yldrax/everybody-codes/tree/master/2025)

i found the very useful
[tqdm](https://tqdm.github.io/)
library.
get a loading bar for your loops!

i also see that `cmp_to_key` was not needed for day 5
and a simple lambda sort would have worked.

i brute forced day 6 (sorry).
it's nice he figured out the "wrap".

nice recursion on day 7.
let's do a quick set cheatsheet:

| **Code** |           **Means**           |
|:--------:|:-----------------------------:|
| a \|= b  | a = a.union(b)                |
| a &= b   | a = a.intersection(b)         |
| a -= b   | a = a.difference(b)           |
| a ^= b   | a = a.symmetric_difference(b) |

yes for day 8, you don't need to store every strike.
this "max update" pattern, i should use it more often.

ok he stopped around where i stopped.
i won't check after day 11 anyway.

## danagle

[repo link](https://github.com/danagle/everybody-codes-challenges/tree/main/2025-the-songs-of-ducks-and-dragons)

he "washed" his code, meaning he cleaned it
and added any "efficient" tricks
(like a modulo trick you don't see in your first pass
but understand afterwards).

but it's a bit too washed.
almost golfed.

he uses 
[numba](https://numba.pydata.org/) 
to speed up his loops. interesting.

nice use of `Counter.most_common()`.

string padding on day 6, why not.
i wondered if someone used `cycle`.

oh itertools 
[pairwise](https://docs.python.org/3/library/itertools.html#itertools.pairwise),
nice!

oh and a 
[trie](https://en.wikipedia.org/wiki/Trie)?!
ok... a prefix tree.
useful for autocomplete, spell check and ip routing.
even better is a 
[radix tree](https://en.wikipedia.org/wiki/Radix_tree),
ok ok.

oh so 
[that's how](https://docs.python.org/3/library/profile.html)
you profile python code.
might be useful for my dod posts.

oh and now a
[fenwick tree](https://en.wikipedia.org/wiki/Fenwick_tree),
watch out we've got a badass over there.
hmmm ok i don't think i'll ever use that.

day 9 he uses a trie again.
and so he doesn't do bfs like i did.
man i need to level up my trees.

ok, i learned about `nonlocal` in imbricated functions.
i don't think i should use it.

i still can't figure out what went wrong in day 10.
day 11, i also tried that and it didn't work. oh well.

nice, he made visualizations!
using `PIL.Image.fromarray()` is tight.

## alex11br  

[repo link](https://github.com/ALEX11BR/everybodyCodes2025/tree/main/d3)

oh shit. numpy arrays,
`functools.reduce`,
we've got a madman.

yeah, no, bad code.

## r01f  

[repo link](https://github.com/r0f1/everybody_codes_2025/tree/main)

nothing fancy.

i really like his:

```python
trees = [
    {a[0], b[0], c[0]}
    for a, b, c in permutations(lines, 3)
    if b > c and is_child(a[1], b[1], c[1])
]
```

quite effective.

## elandor  

[repo link](https://github.com/theElandor/ec2025/tree/main/DeD)

yuck.

---

if you want to see what i did,
[here's my code](https://github.com/1363V4/evc25).

now, let's do the same for aoc!

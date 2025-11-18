---
title: a good class - part 1
layout: post
---

**note:** this is part 1 in a series of posts about oop.

---

> consider how humans, or any other autonomous creatures of nature, operate with their model of the world. we all have our own model of the world contained in our own heads, i.e. we have a copy of the world state for our own use. we mutate the state in our heads based on inputs (events/messages) we receive via our senses. as we process these inputs and apply them to our model we may take action that produces outputs, which others can take as their own inputs. none of us reach directly into each other’s heads and mess with the neurons. if we did this it would be a serious breach of encapsulation! originally, object oriented (oo) design was all about message passing, and somehow along the way we bastardized the message passing to be method calls and even allowed direct field manipulation – yuck! whose bright idea was it to allow public access to fields of an object? you deserve your own special hell. 

> mechanical sympathy

i recently watched good videos about object-oriented programming:
- [oop is bad](https://www.youtube.com/watch?v=QM1iUe6IofM)
- [oop is embarassing](https://www.youtube.com/watch?v=IRTfhkiAqPw)
- [oop is garbage](https://www.youtube.com/watch?v=V6VP-2aIcSc)

bottom line:
**most classes are bad.**

so... how do you make a **good** class?

i propose you check for these 3 things:
- dataclass + slots
- @property
- frozen or read()

let's explain.

## dataclass + slots

first of all, **please use dataclasses.**

there's zero (0) reason not to use them:
you reduce the boilerplate,
you improve readability,
you type attributes...

and you don't lose **anything** except footguns.

```python
from dataclasses import dataclass

@dataclass
class Rectangle:
    width: float
    height: float
```

the next step is activating `slots`.

this will really boost performance (because of c shenanigans)
at the cost of not being able to add attributes at runtime,
**which you shouldn't do anyway.**

```python
@dataclass(slots=True)
class Rectangle:
    width: float
    height: float
```

next is the property check.

## @property

a class is just grouped data,
in other words **data that belongs together.**

if this data *reeaaaally* belongs together,
you should be able to compute something out of it.

in other words, you should have a **property**:

```python
@dataclass(slots=True)
class Rectangle:
    width: float
    height: float

    @property
    def area(self):
        return self.width * self.height
```

no property is a bad tell,
ask yourself why you grouped this data in the first place.
maybe your class isn't really useful.



the only exception where it's ok to not have a property
is if your class is **frozen**,
which we're gonna see in the next chapter.

## frozen or read()

alright,
now you have to make a choice.

either you freeze your dataclass,
because you wanted immutability on the data,
for example, config parameters of a script:

```python
from dataclasses import dataclass

@dataclass(frozen=True, slots=True)
class AppConfig:
    host: str
    port: int
    debug: bool = False

    @property
    def url(self):
        return f"http://{self.host}:{self.port}"
```

and that's ok.
this is a **perfectly acceptable class.**
thanks for coming to my ted talk.

---

oh, i know what you're going to say:

*"but that's not why i make classes! i want to model entities and modify their attributes!"*

i know. 

you want to make a class "monster"
to make little monsters in your game,
give them weapons, armor, attack damage,
reduce their hp when they take a hit,
apply status effects...

look, the only status effect you're gonna get
is "poisoned" when your state is all over the place.
**you're gonna die from oop.**

please reread the citation at the beginning.

if your class isn't frozen,
its attributes should **only be changed by this class**.

the way you'd do this is with a `read()` method:

```python
@dataclass(slots=True)
class Rectangle:
    width: float
    height: float

    @property
    def area(self):
        return self.width * self.height

    def read(self, message):
        """message receiver: decodes message and updates state"""
        msg_type = message.get('type')
        
        if msg_type == 'resize':
            self.width = message.get('width', self.width)
            self.height = message.get('height', self.height)
        elif msg_type == 'scale':
            factor = message.get('factor', 1.0)
            self.width *= factor
            self.height *= factor
        elif msg_type == 'set_width':
            self.width = message.get('width')
        elif msg_type == 'set_height':
            self.height = message.get('height')
        else:
            raise ValueError(f"unknown message type: {msg_type}")
```

> nb: 
> people sometimes advocate for the syntax `_method()`
> as a pythonic way to indicate a "private" method.
> i think it looks awful, and because it doesn't *actually* enforce anything,
> you'd be better off with nice comments in plain english.

of course, you can also write a `send()` method 
if you want your class to emit messages.

but, in a nutshell,
**this is how you do proper oop.**

## red flags

to conclude, some red flags.
if you see:

- state being modified outside the class
- any form of inheritance
- any form of factory (whatever that means)
- any getter or setter
- any class that fails these 3 checks

burn the code to the ground and rewrite functional.

---

there's more to it! check
[part 2]().

delaney talk:
generational index (4bit whenever you have to look up, look up to this)
sparse set = swapback with gen indexes
the queries themselves have this!
and by tracking them you get to optimize your queries!
need to dive into nats
minecraft works that way
dont use booleans! 
existential programming: read first three chapters
example: aoe has a lot of pathfindings
swapbacks alternatives: b trees, quad trees
disruptor pattern: ephermal stuff with a fixed size (very fast)
sparse set + disruptor = very fast
games are all about reusing buffers
for billions of particles: shader+ seed + time
"if you think you're gonna need one, you're wrong"
relations? not a prob with generationa indexes - pgo: profile guided optimization

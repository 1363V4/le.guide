---
title: property/frozen check
layout: post
---

> consider how humans, or any other autonomous creatures of nature, operate with their model of the world. we all have our own model of the world contained in our own heads, i.e. we have a copy of the world state for our own use. we mutate the state in our heads based on inputs (events/messages) we receive via our senses. as we process these inputs and apply them to our model we may take action that produces outputs, which others can take as their own inputs. none of us reach directly into each other’s heads and mess with the neurons. if we did this it would be a serious breach of encapsulation! originally, object oriented (oo) design was all about message passing, and somehow along the way we bastardised the message passing to be method calls and even allowed direct field manipulation – yuk! who's bright idea was it to allow public access to fields of an object? you deserve your own special hell. 
>
> mechanical sympathy

i recently watched good videos about object-oriented programming:
- https://www.youtube.com/watch?v=QM1iUe6IofM
- https://www.youtube.com/watch?v=IRTfhkiAqPw
- https://www.youtube.com/watch?v=V6VP-2aIcSc

the rule is simple:
never make a class unless sometimes.
but what's the rule?

i propose this simple check:
- **does your class have a property?** 
- **is it frozen?**

if not, it's a bad class.

---

a class is just grouped data. 
so either data that belongs together,
or computed data
(which there should be, if this data reeaaaally belongs together).

here is a python example of a good class:

```python
class Body:
    def __init__(self, weight_kg, height_m):
        self.weight_kg = weight_kg
        self.height_m = height_m

    @property
    def bmi(self):
        return self.weight_kg / (self.height_m ** 2)
```

note the `@property` for computed data.

---

even better with dataclass:

```python
from dataclasses import dataclass

@dataclass
class Body:
    weight_kg: float
    height_m: float

    @property
    def bmi(self):
        return self.weight_kg / (self.height_m ** 2)
```

best of both worlds: good syntax, helpful types.

---

`frozen` is the cherry on pancake for your immutable stuff:

```python
@dataclass(frozen=True)
class AppInfo:
    version: str
    max_retry_attempts: int
    timeout_seconds: float
```

---

bottom line:
if you see methods, inheritance...

burn the code and rewrite functional.

---
title: property/frozen check
layout: post
---

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

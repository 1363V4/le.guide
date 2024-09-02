---
title: future trip
layout: post
---

hi jeff,

i just came back from a one-month trip in europe.

or as you americans call it, *"france is closed during summer"*.

why would you care?

because traveling is 
**the most search-intensive task**
there is.

i learned a few things along the way,
and thought i might share them with you.

there's stuff for exa too.

oh, btw, welcome to my blog.

---

## before the trip

oh lord.

we used to buy "all-inclusive" vacations,
just because of the headache of planning a trip by yourself.

these travel companies take a fat margin for that convenience,
as they should be.

but not this time.

we had to:

- search countries / cities to visit
- search hotels and air bnbs
- search flights / trains / boats / buses

this is **at least a dozen different websites.** 

which means a dozen different accounts, 
and a dozen different ux/ui.

and they're all flashing
"20 seconds remaining !! only 1 room left !!".

we rode the tiger.

and in an afternoon, we came up with this:

![travel](/img/exa/travel.png)

3 weeks, 4 countries, 5 cities.

now of course,
we used comparators and aggregators: 
[kayak.com](https://www.kayak.com) 
for example saves you from checking every single flight company.

> they have an easy job,
> since they are only optimizing 
> on one or two metrics: price / duration.
>
> unfortunately, this means
> they are vulnerable to the
> [goodhart's law](https://en.wikipedia.org/wiki/Goodhart%27s_law)
> and companies develop shadow pricing.
>
> so you mainly get high-ranked cheap ryanair tickets,
> only to find out there is a 360€ extra
> if you want to board with your clothes on.

but the **main unresolved pain point** 
is that these searches were
**interdependent**.

>let's say you were planning to be in a city from monday to monday,
>but changed your mind for tuesday to tuesday.
>
>well, you now *only* need to relaunch all of your searches...
>across all search platforms...
>somewhere in these fifty open tabs.

thus the need for a more *holistic* search engine.

arc browser has an
[interesting take](https://x.com/joshm/status/1801279825522352407)
on that (personal ai).

but the problem is far from being solved.

you are juggling with a lot of stuff.
you are building and modifying hypotheses as you go.

in other words, this is the
**perfect use case for a prompt**.

so here is the billion-dollar idea:
**dynamic search.**

a search engine where what you look at changes the search query.
a search engine that gradually understands what you are searching for.
a search engine with retroaction.

i think whoever delivers the perfect ux for this will be the next google.
this is no easy feat,
but this is what the future of search looks like.

---

## during the trip

the search doesn't end there.

you start looking for things to do, places to eat...

- what are the local dishes?
- what's the reputation of this restaurant?
- is this a good spot to visit?
- is it open? is it expensive? is it crowded?
- what will the weather be like?
- ...

*all of this could have been a prompt.*

so, it turns out that these llm things are actually pretty useful.
who could have guessed.

let's review them.

### chatgpt, claude and friends

they make great tourist guides.

i used them constantly to:

- learn the language basics (hello, goodbye, thank you) with their phonetics
- translate stuff
- ask questions about monuments, statues, etc
- ask random trivia about the country 
(what's the history of austria? what does their flag represent? did they legalize cannabis?)

![chat](/img/exa/chat.png)

the results were impressive.

and e2e is coming.
and there might be fine-tuned models coming.
and there might be wearables coming.

they're versatile,
they're cheap.
they don't have the warmth and feel
of a very good guide,
but *they're already better than a bad one*,
simply because they pace at your own rhythm.

i can take an easy bet:
in the future, 
*traveling without an ai will be as unthinkable as traveling without a credit card.*

they are also pretty fun:
we finished a game of thrones
experience in croatia,
and i asked chatgpt to generate
a trivia quiz to test our knowledge
at a bar,
adjusting the difficulty on the fly.

but llms are not enough.

### perplexity

ok, let's talk about the big bad wolf.

perplexity is goated at these 3 specific use cases:

#### you need to verify the information

llms are famously known for hallucinating.

let's take the example of bus tickets:
they're infamous tourist traps.
because you're not a local,
you take the wrong ticket,
go into the wrong zones,
and walk right into a fine.

so you need to verify this information,
because chatgpt will likely freestyle a wrong answer.

perplexity solves that,
by finding and translating the right snippet for you.

also works for "is this restaurant open on mondays?" and the rest:
no hallucinations allowed -> "perplexity, do the heavy lifting".

#### you don't speak the language

english content is more globalized,
more targeted at tourists,
and more likely to be paid for (partnerships, undercover ads).

i don't speak hungarian,
but the blog from a hungarian would be helpful.
a summary of r/budapest could be helpful.

hungarian is like greek to me.
but it's not a problem for llms.

they chew right through it and output perfect english.

![babel](/img/exa/babel.jpeg)

*the great tower of babel, pieter brueghel, 1563*

pic unrelated.

#### you need miscellaneous data

blogs are low-trust content but have hidden gems,
like a cool speakeasy cocktail bar.

trip-advisor is a data dumpster,
their "ai review summary" is useless,
but you still need to crawl
one-star and five-star reviews
to avoid common caveats.

individual websites (for restaurants and attractions)
are always a terrible mess to navigate,
but they contain the most relevant info:
menu, price, opening hours.

perplexity can fetch from all these data sources at once,
and adds some nice ux/ui on top:
here is their map feature,
showcasing hidden gems around you.

![perp](/img/exa/perp.png)

in all this, exa needs to be at least on par.

---

## stress testing

by now, i'm sure you have a burning question:

> why didn't i use exa?

here, there is one thing that is very important to understand.

traveling is core to the human experience.

it is 10% global gdp,
you get to compare languages, behaviours, economics,
see nice stuff,
enjoy life.

and **how else would you suffer through this shit.**

traveling is so much pain.
do you remember bus tickets?

in vienna, to take a bus, we had to:

- download an app
- create an account
- validate the account
- select the right ticket
- pay through a web portal
- scan a qr code which is **outside** the bus
- open yet another validation screen

you need to react quickly.
you need to confirm information.
you need to pay for a lot of stuff.

there are hidden fees. conversion rates. small prints.
most of them in a language or a system you don't understand.

you lack your usual marks.
you don't want to lose time because it is vacation time.
precious time.

and beware of tourist traps,
or "fucking ripoffs"
as one gentleman said, after getting a fine
for not executing these 10+ actions in less than a minute.

**traveling is a stress test.**

this is closely related to
["using the system in anger"](https://x.com/sorreg_namtyv/status/1828419985393475977)
from curtis yarvin.

there are many details which are easy to brush off from your office chair.

but when traveling,
any friction can become paramount.

this is why you **need to get the app**.

forget paying anything using google translate on a site, won't work.
most websites don't work anyway.
apps are just easier and more secure.

this is also why
we used 
[getyourguide](https://www.getyourguide.com) 
a lot.
their app is neat.

i'm sure you see where i'm going:

**every day that passes without the exa app, you lose customers**.

early adopters, critical clients.

*ship it.*

---

## closing thoughts

some random stuff to conclude:

- **the state of ai art is terrible:**
some museums have gimmicky ai attractions,
shipped around two or three years ago, and it shows.
progress went so quick in this field that they're all outdated.
- **the state of vr art is ok:**
again, some gimmicky videos in museums,
but the bottleneck isn't the tech,
just the craft (3d modeling as in video games).
- there's **already a million** "ai trip planners" websites out there.
i'll probably never use them over a general purpose but more powerful model.
a classic conondrum for ai "wrappers".

my girl and i are young, broke and curious:
we walked 15km a day during 3 weeks.
we spent 3.1k/person for 21 days.
we had a terrific time.

most other tourists didn't do that.
most people travel to take pictures
or "party".
nobody used ai.

we still have a long way to go.

fortunately,
there's cool stuff along this road.

![buda](/img/exa/buda.jpeg)

![vienna](/img/exa/vienna.jpeg)

![sziget](/img/exa/sziget.jpeg)

![nice](/img/exa/nice.jpeg)

see ya.

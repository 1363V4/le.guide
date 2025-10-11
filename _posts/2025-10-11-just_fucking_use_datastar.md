---
title: just fucking use datastar
layout: post
---

the plan was simple:
- use [datastar](https://data-star.dev/)
- build anything you fucking want

but no, you dimwits had to have some second thoughts.

so let's have this discussion, shall we?

> context: i made a 
> [shit-ton of projects](https://leg.ovh/) with datastar and 
> [20+ youtube videos about it](https://www.youtube.com/channel/UCSD9LvJNyHGgWw5XipRuohA) 
> so yeah i'm biased, duh.

## "react is fine"

no it's not, you scum.

you make users download 
[megabytes of data](https://infrequently.org/series/performance-inequality/) 
for spinners that never fucking load.

you build services so fragile that the slightest error
sends all your infra in [a roller coaster to hell.](https://blog.cloudflare.com/deep-dive-into-cloudflares-sept-12-dashboard-and-api-outage/)

you shame us all with abhorrent code.
what's a junior dev to think when you show'em 
[your stinky codebase?](https://github.com/ladifire-opensource/facebook-codebase/blob/8fb37667acd68b1b19b0e99405ab157ede5786a3/36.js)
total fucking disgust, correct.

but the worst of your sins is your sync engine.
excuse me but 
*what do you need to fucking sync exactly*?
the server and the client?
did you try, um, i don't know, using htt-fucking-p to exchange data?!

oh you did, you sent a skeleton-ass page and instructions to download more javascript at the nearest black market.
fair, you don't build websites, you build trojan bombs, so
sync my ass.

## "ackhually..."

if you were going to say "next.js": congrats larry 
[you're a comedian](https://projectdiscovery.io/blog/nextjs-middleware-authorization-bypass).

look, i don't care if you use
svelte, vue, vite, vroom, nuxt, angular, bozo.js
or any other "i have nodes in my brain" clown-ass frameworks.

you build a pile of hot garbage on javascript. period.

because you never understood that javascript is a way to interact with the browser and the markup,
because you never understood the browser,
because you never understood the markup,
because you don't fucking read.

maybe start with "hypermedia for dummies"?

## "sikes! i use htmx"

sikes on you, you fuck.

does this look like a blog rant of peace? 

this is war, motherfucker.

you come to battle with your megatron-ass voltron-build 
glued with `htmx`, `alpine.js`, `htmx-sse`, `htmx-head-support`, `htmx-idiomorph`, `htmx-alpine-morph`, `htmx-multi-swap`...

you look like a janky knight in a cyber conflict.

we're gonna laser beam your rusty helm with half the code
and a fraction of the complexity. hold still
(or don't, doesn't matter).

## what's the big fucking deal

datastar is not miracle fucking water.

it's simply:
- htmx with oob default (the correct one btw) and a better morph
- data-attributes made reactive with signals
- ([attributes are hypermedia](https://developer.mozilla.org/en-US/docs/Web/HTML/How_to/Use_data_attributes) by the fucking way)
- and [sse support](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events)

here "sse support" just means using the fucking fetch api,
but with quality-of-life defaults like auto-reconnect and exponential backoffs.

your browser is already a fucking jet engine:
datastar doesn't reinvent the wheel,
it just puts four of them under the rocket so you can get fucking moving.

## "it's just the new fad"

the web doesn't break backward compatibility you dumbass.

datastar websites are forever.
this is what you get by building on fucking specs.

with datastar, you only manage the backend, not the backend + frontend.
complexity is a poison, if you want to manage both,
please shove this
[median lethal dose](https://en.wikipedia.org/wiki/Median_lethal_dose)
down your throat, thank ya.

and btw: never a breaking change.
datastar is just 
[a few thousand lines of typescript](https://github.com/starfederation/datastar/blob/develop/library/src/engine/engine.ts)
and it's v1 forever baby.

## "sorry i said that, i'm an old fart"

ok sensei, congrats on your mastery of php and jquery.

no, sincerely i mean it, you fucking zen monk.
you like code that reads and stuff that works.
well, the future is now and you'll be fine.
heck, you'll love it!

you're gonna be writing so much awk and so little javascript
you'll feel one step closer to heaven, you lucky fuck.

## don't fucking use datastar pro

let me say it loudly for the morons in the back
who think they can hack the fbi but can't put two and two together:
**it's just so that your fucking company can support the project!!**

convince these lobotomized suits they might need `data-persist` in the future 
or whatever other bullshit
and snatch the damn credit card.

no you're never ever gonna need any feature in pro and it's total bait,
but these guys need to eat goddammit.

## don't fucking use datastar

take a wild fucking guess: does this page use datastar?

no! it's a blog post, dumb as rocks text-on-a-page goodness!

you got multiple pages worth of information?
let me doubt that first, most of you are building landing pages
for the ceo of bluetooth-cat-litter-inc who needs a rotating marquee of sponsors.
doesn't qualify as "information", does it?

but even then, let's say you do have multiple pages,
please build an mpa.
you might even want to check the definition to that, who fucking knows.

for the remaining cases: 99% of the time
your job is to build a crud app
without adding more misery to the world.
yet you inventing ever more spectacular ways to fail at that.

we gave you 
[request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)
and you're still looking at the square peg and the round hole with intense dedication, 
you dozy ape.

god forbid you came from 
[the hn website](https://news.ycombinator.com/).
the comments don't even auto-update!
barely usable and probably zero users, i bet you that.

## closing thoughts

yes this is fucking parody.

it's inspired by [this glorious shit](https://motherfuckingwebsite.com/).

and it's made **against**
[this poop pile](https://justfuckingusereact.com/),
[this ai babble](https://reactisfuckingcool.com/),
[that big stain](https://justfuckingusehtml.com/)
and *(jesus, how many abominations must these people shit before the js god is appeased)*
[that other thing](https://justfuckingusesolid.com/).
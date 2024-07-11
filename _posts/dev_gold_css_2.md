---
title: dev - gold.css
layout: post
---


grid-auto-flow: row;

ou pas ?

---

bon tout le monde a plein d'avis sur le css
mais s'en bat la race en détail

daisy ui les gens aiment bien
(pk ?)
donc bon reprendre leur truc de primary et tout
avec du nesting c'est gucci

nesting

```css
.button {
  border-radius: 4px;
  background-color: #f0f0f0;
  color: #333;

  &.primary {
    background-color: #007bff;
    color: #fff;
  }
}
```
 
```css
.a {
  /* styles for element with class="a" */
  &.b {
    /* styles for element with class="a b" */
  }
}
```

---

essayer ce générateur
https://www.reddit.com/r/css/comments/1dqfkxt/ui_generator/

checklist
https://github.com/AllThingsSmitty/css-protips
is() est vraiment bien
intrinsic ratio... ouais ?

autre tricks
https://www.reddit.com/r/css/comments/1dw5sjq/css_wizards_gather_round/
gradient et shape-outside
tu combines avec des animations sur click et hover et t'es le roi du monde

sticky footer
https://developer.mozilla.org/en-US/docs/Web/CSS/Layout_cookbook/Sticky_footers
faut rien avoir à écrire, mais bon
avec simple css on l'a dans le uc à cause de sa grille bizarre
autre truc où il s'est pris les pieds
la grille en 3 pour centrer mais le header qui en prend trois
avec un min(90%, 45rem) bah... dégueu sur extra wide
nan... et avec minmax on s'en sortait ? ouais viteuf mais ouais

---

le site crash fort
surout penser file structure

un reset en root css
https://github.com/CodeStitchOfficial/Intermediate-Website-Kit-LESS/tree/main/src/assets/css
j'aurais séparé avec un main ou un utils
de la redite ?
pas giga clean mais bon
le taff est là

les deux js dont t'as besoin
dark mode et navbar
https://github.com/CodeStitchOfficial/Intermediate-Website-Kit-LESS/tree/main/src/assets/js
(mention spéciale accessibility)


page counter in css
https://herman.bearblog.dev/how-bear-does-analytics-with-css/

hehe ça c'est grave marrant
https://herman.bearblog.dev/the-frustration-loop/

sympa la journée
https://herman.bearblog.dev/quitting-social-media/

sympa ça aussi
https://sive.rs/
une /now page, une /ai page

chatbot sécu
https://botsy.org/
meta facture, environ 5 centimes le sms

ai help
https://developer.mozilla.org/en-US/plus/ai-help
5 questions par jour de gpt3 bah mercé


> The specification recommends not animating from and to auto.
un peu chiant en vrai mais azy
on va juste animer du changement de couleur, du gradient on a dit

carte
> d3.js ?
> api google, on capitalise sur jumelio

echecs poissons
> aller

gold.css
> aller

vc
> foncer
> faire semblant d'être gros
> se faire manger

legires.fr
> façon neal.fun
> avec gold, chess, map



mdrr ng openai
https://www.newgrounds.com/bbs/topic/1417630


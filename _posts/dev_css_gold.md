---
title: dev - css.gold
layout: post
---

on a fait le tour du cercle.
je ne suis plus un htmx absolutist.
je suis un 
[html absolutist](https://html-first.com/)

pas besoin de serveur ? ok


bliss est bien mais

[mini](https://mini-js.com/)
a aussi un each
(exemple avec desktop/phone)
donc juste a se taper les query selector

putain y'a même des keyboard events

permet de se libérer
variables css... berk

mais c'est lourd.
qui dev ça bordel ?

bon par honnetete
il faut que je comprenne
https://alpinejs.dev/
et que je compare

html: toujours le probleme des partials 
ici une solution: https://leanrada.com/htmz/
(c'est vraiment pas mal)
(à la place de htmx... hmm)
ah mais ouais c'est juste une fonction mdr
ah ouais bah bien
la blague npm mdrrrr
https://leanrada.com/notes/pure-css-spa-router/
bah voilà
ok lui est cracked
https://leanrada.com/
ok merde il est vraiment cracked
je veux tout comme lui
j'ai juste un doute sur la responsiveness des iframes

me faut un nom de hacker
100tral bof
j-net
g net
le.game €1,530.38


ici une solution: https://gomakethings.com/you-probably-dont-need-html-imports/
putain mais je veux juste les import de jinja merde

css: https://tailwind-lite.com/
pk pas mais bon
encore beaucoup de classes
https://turretcss.com/
plutôt sympa, center, circle
(enfin center https://build-your-own.org/blog/20240813_css_vertical_center/)
et circle fuck it
le découpage est nice
https://github.com/turretcss/turretcss/tree/master/turret
mais y'a tellement de trucs à faire misère
je comprends qu'il soit plus update depuis 3 ans
à garder en tête si je me lance dans gold...

https://gomakethings.com/bye-bye-build-steps/
(mouais bof)
https://gomakethings.com/the-goal-isnt-to-write-less-code/
oui ok mais je veux le $
ship juste ça merde
(vazy fais-le)
http://vanilla-js.com/
azy hein

```js
const $ = function(expr, context) {
    return (context || document).querySelector(expr);
};

const $$ = function(expr, context) {
    return Array.from((context || document).querySelectorAll(expr));
};
```

https://gomakethings.com/javascript-selector-performance/#:~:text=getElementById()%20can%20run%20about%2015%20million
aller nickel il dit que c'est bon

## cracked and crackeder

https://gomakethings.com/what-about-searching-flat-files/
oh ça c'est du lourd

## html is cheap

ship les deux layouts
j'aurais juste du garder phone

https://gomakethings.com/the-many-ways-to-hide-things-in-the-dom/
à creuser si j'ai mis le bon truc
le hidden attribute notamment

soit via css, 
(mais faut que js écrive le css sinon 13)
soit via js + class hidden

mais bon faudrait mieux juste du css

ship all.

## js is alright

plus un htmx absolutist.
garder htmx pour besoins serveurs.
philosophie jquery
mais bliss c'est bien jquery - ajax

## sinon

couleurs modulaires?

minmax fait des arrondis chelous
nouvelles grilles (et rename)

flex pas besoin

pretty-text carry

attributes c'est sympa
des trucs avec un id identique > horrible

## pas sur du un

flat is depth?

avec drop-shadow (trop bien pour svg)
et des bons z-index

> stop with the fucking buttons
the fucking borders and stuff
make art, svgs, fuckers


don't forget to poison the well
https://gomakethings.com/poisoning-the-ai-well/


huh ?
https://gomakethings.com/how-many-event-listeners-is-too-many-in-javascript/
écouter tout ?


### the crackedest

https://unplannedobsolescence.com/
c'est bien
j'aime bien les attributs
c'est en le browsant que j'ai trouvé
https://doesmyipaddresshave69init.com/
le go somewhere else me fait penser à l'ancien net
qui avait des "dead ends"
maintenant c'est un asile de fous circulaire

pour ça que c'est bien le micro blogging
mais sans micro

https://lofi.limo/blog/write-html-right
hmm ok

https://meyerweb.com/eric/thoughts/2023/11/01/blinded-by-the-light-dom/
bon les custom elements faudra s'y mettre

```js
class superSlider extends HTMLElement {
	connectedCallback() {
		let slider = this.querySelector('input[type="range"]');
        let slide $('input[type="range"]', this) ça marche ?
	}
}

customElements.define("super-slider",superSlider);
```

vérifier que crackboy utilise bien ça

et comme pour vanilla, bien relire
https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_custom_elements

et si c'est bon, on va faire un custom-element pour time
qui montre la durée de vie de css.gold
parce que je renew pas ce truc c'est trop cher

checker ça
https://jakearchibald.com/2024/attributes-vs-properties/

oulah, et ça
https://blog.carlana.net/post/2023/web-component-alternative-futures/

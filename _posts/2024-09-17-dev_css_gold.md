---
title: dev - css.gold
layout: post
---

j'ai fait des erreurs.

oh mon dieu.
beaucoup d'erreurs.
mais j'ai appris.

voyons.

## getting cracked

mon objectif est de faire tourner mes business sur un serveur.

je ne suis plus un htmx absolutist.
si une requête doit taper mon serveur,
je dois être sûr qu'elle est absolument nécessaire.

mais je suis devenu un 
[html absolutist](https://html-first.com/).
et prendre comme premier principe
le principe du moindre pouvoir
me paraît bien.

c'est pas si simple pour autant.

si on veut faire un dark mode en pure css,
il faut bien se servir des variables associées.
on a les
[couleurs relatives](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_colors/Relative_colors)
pour nous aider,
mais c'est un pli à prendre,
et pas forcément compatible partout.

mais pour une view mobile ?
css ou html ?
les layouts sont souvent si différents
qu'il est permis d'en douter.
et en pure html ça passe très bien...

```html
<body>
    <div id="desktop">
        ... desktop view ...
    </div>
    <div id="phone">
        ... phone view ...
    </div>
</body>
```

et une media-query du css qui 
[désactive](https://gomakethings.com/the-many-ways-to-hide-things-in-the-dom/) 
(qui passe en `display:none`)
l'un ou l'autre.[^1]

```css
#phone {
    display: none;
}
#desktop {
    display: block;
}

@media (max-width: 610px) {
    #phone {
      display: block;
    }
    #desktop {
      display: none;
    }
}
```

[^1]: je l'avais initialement fait avec du javascript, 
    mais c'était complétement con.

le souci c'est qu'on va vite écrire les choses deux fois.
le souci c'est qu'on va vite écrire les choses deux fois.[^2]

[^2]: [jinja](https://jinja.palletsprojects.com/en/3.1.x/)
    c'est la vie.
    je comprends pas pourquoi
    [on veut s'en passer](https://gomakethings.com/you-probably-dont-need-html-imports/),
    ni pourquoi html a lâché l'affaire.

pas foooooorcément un souci,
si on fait les choses bien.

```css
#desktop #menu {
    padding: 10%;
}

#phone #menu {
    padding: 20%;
}
```

moins feng shui,
mais c'est normal.
si tu veux un behaviour différent
sur mobile et desktop, faut le payer.

en js, c'est plus chiant :

```js
const phoneMenu = ("#phone" || document).querySelector("#menu")
```

ou utiliser
`querySelectorAll`,
mais ça renvoie une NodeList...
et on voit vite les limitations.

bon d'ailleurs, tant qu'on parle de ça.

```js
const $ = function(expr, context) {
    return (context || document).querySelector(expr);
};

const $$ = function(expr, context) {
    return Array.from((context || document).querySelectorAll(expr));
};
```

de rien, c'est maison c'est cadeau.[^3]

[^3]: j'avais l'habitude d'importer tout jquery pour avoir ce truc.
    puis tout [bliss.js](https://blissfuljs.com/).
    mais faut arrêter les conneries.
    **il faudrait un reset javascript**
    **comme on a des resets css.**
    et oui, on pourrait l'écrire différement, mais c'est
    [très bien comme ça.](https://gomakethings.com/javascript-selector-performance/#:~:text=getElementById()%20can%20run%20about%2015%20million)

## cracked and crackeder

j'ai lu pas mal de librairies
et j'ai douté de htmx.

j'ai découvert
[mini](https://mini-js.com/),
qui a un each,
qui a juste ce qui faut,
qui a même des keyboard events.

mais c'est lourd.
et pas moyen de trouver qui dev ça.

(je comprends toujours pas
ce que fait alpine ni comment ça compare
aux [vraies bonnes librairies](http://vanilla-js.com/))

enfin...
on l'a dit un bon stack, c'est du least power.

et ça passe par les variables css,
par les 
[data-attributes](https://jakearchibald.com/2024/attributes-vs-properties/) 
que je maîtrise un peu mieux,
et peut-être par les 
[custom elements](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_custom_elements)
même si je suis pas encore 
[100% convaincu.](https://blog.carlana.net/post/2023/web-component-alternative-futures/)
[^4]

[^4]: j'aime bien [ce style d'écriture](https://meyerweb.com/eric/thoughts/2023/11/01/blinded-by-the-light-dom/), cependant.

le css c'est dur.
[ça s'améliore](https://build-your-own.org/blog/20240813_css_vertical_center/)
mais c'est dur de penser hors tailwind.

il y a bien
[tailwind lite](https://tailwind-lite.com/)
mais c'est pas compatible avec daisyui et tout le reste.

il y a 
[turret.css](https://turretcss.com/),
qui présente 
[un très beau découpage](https://github.com/turretcss/turretcss/tree/master/turret),
mais il est plus update depuis 3 ans.
c'est tellement de boulot, je comprends.

à garder en tête pour gold...
(mais ça prend forme).

j'ai lu pas mal de blogs
et pleuré la mort du css.

on a vu gomakethings 
(qui a notamment la très bonne idée
de faire une
[text database](https://gomakethings.com/what-about-searching-flat-files/))
mais y'en d'autres.

j'ai découvert 
[lui](https://lofi.limo/blog/write-html-right),
avec du bon lo-fi en prime.

j'ai découvert
[unplanned obsolescence](https://unplannedobsolescence.com/)
et je suis d'accord avec tout.

et dedans j'ai trouvé
[un site à l'ancienne](https://doesmyipaddresshave69init.com/).
le "go somewhere else" me fait penser à l'ancien net,
qui avait couloirs qu'on suivait
jusqu'aux *"dead ends"*.
maintenant c'est un asile de fous circulaire.

il faut faire les choses à l'ancienne.
je pense que le principe du least power,
ça doit aussi vouloir dire
commencer par écrire le site en pure statique.

et htmx en touche finale.

### the crackedest

en continuant à creuser le sujet htmx,
je suis tombé sur
[htmz](https://leanrada.com/htmz/).

et faut dire que la documentation
fait rire.
la simplicité du truc,
la blague npm.
il y a de l'esprit.

et pour cause :
[le mec est giga cracked.](https://leanrada.com/)

non mais
[regardez ça](https://leanrada.com/notes/pure-css-spa-router/).
no js !

c'est là que j'ai réalisé qu'avant html > css > js,
il y a 
[url.](https://leanrada.com/notes/compressing-websites-into-urls/)

je veux tout comme lui.
il est vraiment cracked.

bref, htmz super idée.
j'ai juste un doute sur la rapidité des iframes.

## conclusion

j'ai repris goût à écrire du js,
[même s'il reste des subtilités.](https://gomakethings.com/how-many-event-listeners-is-too-many-in-javascript/)

j'ai bien avancé sur
gold.css,
même s'il faudrait réécrire du code,
et surtout réécrire le commandement un.

je me demande si ça serait pas mieux :
`flat is depth`.

en fait je commence à être fatigué,
fatigué de la gestion de la typographie,
fatigué des breakpoints arbitraires,
fatigué des boutons à la con,
des fuckings borders et des fucking arrondis.

de l'autre côté,
j'aime bien les filtres,
notamment drop-shadow,
qui combote bien avec z-index.

en gros, je veux que le css fasse la mise en forme,
**mais pas le design.**

le design, on le fait avec les illustrations, les svg.
si on veut passer le web d'un medium textuel à visuel,
on le fait vraiment.

ne jamais oublier : `the medium is the message`.

et c'est déjà pas mal.[^5]

---

[^5]: oui, j'ai mis des p'tites footnotes,
    sinon je m'en sortais pas ici.
    à voir si je garde.


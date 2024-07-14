---
title: dev - gold.css 2
layout: post
---

plan d'attaque

container mobile

bon, on a fait quelques modifs, et appris des trucs.

## gold.css v2

on a commencé par faire du
[layering](https://css-tricks.com/css-cascade-layers/)
de notre template.

j'aime beaucoup le concept,
ça donne de la hiérarchie
et ça rend le truc plus modulaire
et plus réutilisable.

on a fait :
- reset : bon, c'est mon reset mais 
[en fait y'en a plein](https://css-tricks.com/css-remedy/)
- default : espaces, typographies
- theme : couleurs, polices
- layouts : les golds trucs, les grilles, les flexboxes
- components : les éléments html
- utilities : les classes style "tailwind" comme "p-s"
- debug : stack au top pour debug

c'est bien.
et surtout pour que ça casse pas :
ne jamais utiliser `!important`.

ensuite on a mis du nesting,
ça ressemble à ça :

```css
.a {
  /* styles for element with class="a" */
  &.b {
    /* styles for element with class="a b" */
  }
}
```

pratique pour les gaps flexbox,
faire des trucs genre `primary`
à la daisy ui :

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

## css tricks

on a appris pas mal de choses,
notamment sur le site
[css tricks](https://css-tricks.com/).

dans les idées que j'aime bien :

conditionner une 
[variable](https://css-tricks.com/dry-switching-with-css-variables-the-difference-of-one-declaration/)
à une media query,
pour écrire du code plus logique,
plus joli,
plus simple.

les
[container queries](https://css-tricks.com/css-container-queries/)
plutôt que les media queries,
pour faire des composants réutilisables.
attention la syntaxe est un peu touchy :

```css
#hero-container {
    container: hero-container / inline-size;
}

@container hero-container (width < 377px) {
    #hero {
        width: 100%;
    }
}
```

ensuite, le design,
faut d'abord qu ce soit cohérent,
ensuite que ce soit joli.
et pour ça,
utiliser des 
[gradients](https://css-tricks.com/grainy-gradients/)
des transitions,
et des belles images, des beaux svg.


## conclusion

primo, css est un langage
[bien cassé](https://wiki.csswg.org/ideas/mistakes)
deuzio,
css est un langage
[bien puissant](https://herman.bearblog.dev/how-bear-does-analytics-with-css/).
c'est pas idéal mais faut faire avec.
faut être [créatif](https://herman.bearblog.dev/the-frustration-loop/).

tertio, y'a pas besoin de react.
dans 99% des cas,
le seul js dont t'as besoin,
c'est [dark mode et navbar](https://github.com/CodeStitchOfficial/Intermediate-Website-Kit-LESS/tree/main/src/assets/js).

maîtrise le css,
y'a plein de trucs à faire.
shape-outside,
plein de transitions,
sur les pseudo-sélecteurs
(hover, focused...),
avec de belles courbes de bézier,
les positions "sticky"...

maîtrise le.
cuisine
[tout le cookbook](https://developer.mozilla.org/en-US/docs/Web/CSS/Layout_cookbook),
connaît par coeur tes
[keywords](https://github.com/AllThingsSmitty/css-protips) (comme `is()`),
lis les blogs,
utilise 
[l'ia de mozilla](https://developer.mozilla.org/en-US/plus/ai-help)...

muscle ton jeu.

y'a qu'à voir les belles pages de 
[codestitch](https://codestitch.app/app)
garanti no js.

et pour finir :
ces articles ont été giga painful à écrire.
gold.css a été painful as well.

faut que tu fasses le taff toi-même,
learn by doing,
no shortcuts.

```css
dura css,
sed css.
```

à un de ces quatre.

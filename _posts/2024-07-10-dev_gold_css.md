---
title: dev - gold.css
layout: post
---

[english version here.](https://www.deepl.com/translator?share=generic#en/fr/there%20you%20go)

j'ai fait un template css pour pouvoir bootstrap mes futurs projets.
décortiquons ça ensemble :

- [modular design](#modular-design)
- [css reset](#css-reset)
- [simple stuff](#simple-stuff)
- [gold box](#gold-box)
- [gold grid](#gold-grid)
- [conclusion](#conclusion)

## modular design

*nb : je recommande de lire [cet article](/2024/06/25/dev_kicknews_3) avant de commencer.*

donc, au départ j'avais envie d'essayer
le concept d'échelles modulaires :
en gros, chaque espacement est une puissance d'un ratio.

en prenant comme ratio le nombre d'or,
comme le suggérait every-layout.dev
en blaguant à moitié,
on obtient ces mesures :

![phi.png](/img/dev/phi.png){:.ioda}

---

voici comment on a commencé 
à les implémenter :

```css
/* modular spaces */

:root {
  --phi: calc((1 + sqrt(5)) / 2);
  --m: 1rem; /* basis */
  --xxs: calc(var(--m) * pow(var(--phi), -3));
  --xs: calc(var(--m) * pow(var(--phi), -2));
  --s: calc(var(--m) * pow(var(--phi), -1));
  --l: calc(var(--m) * pow(var(--phi), 1));
  --xl: calc(var(--m) * pow(var(--phi), 2));
  --xxl: calc(var(--m) * pow(var(--phi), 3));
}
```

la syntaxe est inspirée du *atomic css*,
avec des noms de variables parlants.

---

on peut ensuite facilement écrire des *helper classes*
façon tailwinds, du genre :

```css
/* utility classes */

.p-s {
  /* small padding */
  padding: var(--s);
}

.m-l {
  /* large margin */
  margin: var(--l);
}
```

on est pas obligé de tout écrire,
[uno css](https://unocss.dev/guide/) 
peut très bien faire ça pour nous,
mais vous voyez l'idée.

de la même façon,
on fait la typographie :

```css
/* typography */

h1 {
  font-size: var(--xxl);
}
h2 {
  font-size: var(--xl);
}
h3 {
  font-size: var(--l);
}
h4, h5, h6, p {
  font-size: var(--m);
}
```

avant, j'allais tout le long de la power scale,
de h6 = 1rem à h1 = phi^5,
mais ça fait vraiment gros.

il faut penser bootstrap, sortir un truc raisonnable
et laisser le soin à l'utilisateur 
de s'amuser ensuite.

---

## css reset

là, bon,
pas grand chose à dire,
j'ai juste piqué le reset de josh comeau,
avec quelques modifs.

```css
/* josh comeau css reset */

*, *::before, *::after {
  box-sizing: border-box;
}

* {
  margin: 0;
}

body {
  -webkit-font-smoothing: antialiased;
}

img, picture, video, canvas, svg {
  display: block;
  max-width: 100%;
}

input, button, textarea, select {
  font: inherit;
}

p, h1, h2, h3, h4, h5, h6 {
  overflow-wrap: break-word;
}
```

si ton bootstrap n'offre pas un reset css,
c'est un mauvais bootstrap.

---

## simple stuff

ici j'ai piqué des idées à simple.css,
on va les détailler ensemble.

remarque : 
j'aurais pu en piquer à pico.css,
que j'utilisais avant,
mais j'avais pas le coeur à bouffer son code.
donc pensez à écrire les choses le plus simplement possible,
ça facilite le vol.

```css
/* simple.css ideas */

html {
  font-family: var(--sans-font);
  scroll-behavior: smooth;
}

body {
  color: var(--gold_0);
  background-color: var(--light);
}
```

oui alors il y a des petites variables de customisation
de couleur ça et là,
on les setup au début :

```css
/* colors */

:root {  
  --light: #E8EDDF;
  --dark: #333533;
  --gold_0: #C1A24E;
  --gold_1: #8D7840;
  --gold_2: #7a6220;
  --blue: #010C1E;
}
```

j'aime bien.
quelques variations sur une couleur,
une couleur complémentaire forte
(pour les trucs comme button-primary),
un noir et un blanc.

---

revenons à nos moutons :


```css
/* buttons and links */

a,
a:visited {
  color: var(--gold_1);
}

a:hover {
  text-decoration: none;
}

button,
.button,
a.button,
input {
  border: 1px solid var(--gold_0);
  background-color: var(--gold_0);
  color: var(--dark);
}

button:enabled:hover,
.button:not([aria-disabled="true"]):hover,
input[type="submit"]:enabled:hover,
input[type="reset"]:enabled:hover,
input[type="button"]:enabled:hover,
label[type="button"]:hover {
  color: var(--gold_0);
  background-color: var(--gold_1);
  border-color: var(--gold_1);
  cursor: pointer;
}

.button:focus-visible,
button:focus-visible:where(:enabled),
input:enabled:focus-visible:where(
  [type="submit"],
  [type="reset"],
  [type="button"]
  ) {
    outline: 1px solid var(--gold_1);
    outline-offset: 1px;
}

.button[aria-disabled="true"], 
input:disabled,
textarea:disabled,
select:disabled,
button[disabled] {
  cursor: not-allowed;
  background-color: var(--blue);
  border-color: var(--blue);
  color: var(--gold_2);
}
```

de quoi faire des jolis boutons,
des jolis inputs,
la base.

si on veut les arrondir,
le faire direct ou
créer une classe spécifique.
m'enfin c'est virtuel,
vous allez pas vous cogner la tête dessus.

---

continuons :

```css
/* simple.css ideas */

abbr[title] {
  cursor: help;
  text-decoration-line: underline;
  text-decoration-style: dotted;
}

table {
  border-collapse: collapse;
}

td,
th {
  border: 1px solid var(--gold_0);
  text-align: start;
  padding: var(--m);
}

th {
  background-color: var(--gold_2);
  font-weight: bold;
}

tr:nth-child(even) {
  background-color: var(--gold_1);
}

hr {
  border: none;
  height: 1px;
  background: var(--gold_2);
}

blockquote {
  padding-inline: var(--m);
  border-inline-start: var(--l) solid var(--m);
  font-style: italic;
}

code {
  font-family: var(--mono-font);
  color: var(--dark);
}

pre {
  white-space: pre-line;
}
```

bon ça c'est la base,
certaines choses devraient être par défaut,
la table par exemple, mais bref.

---

j'en profite enfin pour faire un détour
parmi les *utility classes* de every-layout :

```css
/* every-layout utilities */

.stack {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.stack-large > * + * {
  margin-block-start: var(--l);
}
.stack-medium > * + * {
  margin-block-start: var(--m);
}
.stack-small > * + * {
  margin-block-start: var(--s);
}
```

si j'ai beaucoup aimé le stack,
l'élégance du *owl operator*...
ça n'en reste pas moins une flexbox.
et au final, mieux vaut utiliser gap.

adieu donc, beau stack, c'était cool.

---

## gold box

on arrive dans le dur.

comment aller plus loin avec le nombre d'or,
avec la divine proportion ?

un truc très simple, c'est déjà ça :

```css
.gold-center {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.gold-center > * {
  width: 61.8%;
}
```

61.8%, c'est phi à la louche.

on peut stacker des choses comme ça,
et retrouver une proportion harmonieuse.
c'est notamment pratique pour un texte bien centré,
ça fait joli.

mais si on veut aller plus loin ?
si on veut deux éléments en proportions dorées,
l'un par rapport à l'autre ?
bien sûr on peut continuer d'utiliser des flexboxes.

ça a commencé comme ça :

```css
/* golden boxes */

.chain {
  display: flex;
  flex-direction: row;
  align-items: center;
  flex-wrap: wrap;
}

.gold_0 {
  flex: 1 1 144px;
}

.gold_1 {
  flex: 1.618 1.618 233px;
}
```

on prend une flexbox, ici *chain*,
on y met deux éléments, et on colle à chacun
la classe gold-0 (le petit bout)
ou gold-1 (le grand bout).

flex ici définit le flex-grow et le flex-shrink :
on s'assure ainsi que les deux éléments restent
dans les bonnes proportions...
pour peu qu'il y en ait pas un qui soit trop gros.

le pire, c'est écrire ce `144px`
magique alors que dans mes rêves,
c'est responsive même sur tamagotchi.

> ### golden break
> 
> je déteste écrire des valeurs magiques,
> mais bon en css on a pas toujours le choix.
> quelles valeurs choisir ?
> 
> vous vous en doutez,
> 123 et 199 sont des bons choix.
> mais pourquoi ?
>
> tout simplement parce qu'ils appartiennent
> à la [suite de fibonnaci](https://fr.wikipedia.org/wiki/Suite_de_Fibonacci)
> `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597`,
> qui a comme propriété que les quotients
> de deux de ses termes consécutifs
> sont la meilleure approximation du nombre d'or.
> par exemple, `233/144 = 1.61805...`.
> pas mal non ?
> 
> c'est aussi pratique pour définir des breakpoints,
> par exemple pour les inévitables *media queries*.
> on peut par exemple dire qu'un smartphone (ou breakpoint-small)
> est défini à 610px,
> qu'on partage en 233px et 377px.
> de même une tablette à 987px (377+610)
> ou un desktop (breakpoint-l) à 1597px (610+987).

on avait parfois un problème :
on avait souvent un gros truc dans une des boîtes
qui foutait tout en l'air.
le wrapping n'arrangeait rien.

```css
.gold-0 {
  flex: 1 auto;
  min-width: 0;
  min-height: 0;
  overflow: hidden;
}

.gold-1 {
  flex: var(--phi) auto;
  min-width: 0;
  min-height: 0;
  overflow: hidden;
}
```

on a été obligé d'utiliser
[overflow: hidden](https://stackoverflow.com/questions/36247140/why-dont-flex-items-shrink-past-content-size)
mais ça amène d'autres problèmes...
utiliser flex pour avoir un ratio précis n'est pas
forcément une bonne idée.

(est-ce qu'on a fait tout ça pour rien ?
peut-être. à voir si on a envie de coller ces classes
sur quoi que ce soit.
[une sidebar](https://every-layout.dev/layouts/sidebar/)
peut-être ?)

pouvons-nous faire mieux ?

---

## gold grid

déjà on avait un souci,
on mettait une classe
sur le container,
et pas sur les éléments à l'interieur.

alors j'ai essayé de faire la même boîte au format grid.

ça donne ça :

```css
/* golden grids */

.grid-01 {
  display: grid;
  grid-template-columns: 1fr var(--phi)fr;
}

.grid-01 {
  display: grid;
  grid-template-columns: var(--phi)fr 1fr;
}
```

on remarquera ici le joli usage de l'unité fr,
pour *fraction*,
qui semblait destiné à cet usage.

on a toujours le problème des gros trucs qui débordent,
(car `1fr = minmax(auto, 1fr)`),
on se chauffe un peu à lire la doc de grid
et on obtient ça :

```css
.grid-01 {
  display: grid;
  grid-template-columns: minmax(144px, 1fr) minmax(233px, var(--phi)fr);
}
```

dans la pratique, c'est pas mal du tout,
c'est robuste,
faut juste écrire les deux autres en vertical
avec `grid-template-rows`
(laissé en exercice au lecteur).

> ### implicite vs explicite
>
> on aurait aussi pu écrire
> `grid-auto-columns: 1fr var(--phi)fr`
> pour avoir une grille 'implicite',
> c'est-à-dire qui wrap si son contenu est trop gros.
>
> en principe, en css,
> 'implicit is better than explicit',
> à l'inverse de python.
>
> mais je me suis tellement cassé le crâne
> avec le wrapping des flexbox
> que je veux garder grid
> pour les use case explicites.

ça demande encore du testing,
mais bon,
ça fait le café pour l'instant.

---

## conclusion

eh beh voilà.

vous pouvez aller voir 
[tout ça](https://gold-css.onrender.com)
en action dès maintenant.

en bonus,
quelques autres trucs 
où j'ai une opinion :

```css
article {
  border: 1px solid var(--dark);
  border-radius: var(--m);
  overflow: hidden;
}
```

article qui donne juste une belle bordure,
qui cache ce qui dépasse.
sorte de "cadre".
ensuite on met de qu'on veut dedans.

```css
.w-100 {
  width: 100%;
}

.h-100 {
  height: 100%;
}
```

pas sûr que ce soit la meilleure façon de l'écrire,
mais c'est des classes pratiques.

dans le prochain chapitre,
on va déposer tout ce qu'on a chaluté
de connaissances en essayant de
faire ce qu'on a fait.

stay tuned.

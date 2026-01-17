---
title: dev - legires.fr
layout: post
---

j'avais un domaine de libre, j'ai voulu faire un truc.

bon, c'est pas une vraie raison.
on peut très bien faire un millier de sous-domaines,
tout héberger sur github pages.
vive les records cname.

(observation qui sera utile plus tard,
pour le projet navblog).

non, la vraie raison,
c'est que je voulais copier le site de
[neal.fun](https://neal.fun/).

il est cool,
il fait des jeux sympas,
il a un beau portfolio minimaliste.

bon,
[forcément](/autre/poesies/forcement.md),
j'ai fait un gros caca hideux.

mais j'ai appris des trucs.

---

## svg

j'expérimente avec les svg.
la
[génération ia](https://svg.io/)
est pas mal.

première leçon,
je n'ai rien pour les éditer correctement.
par exemple, j'ai fini par me rendre compte
que je galérais parce que les chemins traçaient
le blanc au lieu du noir.

deuxième leçon, 
s'en servir en background c'est pas terrible.
ou alors juste un peu en haut.
ou en contour ou en surimpression,
pour faire des jolis effets.

mais en background non, horrible,
parce que j'ai dû l'étirer dans tous les sens.
étirer pour ordi, étirer pour téléphone,
couper ce qui dépasse...

et c'est là que j'ai capté :
**faut étirer ce qui est étirable**.

ça aura son importance pour la suite.

---

## css layers

deuxième fuck up : le layering css.

je pensais, en écrivant
[gold.css](/_posts/2024-07-14-dev_gold_css_2.md),
qu'en découpant en layers,
les gens allaient pouvoir importer
uniquement les couches qu'ils voulaient.

que nenni.

tout s'importe.
faut juste être bien atomique,
et faire des couches de couches de couches...

donc bon,
j'ai dû repasser sur gold.css,
tout réécrire,
regarder ce que je voulais garder...

conclusion ?
la golden grid,
**c'est quand même pas mal.**

---

## gold

du coup,
comme disent les jeunes,
j'ai eu l'idée.

le thème du thème (lol),
c'est le nombre d'or ?
étale-toi sur l'écran et fais une spirale.

voilà.
pas plus compliqué.
mais fallait y penser.

et voilà qui est fait :
[css.gold](https://css.gold),

j'en suis très fier.

---

## conclusion

mais au fait,
ton site pourri il est où ?
ici, 
[allez voir](https://legires.fr/).

pour gold.css,
j'aimerais bien faire de la typographie fluide.
mais pour ça, il faut que je sois plus chaud
sur les container queries.

heureusement, j'ai trouvé un
[nouveau blog cool](https://moderncss.dev)
à poncer.

j'ai aussi pas mal expérimenté les variables conditionnelles,
c'était cool.
mais pour le dark theme,
mieux vaudrait apprendre à se servir de
`color-scheme`.

et puis j'ai eu l'idée de faire une échelle modulaire
pour le temps.

ça aussi c'est bien goldé.

allez peace.

---
title: dev - kicknews 4
layout: post
---

récemment j'ai écrit cette horreur :

```js
// omg du js ?!
$.ready().then(function(){
    var copy_button = $("#copy_button");
    copy_button.addEventListener("click", function(event) {
        var ts = $$(".refs").map(function(element){
            return element.textContent
            });
            // et htmx alors ?!
            navigator.clipboard.writeText(ts.join('\n'));
            copy_button._.set(
                {
                    style: {backgroundColor : "green"},
                    textContent: "Copied!"
                }
            );
            // mais c'est de la merde ?
            setTimeout(function() {
                copy_button._.set({
                    style: {backgroundColor : "", transition: "background-color 1s ease-in"},
                    textContent: "Copy refs"
                });
            }, 3000);
        });
});
```

que ? quoi ? feur ? $ ?
nous allons voir en détail :

- [ce que doit faire js](#the-right-tool-for-the-right-job)
- [ce que peut faire htmx](#feignant-et-névrosé)
- [ce qu'il reste à faire](#the-juice)

## the right tool for the right job

ça a commencé en lisant un horrible 
[thread 4chan](https://boards.4chan.org/g/thread/101127646).

oui alors je vous arrête tout de suite.
4chan est le dernier site "lisible".
je suis de la génération forum,
vos réseaux sociaux de merde ont plus de 
[bulles](https://fr.wikipedia.org/wiki/Bulle_de_filtres)
qu'un pétomane sous dom pérignon.

d'ailleurs vous avez vu,
c'est alambiqué ici.
le site est bien rangé,
mais dans les posts c'est l'anarchie.

la preuve c'est que j'ai toujours pas parlé du fond du sujet :
js n'est pas le mal.

react oui, c'est satan iv, aucun doute.
mais il y a des choses que htmx **ne peut pas** faire.

notamment sur l'exemple ci-dessus :
si le client veut pouvoir cliquer sur un bouton pour copier un truc dans son presse-papier,
il va falloir sortir js. 

pas le choix.
mais pour autant, et quitte à en écrire,
voici un tip : 
utiliser 
[bliss.js](https://blissfuljs.com/).

(ps : bon faites attention, il y a eu une 
[supply chain attack](https://news.ycombinator.com/item?id=40791829)
sur polyfill.
donc rappel : importez de manière responsable svp).

ça reprend la syntaxe de jquery,
sans les requêtes ajax dont vous n'aurez pas besoin
de toute façon puisque htmx.

ça fournit quelques fonctions utiles
(pas besoin d'underscore.js a priori),
et surtout, c'est suffisamment limité pour que
vous n'utilisiez js que pour le cas suivant :
*je trouve un élément et je lui attache une fonction basique.*
c'est tout. 

on sélectionne un élément avec $.
plusieurs éléments avec $$.
on a des méthodes sur les objets qu'on récupère.
le tout est joli sans trop en faire.

bliss.

## feignant et névrosé

le code en exemple a deux erreurs.
voyons la première.

je me définis comme un feignant névrosé :
je ne refuse pas l'effort par principe,
mais parce qu'il risque de me tuer.

> staive... et donc ?

et donc il faut regarder où l'effort est incompressible,
pour y concentrer ses forces.

dans mon modèle, 
le server est la *source of truth*,
mais aussi la *source of work*.

vous ajoutez à ça que souvent dans les apps htmx,
le réseau est le principal *bottleneck*,
et vous déduisez vite la règle d'or : **précalculer**.

on l'a vu : js ne doit rajouter que l'interactivité,
et encore par petites touches.
sur mon code, il crée une variable :
méfiez-vous, c'est bien un red flag.
eh oui.
la loi est dure, mais c'est la loi.

qu'aurait-il fallu faire ?
tout simplement : 
- précompute la liste des refs
(si elles sont apparues dans le dom, c'est qu'htmx les a vu),
- mettre ça dans un div hidden au bon format, 
- puis aller le chercher par id avec js pour copier dans le presse-papier.

on s'épargnait le `var ts` qui donne envie de se pendre,
et le join affreux.

une fois de plus : dura lex.
mais c'est pour votre bien.

bien sûr,
il faut être très musclé sur le
[event driven](https://htmx.org/examples/update-other-content/#events)
pour pouvoir faire beaucoup de features,
ainsi que sur le
[preload](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/preload/README.md)
pour perf à donf.

pour finir, comme j'ai parlé de htmx :
allez voir
[mavo.io](https://mavo.io/).
c'est la même idée que htmx avec une approche différente.

ça a été fait par la créatrice de bliss, 
[léa verou](https://lea.verou.me/blog/).
son blog est très bien.

## the juice

mais au fait...
pourquoi on se fait autant chier ?

après tout, l'important c'est de ship,
on pourrait juste go
[webflow](https://webflow.com/)
et roule simone.

effectivement,
l'important c'est la portée,
et c'est bien à cause de ça qu'on a la
[loi d'artwood](https://blog.codinghorror.com/all-programming-is-web-programming/)
contre laquelle il faut lutter.

mais le vrai plus important,
c'est le 
[juice.](https://www.youtube.com/watch?v=Fy0aCDmgnxg)

regardez
[eieio](https://eieio.games/) :
il en fout du juice !
et il le fait surtout avec du css.

voilà où je voulais en venir :
si on fait tout le compute et toute la logique
sur le serveur en python,
qu'on garde qu'en cas d'absolue nécessité,
il faut **juice avec css**.

c'est mon gros sujet de réflexion du moment, en gros :

- ne pas utiliser view transitions, c'est trop complexe et pas assez mûr.
- au contraire, bourrer la [transition](https://htmx.org/examples/animations). multiplier les classes et les états, du success, du hover, du disable on y va.
- oui les classes... en vrai de vrai,
j'aime pas trop la contrainte de garder l'id stable d'htmx,
[cf itcss](https://developer.helpscout.com/seed/glossary/itcss/)
mais je vois pas comment faire autrement.

regarde ! tu peux même faire 
[bouger une balle](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_transitions/Using_CSS_transitions#using_transitions_to_make_javascript_functionality_smooth)
avec un tout petit peu de js.

ce qui est intéressant,
c'est comment ça change la réflexion.

est-ce que par exemple en utilisant 
[hx-trigger](https://htmx.org/attributes/hx-trigger/)
sur intersect et des gros blocs plein de transitions,
on peut pas avoir un 
[joli truc à scroll down](https://neal.fun/universe-forecast/) 
qui bouge et tout ?
sûrement mais faut preload à mort, comme on a dit.

et faut du café.
on a encore beaucoup de tests à faire.

et pour pousser css à fond, va falloir
[bien réfléchir](https://mrmrs.cc/writing/scalable-css/).

dev - kicknews s'arrête donc,
on va parler css maintenant.

la suite... au prochain épisode.

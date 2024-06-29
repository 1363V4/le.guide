---
title: dev - kicknews 4
---


bliss js
supply chain attack sur polyfill
pas trop de maj

```js
$.ready().then(function(){
    var copy_button = $("#copy_button");
    copy_button.addEventListener("click", function(event) {
            var ts = $$(".threat_ref").map(function(element){
                return element.textContent
            });
            navigator.clipboard.writeText(ts.join('\n'));
            copy_button._.set(
                {
                    style: {backgroundColor : "green"},
                    textContent: "Copied!"
                }
            );
            setTimeout(function() {
                copy_button._.set({
                    style: {backgroundColor : "", transition: "background-color 1s ease-in"},
                    textContent: "Copy refs"
                });
            }, 3000);
        });
});
```

j'aurais juste du faire un shadow dom
mettre ça dans un div hidden, aller le chercher avec un id
en tt cas fallait copier dans le presse papier
htmx peut pas

la transition pas nécessaire, j'aurais dû faire du css transi
https://htmx.org/examples/animations
mais j'aime pas le fait de garder l'id stable
inverted triangle css (itcss)
view transitions c'est dégueulasse
je préfère css transitions sur des hover des trucs comme ça
tu peux même faire bouger une balle eh
https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_transitions/Using_CSS_transitions#using_transitions_to_make_javascript_functionality_smooth
avec un tout petit peu de js

gros thread 4chan
https://boards.4chan.org/g/thread/101127646
js n'est pas le mal
mais react oui
en gros ne pas oublier que network is the bottleneck

https://eieio.games/
faut faire du js
et surtout mettre du juice !
il met du juice de fou avec du css lui

js less shitty
jquery pas si mal mais bon ajax fait par htmx
https://blissfuljs.com/
une belle syntaxe shorthand
des methodes sur les objets
je comprends pas pk elle dit de garder addEventListener
si on met qu'un event alors que set c'est le feu
https://blissfuljs.com/docs#fn-set

underscore js
utile ?
le fp... je préfère sur serveur merci

en vrai l'important c'est de ship
wp est vraiment trop moche mais une startup ?
go https://webflow.com/ comme tengo

## htmx

similaire à https://mavo.io/
de la créatrice de bliss, léa verou

event driven
https://htmx.org/examples/update-other-content/#events
faut consulter le hx-trigger du header okok
mais j'ai pas compris le bubble up

est-ce que par exemple en utilisant hx-trigger
https://htmx.org/attributes/hx-trigger/
sur intersect et des gros blocs avec transition
on peut pas avoir un joli truc à scroll down qui bouge et tout ?
sûrement

ou par exemple, pour retaper le jeu des villes jumelles en naviguant dans un graphe bien ?

ça il faut que je test
https://htmx.org/attributes/hx-prompt/

et hx-include dans tout ça ?
>Eg some time ago I made an online editor for a niche language so I would need to fit there entire code, input buffer, logs of all previous runs, audio/image outputs it generated, settings for all the key binds and other options available. Plus the state of glyph drawer and also serialized entire internal state of the REPL, if I were to finish that feature.
This can all be trivially fixed with hx-include, especially since I doubt you need all these things for every single call. Even if you did, rendering an hx-include next to every hx-post is still much easier than using javascript.

It also sounds like your website doesn't have serverside state at all, in which case it doesn't really matter if you do everything client side anyway.

I have an LLM frontend I manage with HTMX, and I need to do calls to the server which may take a long time. For this I HAVE to use custom javascript, since HTMX doesn't support request canceling, and this is totally fine. I use javascript for this, and then I use HTMX to manage most of the state, such as settings, prompt blocks, logs and history, etc. etc. HTMX allows me to do this with 0 friction, unlike react, which 100% dictates how my shit should be written.

ça a l'air puissant quand même
mais le doc montre pas bien

ce qui est intéressant
c'est effectivement comment ça change la réflexion
transitions tout le graphique c'est css
call server pour source of truth
petits ajusts js

encore beaucoup de tests à faire

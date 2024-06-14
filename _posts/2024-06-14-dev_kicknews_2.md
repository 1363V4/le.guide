---
title: dev - kicknews 2
layout: post
---

kicknews n'est qu'un étape vers le projet final.

j'ai fait un nombre ridicules de sites en chemin,
pour à chaque fois apprendre à maîtriser une nouvelle tech :

- 1363v4
    - apprendre venv
    - apprendre flask
- n0sq
    - apprendre render
    - apprendre le css
    - apprendre jinja2
    - apprendre tailwind
- revanche
    - apprendre le routage dns et le dynamic dns
    - apprendre le tls
    - apprendre les sous-domaines
    - apprendre les serveurs web
- legires
    - apprendre htmx
    - apprendre htmlgenerator
    - apprendre pythonanywhere
    - apprendre git
- kicknews
    - apprendre htpy

j'ai appris un peu plus que htpy.

---

j'ai appris les hx-indicators.
c'est un peu le cul parce que ça collapse pas
même en opacité 0.
pas trouvé la solution.
pas génant en l'état car petit.

j'ai appris que les divs clickables,
c'était un peu le cul aussi.
trop dur de chopper la value.
on est tellement mieux avec un *button*.

j'ai appris à faire du oob-swap.
je n'ai lu [cet article](https://htmx.org/examples/update-other-content/)
qu'après :
j'aurais dû faire 1,
au moins je comprends 2,
je suis chaud d'essayer 3.
prochain projet.

---

j'ai appris [exa](https://exa.ai/search).

j'ai fait mes tests en faisant des vrais calls api.
au final j'ai pas grillé mes requêtes gratuites,
mais j'ai quand même mis des garde-fous :

- un max request
    - facile à bypass en resettant la session, mais bon ça stoppe l'utilisateur moyen
    - mettre en database les requêtes
        - j'ai eu l'idée après avoir mis des bulles exemples
        - 80% des visiteurs vont cliquer dessus, merci pareto

ça reste facile à hacker.
on peut facilement me faire exploser la db.
ou la facture exa.

sans compter les erreurs de logique dans mon code.
typiquement, je regardais si la requête était en db,
mais seulement après l'avoir executée quand même. 
débile.

pas de vulns xss a priori mais j'en mettrais pas ma main à couper.

bref la cyber a 
[de beaux jours](https://medium.com/message/everything-is-broken-81e5f33a24e1) 
devant elle...

---

j'ai appris peewee.

c'est compliqué les subtilités des db.
je suis allé au plus simple,
j'espère que ça va tenir.

j'ai appris que render utilisait
des fichiers éphémères.
qu'on pouvait utiliser une db postgre
(bien sûr, après avoir setup sqlite),
mais qu'elle expirait en 30 jours.

et après 30 jours on fait quoi ?

> j'y penserai demain

m'en suis sorti mais bon.
sacré paquet de noeuds.
un vrai sujet à considérer.

---

j'ai pas appris le threading.
je sais bien que la limitation de flask,
c'est qu'il gère pas l'async.
me sens pas encore prêt.
ça viendra.

j'ai installé des extensions finalement utiles pour cursor.
rainbow tabs, sqlite viewer.

j'ai ramble sur x.

---

et j'ai ship.

fait. avance.

trouve des points étapes.
ici, c'était mieux comprendre exa,
intégrer leur api,
préparer mon call avec leur founder (merci à lui).

c'est un peu du louvoyage.
la vie c'est un vent de face.
avance.

rêve, crois, mais fait. 

[avance](https://www.youtube.com/watch?v=khPC2iOsgJI).

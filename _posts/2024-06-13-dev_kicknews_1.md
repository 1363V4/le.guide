---
title: dev - kicknews 1
layout: post
---

j'ai un projet en tête.

je vais devoir faire :

- le backend
- la base de données
- les cronjobs
- le design
- la facturation
- le frontend
- l'hébergement
- le login
- le marketing
- la sécurité

rien de bien fou.

---

je vais utiliser la stack suivante (? quand je suis pas sûr) :

- flask
- peewee
- cron du serveur
- uno css ?
- stripe / lemon squeezy ?
- htpy + htmx
- render ?
- flask-login
- twitter ?
- flask-security

---

pour la stack technique, j'ai choisi en fonction de deux principes :

1. le code doit être beau
2. je dois comprendre ce que je fais

htmx et htpy remplissent bien le 1 et le 2. 
je trouve js dégueulasse.

l'avantage c'est que je me retrouve avec la structure de fichiers suivante :

- static
    - css
        - un template minimal de bootstrap (pico css, simple css...)
        - un custom.css
    - fonts
    - img
    - svg
    - js
        - juste htmx
    - svg
- app.py
    - le logique de routage
- components.py
    - fabriquer le html
- models.py
    - les modèles de la base de données
- utils.py
    - "business logic", calculs, insertions db etc

l'avantage donc,
c'est que je peux commencer un projet avec les 4 fichiers .py,
et ensuite "ranger" sur le tableau blanc
les choses dont je vais avoir besoin.

> app, components, models, utils

en gros, c'est mon template de documentation d'architecture technique (dat).

---

et voilà, c'est fait :

[kicknews.tech](kicknews.tech)

la suite au prochain épisode.

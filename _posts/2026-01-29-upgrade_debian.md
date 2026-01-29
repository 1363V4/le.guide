---
title: upgrade debian
layout: post
---

bon, faut upgrade debian de 12 à 13.

ce qui veut dire tout wipe.

prévoyons.

## enfermé dehors ?

j'ai surtout peur que ça m'écrase mes settings ssh.

enfin bon, j'ai
[déjà documenté](https://blog.legires.fr/2024/12/11/monter_serveur.html)
mon setup s'il faut refaire des clés.

et 
[bread](https://www.youtube.com/watch?v=WwGRGfLy6q8)
a une très bonne vidéo ssh si besoin.

ma config en gros :

```bash
PermitRootLogin no
AllowUsers le
Port XXX
PubkeyAuthentication yes
AuthenticationMethods publickey
PasswordAuthentication no
```

## sauvegardes

j'ai zippé mes sites et ils sont sur github.
comme je veux rewrite je m'en fous un peu.

## dot files ?

non, je sais pas encore m'en servir.

je vais devoir remettre les trucs dont je me sers :

- oh my posh
- [micro](https://blog.legires.fr/2025/10/24/micro_config.html)
- htop

pour oh my posh, penser à rajouter dans .bashrc :

```bash
#ohmyposh
export PATH=$PATH:/home/le/.local/bin
eval "$(oh-my-posh init bash)"
```

## alias

tant qu'on est dedans...
j'en utilise que deux :

```bash
alias update='sudo apt update && sudo apt upgrade -y'
alias gitup='git add . && git commit -m "dev" && git push'
```

et aussi uncomment `la`.

## un peu d'aide ?

oui je veux bien.

je vais redonner une chance à vibe by mistral.
petit assistant serveur.

```markdown
You are an agent helping the maintainer of a Debian server. 
The purpose of this server is to host Python apps.

Always plan first. No yapping.
Prefer lists and markdown formatting.

If you propose code: no comments, no classes.
Code should be simple, straightforward and secure.
```

## firewall

simple :

```
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
80/tcp                     ALLOW       Anywhere
XXX/tcp                   ALLOW       Anywhere
443/tcp                    ALLOW       Anywhere
25/tcp                     ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
80/tcp (v6)                ALLOW       Anywhere (v6)
XXX/tcp (v6)              ALLOW       Anywhere (v6)
443/tcp (v6)               ALLOW       Anywhere (v6)
25/tcp (v6)                ALLOW       Anywhere (v6)
```

je crois que j'ai ouvert le 25 pour recevoir des mails mais je peux drop ça.

## quelle stack ?

python déjà.

`uv python install 3.14 --force`

ensuite sanic j'aime vraiment bien.
on garde mais faut faire des blueprints.

ensuite pour la database il est l'heure d'être un grand garçon.
on va passer sur le combo sqlite + peewee + harlequin.

et un autre grand saut dans l'inconnu mais bon :
on va ditch redis et passer sur nats.

le dernier point épineux c'est la génération html.
j'aime bien htpy mais bon...
en main ?? et puis la gueule du rewrite.

## caddy

bah ça va être vachement plus simple.

```
(app_config) {
    header {
        X-Content-Type-Options nosniff
        X-Frame-Options SAMEORIGIN
        X-XSS-Protection "1; mode=block"
        Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"
        Referrer-Policy strict-origin-when-cross-origin
        Permissions-Policy "camera=(), microphone=(), geolocation=(), interest-cohort=()"
        -Server
    }

    @static path *.jpg *.jpeg *.png *.gif *.ico *.css *.js *.woff *.woff2 *.opus *.mp4 *.webp *.svg
    header @static Cache-Control "public, max-age=2592000, immutable"

    encode
}

leg.ovh, www.leg.ovh {
    reverse_proxy unix/home/le/legovh/legovh.sock
    import app_config
}
```

je crois qu'on peut l'améliorer un peu mais c'est déjà très bien.

## déployer

quand je faisais quart, j'avais :

```bash
[Unit]
Description=Hypercorn instance to serve 10schat
After=network.target

[Service]
User=le
Group=www-data
WorkingDirectory=/home/le/10schat
ExecStart=/home/le/10schat/.venv/bin/python -m hypercorn -c hypercorn.conf app:app

[Install]
WantedBy=multi-user.target
```

mais c'est encore plus simple avec sanic qui porte la config :

```bash
[Unit]
Description=Sanic instance to serve draft
After=network.target

[Service]
User=le
Group=www-data
WorkingDirectory=/home/le/draft
ExecStart=/home/le/.local/bin/uv run app.py

[Install]
WantedBy=multi-user.target
```

pas d'overhead à utiliser uv.
enable, start et roule ma poule.

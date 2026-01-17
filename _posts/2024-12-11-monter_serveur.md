---
title: monter un serveur
layout: post
---

en ce moment je fais des sites.

comment ? je vais chez monsieur ovh,
j'achète un vps (un serveur avec une adresse ip),
un nom de domaine
(je rajoute deux **a records**, www et apex, vers le vps, puis j'enlève les autres)
et puis je configure le serveur.

je fais ça comme ça :

## premiers pas

on se log :

```bash
ssh debian@your_server_ip
```

et on fait un compte :

```bash
sudo apt update && sudo apt upgrade -y
sudo adduser yourusername
sudo usermod -aG sudo yourusername
```

## sécurité

sécurité simple et rapide,
seul notre ordi pourra se connecter au vps :

```bash
sudo nano /etc/ssh/sshd_config
```

et on écrit :

```
PermitRootLogin no
PasswordAuthentication no
AllowUsers yourusername
PubkeyAuthentication yes
AuthenticationMethods publickey
Port XXX
```

puis, en local :

```bash
ssh-keygen -t ed25519
```

pour créer une clé, qu'on copie :

```bash
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh debian@your_server_ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

attention, sur le dossier .ssh du nouvel user, pas sur debian !

on donne les droits :

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

puis, en local, sur le fichier config

```bash
Host nomdusite
  HostName IP
  User yourusername
  Port XXX
  IdentityFile C:\Users\username\.ssh\id_ed25519
```

ensuite tu pourras "ssh nomdusite" tranquillement.

## firewall

petit firewall :

```bash
sudo apt install ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw allow your_custom_port/tcp #ssh
sudo ufw allow 80/tcp   # HTTP
sudo ufw allow 443/tcp  # HTTPS
sudo ufw allow 'Nginx Full'
sudo ufw enable
```

## nginx

on va faire le server web avec nginx et la wsgi avec gunicorn :

```bash
sudo apt install python3 python3-pip python3-venv nginx
sudo nano /etc/nginx/sites-available/myflaskapp
```

la config :

```nginx
server {
    listen 80;
    server_name domainname.com www.domainname.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    server_name domainname.com www.domainname.com;

    ssl_certificate /etc/letsencrypt/live/domainname.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/domainname.com/privkey.pem;

    location / {
        proxy_pass http://unix:/home/username/domainname/domainname.sock:/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## certbot

on va demander notre cadenas :

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
sudo systemctl status certbot.timer
sudo nginx -t
sudo systemctl restart nginx
```

## gunicorn

```bash
sudo apt install python3 python3-pip python3-venv nginx
sudo nano /etc/systemd/system/myflaskapp.service
```

on écrit le service :

```
[Unit]
Description=Gunicorn instance to serve yourwebsite
After=network.target

[Service]
User=username
Group=www-data
WorkingDirectory=/home/username/app
Environment="PATH=/home/username/app/venv/bin"
ExecStart=/home/username/app/venv/bin/gunicorn \
    --config /home/username/app/conf/gunicorn_config.py \
    app:app

[Install]
WantedBy=multi-user.target
```

puis dans ton dossier dédié dans le dossier user :

```bash
python3 -m venv venv
source venv/bin/activate
pip install flask gunicorn
```

on écrit la config gunicorn :

```python
loglevel = "info"
errorlog = "/home/username/app/log/error.log"
accesslog = "/home/username/app/log/access.log"
bind = "unix:/home/username/app/app.sock"
workers = 3
user = username
group = "www-data"
timeout = 120
```

et on lance le service :

```bash
sudo systemctl start myflaskapp
sudo systemctl enable myflaskapp
```

## attention aux droits

je me suis fait avoir, www-data doit avoir les droits sur le folder de l'app :

```bash
sudo chmod 710 /home/username
```

et on relance tout :

```bash
sudo systemctl restart nginx
sudo systemctl restart service
```

voilà, normalement ça marche.

ensuite go écrire une app.

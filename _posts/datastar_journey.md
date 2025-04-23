---
title: a datastar journey
layout: post
---

journey as he said

inspired by game dev so why the fuck not

turbo seems bad finally
and webviews wrappers won't make the cut to the app store
allegedly

think ahead
https://data-star.dev/guide/stop_overcomplicating_it

i fuck with "regex and some glue code"

web components
https://lit.dev/docs/
for the chessboard ?
https://data-star.dev/examples/web_component

write a flask wrapper
https://github.com/starfederation/datastar/blob/main/sdk/python/src/datastar_py/responses.py
i don't see why gunicorn wouldn't work
sinon :
https://flask.palletsprojects.com/en/stable/deploying/gunicorn/
https://www.gevent.org/
https://docs.python.org/3/library/asyncio-task.html#coroutine
tell flask it is behind a proxy
https://flask.palletsprojects.com/en/stable/deploying/proxy_fix/

risque de sécurité de clean mon log des polling, comically bad

bon la partie alpine c'est facile

depth first evaluation c'est pas clair dans les examples

j'ai voulu refaire le sdk mais bof...
ceci dit, il bouge

attention c'est pas parce qu'il y a disable
sur un bouton que ça s'enlève pas
sécurité sécurité
le plan :
1 comprendre en gros la syntaxe
2 comprendre la philo
3 se plaindre
> des exemples
> de la sécu
4 rejoindre le culte
5 profit

what is the web ?
a bunch of servers containing changing hypermedia documents
> what is hypermedia? (media with instructions and links)
+ your browser (hypermedia navigator)
what is the problem? changing and links
should you use datastar?
no, htmx is fine, because async is hard to do
but if you do big compute or async for real, then yes

un peu absolutiste
genre je veux faire un form normal avec un redirect
pas possible depuis le serveur
enfin si mais bon... soit je me passe de data-indicator
soit je me passe du redirect serveur...
je comprends pas encore trop la sse way
et j'ai toujours pas les updates sur join...
je m'y prends mal je pense

ok après une nuit de sommeil on relance
je vais déjà optimiser le first print
puis un bouton qui initie le sse et envoie le reste
déjà un problème: pourquoi fermer la connexion

garder la connexion ouverte c'est le vrai enjeu
et je m'y prends mal, mon while true envoie beaucoup trop de données
dois-je pub/sub ?
très satisfaisant pourtant d'éliminer une entrée dans la db et la voir disparaitre en live...

bon, je m'y prends mal encore, l'idée est là mais je dois mieux comprendre la connexion
si je fais juste on-signals-change > endpoint, ça en spawn trop

vise la lune et atterris dans les étoiles 
je demandais des trucs impossibles
voir la db se modifier depuis l'orid sans faire de polling ? impossible
faire de la communication double sens, pareil,
dans le sens de récupérer ses signaux à tout moment
(et pourquoi faire ? pourquoi s'entêter dans cette single lasting connection)
parce que ça, c'est les étoiles, aujourd'hui je l'aurais
mais il va falloir mettre un cookie ?

réduire les endpoints, balancer big chunks of state
faut se le mettre dans la boule

ok donc: petite démo interactive, x-show et hx-on on va dire 
avec click to enter puis create et join
join et create un système de queue
et puis ensuite on passera à la salle si vous le voulez bien

3 approches :
```python
try:
    input_value = json.loads(request.args.get('datastar')).get('input_value')
except:
    input_value = ""
valid = "uno" in input_value.lower()
return SSE.merge_signals(signals={'valid_name': valid})

async def event():
    yield SSE.merge_signals(signals={'valid_name': valid})
response = await make_response(event(), SSE_HEADERS)
response.timeout = None
return response

queue = asyncio.Queue()
@stream_with_context
async def event():
    while True:
        try:
            input_value = json.loads(request.args.get('datastar')).get('input_value', '')
            valid = "uno" in input_value.lower()
            print("okok", input_value, request)
            if valid:
                print("ok")
                yield SSE.merge_signals(signals={'valid_name': valid})
            await asyncio.sleep(0)  # Add small delay to prevent busy loop
        except asyncio.CancelledError:
            break
        except Exception as e:
            print(f"Error in event stream: {e}")
            continue
response = await make_response(event(), SSE_HEADERS)
response.timeout = None
return response
```

1 one shot et voilà, en vrai pour un data-on-change pk pas
2 pas trop utile... si ?
3 streaming continu, faut adapter au disconnect
mais c'est stylé, ça reconnecte tout seul et tout
mais il **faut** que j'arrête de me demander ce qu'il y a dans le front
je dois m'en foutre le plus possible

ok pas mal, il a fallu gueuler sur o3 mais bon 

```python
from quart import Quart, render_template, request, make_response
from datastar_py.sse import ServerSentEventGenerator as SSE
from datastar_py.sse import SSE_HEADERS
import asyncio
import datetime

app = Quart(__name__)

# ----- BACKGROUND TASK FUNCTIONS -----

async def fetch_url(url):
    """
    Simulates fetching data from a URL.
    In a real implementation, you could use aiohttp or similar.
    """
    # For demonstration purposes, we return a fixed content.
    result = {
        "url": url,
        "content": "Example content from {}".format(url),
        "fetched_at": datetime.datetime.now().isoformat()
    }
    return result

def validate_string(input_str):
    """
    Validates the input string.
    For this example, the string is considered valid if it contains 'hello' (case-insensitive).
    """
    is_valid = "hello" in input_str.lower()
    result = {
        "input": input_str,
        "is_valid": is_valid,
        "checked_at": datetime.datetime.now().isoformat()
    }
    return result

async def query_database(sql):
    """
    Simulates a database query.
    In a real application, this would interact with your database.
    """
    # For demonstration, we return a fixed result.
    result = {
        "query": sql,
        "results": ["row1", "row2", "row3"],
        "queried_at": datetime.datetime.now().isoformat()
    }
    return result

# ----- SSE ENDPOINT COMPOSING MULTIPLE EVENTS -----

@app.route("/sse_demo")
async def sse_demo():
    """
    SSE endpoint that composes several events based on request parameters.
    The "action" query parameter controls which tasks are performed.
    The "value" query parameter is used for string validation.
    Allowed actions: "fetch", "validate", "query", or "all" (default is "all").
    """
    action = request.args.get("action", "all")
    input_value = request.args.get("value", "Hello World")

    async def event_generator():
        # Compose a list that will be sequentially yielded as SSE events.
        events = []
        # If action is "all" or "fetch", perform the URL fetch.
        if action in ("all", "fetch"):
            fetch_result = await fetch_url("http://example.com")
            events.append(SSE.merge_signals(signals={"result": fetch_result}, event="fetch"))
        # If action is "all" or "validate", perform the string validation.
        if action in ("all", "validate"):
            validate_result = validate_string(input_value)
            events.append(SSE.merge_signals(signals={"result": validate_result}, event="validate"))
        # If action is "all" or "query", perform the database query.
        if action in ("all", "query"):
            query_result = await query_database("SELECT * FROM demo;")
            events.append(SSE.merge_signals(signals={"result": query_result}, event="query"))
        
        # Yield each composed event in order.
        for ev in events:
            yield ev

        # Send a final event that indicates completion.
        yield SSE.merge_signals(signals={"message": "All tasks completed."}, event="complete")
        
        # Keep the connection open.
        # Although no further tasks are running, we yield control.
        while True:
            await asyncio.sleep(0)
    
    response = await make_response(event_generator(), SSE_HEADERS)
    response.timeout = None  # Ensure the connection stays open.
    return response

# ----- VIEW ENDPOINT (SSE CLIENT) -----

@app.route("/")
async def index():
    """
    A simple view that connects to the SSE endpoint.
    Modify the query parameters (action and value) in the URL if needed.
    """
    return await render_template("sse_demo.html")

if __name__ == "__main__":
    app.run(debug=True)
```

oui pourquoi pas ça peut marcher si les trucs qui renvoient vers cette route 
rafraichissent la requete pour rafraichir les args

ok donc
#datastar hands-on 
1. hypermedia (média avec instructions, "navigateur") 
2. signal simple 
3. update d'un signal (validation) (en vrai faudrait fragment)
4. update d'un fragment (join room, ouvrir un signal quand nécessaire)
5. une room, le serveur envoie une info différente à chacun
6. js custom avec une carte à gratter

deadlocks 
https://stackoverflow.com/questions/56377402/why-is-asyncio-queue-await-get-blocking
and infinite loops are scary, i can't hear the fans of my remote server 

<!-- discord ultrarena: https://discord.gg/Fjp3QvNf
ça se refait facile, avec les arrow keys pour bouger,
juste update le fragment de ton joueur, sa pos, sa class=cheer_value en popover,
un peu de debounce, fleches pour bouger,
le petit cooldown façon wow en merge fragment"disabled",
les grosses emotes je sais pas encore mais ça devrait aller,
utiliser twitch embed bon ça ira...
ouais. react + graphql nana c'est forcément pas ça.
ça va le faire tranquille. -->

revenons à nos moutons
pourquoi pas un jeu de réflexes ?
avec un buzzer en webcomponent qui renverra l'event entre le moment où il a display et où il a cliqué
6. buzzer

aussi, comment empêcher ouverture de trop de connections 
solution 1: renvoyer un fragment qui disable le bouton et qui met un petit indicateur (simple, efficace)
solution 2: cookie user et abort 400 ?
il faut que je test ça

visiblement le cache était déjà setup donc 
le comportement bizarre en tab in/tab out c'est pas ça 
ça se joue à si y'a un loop ou pas 

gaffe à pas envoyer de password pour validation ! les forms c'est pas pour les chiens

et donc, new user >
register queue, populate...
mouais, quitte à le faire pour les salles autant "poll"
on montrera d'autres choses
les salles donc...

à la fin, pas sûr de pourquoi buzzed ne "bubble up" pas...
mais bon, on s'en est sorti avec ce composant de mes deux.
allez on rajoute un peu d'aléatoire.

et bon bah... jcrois que c'est bon pour le mvp.
plus qu'à obs, record, upload et ping.

ici lit pour faire des composants qui font des events
https://chatgpt.com/c/67a1c363-71d4-800c-9bcc-229b55f98477

---

deux vidéos plus tard
j'ai encore l'impression de faire trop d'endpoints c'est terrible
des routes /<user_id>/<action> ?
comment bien faire une auth ?

je fais pas encore bien les updates, les queues
quand je veux les faire depuis les classes ça foire
classes que je sérialisent toujours pas
je sais pas où foutre les queues non plus

---

on s'est bien amusé avec redis
ça va vite vroum vroum

---

bon faut que je les foutent dans redis

tinydb c'est vraiment bien
faut que je le mette au moins sur leg.ovh
stack nginx/gunicorn/flask
puis htmx/tinydb
bon c'est parfait quoi

deux problèmes sur temp.py tmp
pourquoi I déborde en H ou je sais pas quoi
comment faire le texte, StrEnum ?
non int enum

oui donc grosso modo ça
comment marche bhil
bhil x
et comment faire ton intenum/strenum bref
si tu sais ce qui a dedans
sinon liste mais c'est bien car c'est different d'array
tu sais qu'il faut pas y accéder tout de suite


import array

for t in array.typecodes:
    a = array.array(t, [])
    print(a, a.itemsize)

array('b') 1
array('B') 1
/home/le/tmp/temp.py:121: DeprecationWarning: The 'u' type code is deprecated and will be removed in Python 3.16
  a = array.array(t, [])
array('u') 4
array('w') 4
array('h') 2
array('H') 2
array('i') 4
array('I') 4
array('l') 8
array('L') 8
array('q') 8
array('Q') 8
array('f') 4
array('d') 8


import secrets

s = secrets.token_bytes(8)
print(s)

u5 = array("L", s)
print(u5)

25 millions d'années pour guess
si j'augmente un L toutes les millisecondes (100FPS)
je le remplis au bout de 600 millions d'années

random.randbytes(n) existe mais pas secure

un I c'est 6 jours

parce qu'en vrai pas besoin d'uuid
array('L', uuid4().bytes)
parce que l'id c'est l'index
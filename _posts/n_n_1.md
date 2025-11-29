n = n * 1

même dans un hyperespace,
peut-on le prendre dimension par dimension ?

idée : si je prends un encoding de mots en n dimensions,
mettons que je commence une phrase
pour chercher le mote suivant probable,
je peux utiliser une recherche de proximité
avec une norme l de n
(grossir la n-sphere)

mais je peux aussi choisir un random i parmi n
et chercher dans cette direction
proposer à l'user un choix binaire sur le premier à "gauche" et à "droite"
et selon sa réponse améliorer les positions ?

"ok, c'est censé arriver plutôt à droite
donc je décale la composante i de chaque mote de la chaîne
un peu à droite"

sous-optimal ? certainement
sujet à des sous-optimum ? peut-être
plus facile to reason about ?
ah oui, et c'est d'ailleurs l'enjeu

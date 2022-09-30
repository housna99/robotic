# Apprentissage en ligne pour Pioneer

## Desription

Le probleme est le suivant : un robot Pioneer se situe dans une certaine
configuration (x, y, theta) dans l'espace et doit rejoindre une cible
(x', y', theta').
Il est commandé par un réseau de neurones qui prend en entree l'erreur entre
la position reelle et la position cible et donne en sortie la commande sur les
deux roues (q_1, q_2)

## Arborescence

- BackProp_Python_v2.py : le modele du reseau de neurones utilise dans run.py ainsi que la rétropropagation du gradient associe.

  - Note : Dans le constructeur de NN, on peut modifier l'intervalle des valeurs de depart des poids aux lignes ou randomizeMatrix est appelee.

- online_trainer.py : c'est dans ce fichier que se situe l'algorithme d'apprentissage, ainsi que le calcul du gradient.
- run.py : le fichier qu'il faut lancer pour utiliser l'application. Attention a� bien le modifier selon les besoins (robot reel, robot simule)
- simu.ttt : la scene V-REP contenant le modele du Pioneer
- vrep_pioneer_simulation.py : le modele du Pioneer simulé
- rdn.py : le modele du Pioneer reel, contrôlé avec RosAria
- v1.py : une premiere version de l'apprentissage sur simulateur, non essentiel a� la simulation
- BackProp_Python.py : le modele original, qui peut etre utilise pour d'autres projets, non essentiel e� la simulation

## Utilisation

_Attention_ : testé sous python 3.5 uniquement

### Simulation

L'apprentissage sur la simulation se fait avec le simulateur V-REP. La première
chose que vous devez donc faire est de [télécharger](http://www.coppeliarobotics.com/downloads.html)
la version de V-REP correspondant à votre OS (Win, OS X, Linux disponibles).
Dans ce code, on utilise l'API externe de V-REP en python, il va donc falloir
que vous copiez trois fichiers dans ce dossier :

- vrep.py et vrepConst.py que vous trouverez dans les fichiers d'installation
  de V-REP sous programming/remoteApiBindings/python/python
- remoteApi.?? dont l'extension dépendra de votre OS (Linux : .so, Win : .dll,
  OS X : .dylib)
  que vous trouverez sous programming/remoteApiBindings/lib/lib

Avant de lancer le programme, il faut modifier run.py pour s'assurer que
l'objet `robot` au début du fichier est bien une instance de robot simulé :

```
robot = VrepPioneerSimulation()
```

Il suffit ensuite de lancer le fichier run.py et de suivre les instructions :

```
$ python run.py
```

Si tout fonctionne correctement, l’utilisateur verra apparaître ‘Connected to
remote API server on…’ puis l’IP du serveur vrep. On peut modifier l’IP et le
port dans le fichier vrep_pioneer_simulation.py.

A la fin de la simulation, les poids de la dernière itération sont enregistrés
dans le fichier `last_w.json`. Attention, celui-ci écrase le précédent fichier
si son nom n'a pas été changé !


# Les algorithmes de recherches

## 1) Contexte

Considérons une liste d’étudiants participant à un examen. Les étudiants sont classés par ordre alphabétique. Un surveillant doit absolument parler à l’un des étudiants : il y a une fuite d’eau chez lui et la canalisation a lâché. Il faut qu’il rappelle lespropriétaires. 

Prenons un autre exemple : On cherche dans un dictionnaire la page à laquelle se trouve un mot. Un dictionnaire peut être considéré comme un tableau trié.

Comment faire pour trouver le mot le plus rapidement possible ?

Ces deux situations se modélisent de la même façon en informatique. On a un tableau trié d’éléments et on doit trouver l’index d’un élément dans le tableau. On doit aussi éventuellement pouvoir vérifier qu’il ne figure pas dans le tableau. Ce problème de la recherche en table est un problème de base de l’informatique théorique. Il est intéressant par ce qu’il permet d’entrevoir la notion d’efficacité d’un algorithme. 

En résumé, le problème est le suivant :
On considère un tableau T trié de N éléments. Comment montrer qu’un objet O se trouve dans le tableau, en précisant son index, ou ne s’y trouve pas.

## 2) Un premier algorithme

### 2.1) Principe

On peut procéder de façon assez naïve pour résoudre ce problème. Il suffit de parcourir le tableau en commençant par le premier élément, et de le parcourir jusqu’à ce que l’on ait trouvé O. Pour rechercher notre aiguille dans la meule de foin, on la parcourt de façon exhaustive.

### 2.2) Exercice

Réaliser un algorithme qui effectue cette recherche sans fonction puis avec.

## 3) La recherche par dichotomie

### 3.1) Principe

Cette méthode s’apparente à la méthode "diviser pour mieux régner". On compare le nombre recherché au nombre qui se trouve au centre du tableau :

- Si le nombre recherché est égal au nombre qui se trouve au centre du tableau, c’est terminé.
- Si le nombre recherché est inférieur au nombre qui se trouve au centre du tableau, on recommence sur la première moitié du tableau.
- Si le nombre recherché est supérieur au nombre qui se trouve au centre du tableau, on recommence sur la deuxième moitié du tableau.

 Exemple : Supposons que le nombre recherché soit égal à 3 :
  Étape 1 : 1 2 3 4 5 6 7 8 9
  Le nombre au centre du tableau est 5. Puisque 3 est inférieur à 5, on recherche dans la 1ère moitié du tableau
  Étape 2 : 1 2 3 4 5 :
  Le nombre au centre du tableau est 3, il est égal au nombre recherché, c’est terminé.

## 4) Exercice : écrire la fonction

Écrire la fonction rechercheDicho qui effectue la recherche par dichotomie. Montrer la terminaison de la recherche dichotomique à l’aide d’un variant de boucle.

## 5) Comparaison entre les deux méthodes de recherche

Tester le temps mis par ces deux algorithmes pour rechercher une valeur sur un liste de 10,100,1000 éléments. Faites en la représentation graphique. Évaluer la complexité de ces deux algorithmes

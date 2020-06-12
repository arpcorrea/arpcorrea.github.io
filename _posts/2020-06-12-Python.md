# Introduction

Nos données d'aujourd'hui sont un fichier _comma-separated values_ (CSV) sur l'inflammation de patients :
```
0,0,1,3,1,2,4,7,8,3,3,3,10,5,7,4,7,7,12,18,6,13,11,11,7,7,4,6,8,8,4,4,5,7,3,4,2,3,0,0
0,1,2,1,2,1,3,2,2,6,10,11,5,9,4,4,7,16,8,6,18,4,12,5,12,7,11,5,11,3,3,5,4,4,5,5,1,1,0,1
0,1,1,3,3,2,6,2,5,9,5,7,4,5,4,15,5,11,9,10,19,14,12,17,7,12,11,7,4,2,10,5,4,2,2,3,2,2,1,1
0,0,2,0,4,2,2,1,6,7,10,7,9,13,8,8,15,10,10,7,17,4,4,7,6,15,6,4,9,11,3,5,6,3,3,4,2,3,2,1
0,1,1,3,3,1,3,5,2,4,4,7,6,5,3,10,8,10,6,17,9,14,9,7,13,9,12,6,7,7,9,6,3,2,2,4,2,0,1,1
```
* où chaque lignes représente un patient;
* chaque colonnes représente une journée consécutive.

On veut pouvoir:
- charger des données en mémoire;
- calculer des statistiques sur ces données
- créer des graphiques des résultats.

Pour cet atelier nous utiliserons [Python 3](https://docs.python.org/3/). Vous pouvez à tout moment vous référer au matériel d'origine de [Software Carpentry](http://swcarpentry.github.io/python-novice-inflammation/).

***

# Variables
### Objectifs
* Assigner des valeurs aux variables.

Nous pouvons utiliser Python comme une calculatrice :


```python
3 + 5 * 4
```

C'est bien mais nous ne pouvons réutiliser ce résultat. Pour ce faire, nous devons utiliser une _variable_.
Par exemple, créons une variable `poids_kg` contenant un poid en kilogramme.


```python
 
```

Maintenant, lorsque nous utiliserons `poids_kg`, Python nous retournera la valeur qui lui est associée.

En Python, les noms de variables doivent respecter les règles suivantes :
- peuvent inclure des lettres, nombres et barre de soulignement;
- ne peuvent débuter par un nombre;
- sont sensible à la casse.

Par exemple :
- `poids0` est un nom de variable accepté alors que `0poids` ne l'est pas.
- `poids` et `Poids` sont deux variables différentes.


```python

```

## Types

Il existes plusieurs types de données, en voici trois très communs :
- nombres entier;
- nombres décimaux;
- chaînes de caractères.

Dans l'exemple précédent, nous avons assigné la valeur entière `60` à la variable `poids_kg`.
Afin de créer une valeur décimale, nous pouvons :


```python
poids_kg = 60.0
```

Et afin de créer une chaîne de caractères, nous utiliser entourer du texte de guillemets simple ou doubles, par exemple :


```python
poids_kg_texte = 'poids en kilo :'
```

## Utilisation de variables

Afin d'afficher la valeur d'une variable à l'écran, nous pouvons utiliser la fonction `print` :


```python

```

Il est aussi possible d'afficher plusieurs variables :


```python

```

On peut même effectuer des opérations arithmétiques, par exemple convertir en livre.


```python
print("Le poids en livres est: ", poids_kg * 2.2)
```

La variable `poids_kg` n'a pas été modifié.


```python
print(poids_kg)
```

On peut assigner une nouvelle valeur à la variable


```python
# poids_kg = 
print('Le poids en kilogrammes est maintenant:', poids_kg)
```

## Exercice

Pouvez-vous prédire quelles seront les valeurs des variables `masse` et `age`?


```python
masse = 47.5
age = 122
masse = masse * 2.0
age = age - 20
print(masse, age)
```

***
# Charger des données
### Objectifs
* Comprendre ce qu'est une librairie et leur utilité;
* Importer une librairie et pouvoir utiliser ses fonctions;
* Charger des données tabulaires depuis un fichier;
* Sélection de valeurs individuelles et sous-sections des données;
* Effectuer des opérations sur les données.

Pour débuter, nous avons besoin de charger un module nommé [NumPy](https://docs.scipy.org/doc/).


```python

```

On peut maintenant utiliser numpy pour charger notre fichier csv.


```python
numpy.loadtxt(fname='data/inflammation-01.csv', delimiter=',')
```

Le fichier chargé en mémoire est affiché à l'écran, mais on ne peut pas le manipuler directement. Pour ce faire, il faut créer une variable. Tout comme on assigne une valeur à une variable, on peut assigner à une variable le résultat d'un appel de fonction.


```python
data = numpy.loadtxt(fname='data/inflammation-01.csv', delimiter=',')
```

Puis affichez le résultat de cette assignation à l'aide de la fonction `print` 


```python

```

À tout moment, on peut connaître le type d'une variable en utilisant la fonction `type`.


```python

```

Notre structure de données représentée par la variable `data` a aussi des propriétés, par exemple `dtype`.


```python
print(data.dtype)
```

On peut aussi afficher les dimensions de notre tableau en accédant à la propriété `shape`.


```python

```

Pour accéder à un élément de notre tableau, nous utilisons les crochets ou "brackets" (`[]`). Par exemple, essayons d'accéder à l'élément de la ligne 30 et de la colonne 20.


```python

```

À votre avis, quels sont les indices correspondant à l'élément situé à sur la première ligne et la première colonne?


```python

```

![Python Zero Index](images/python-zero-index.png)

On peut non seulement extraire des éléments, mais aussi des sous-ensembles de notre tableau en utilisant le concept de tranche représenté par l'opérateur `:`.


```python

```

Les indices des tranches ne doivent pas obligatoirement commencer à 0.


```python

```

Il n'y a pas non plus d'obligation de définir la borne inférieure et supérieure des tranches. Ainsi, on peut appeler directement:


```python
vue_table = data[:5, 30:]
print("Notre petite table:")
print(vue_table)
```

On peut appliquer des opérations avec des scalaires directement sur notre tableau. Par exemple, si on voulait multiplier chacune des valeurs du tableau précédent, on ferait ceci:


```python
# doubletbl = 
```

On peut aussi effectuer des opérations entre des tableaux. On peut par exemple additioner le premier et le second tableau que nous avons créés.


```python
# ... = ... + ...
```

Souvent, nous sommes intéréssés à réaliser des opérations plus complexes qu'additionner, multiplier ou soustraire. Numpy fournit des fonctions pour réaliser ces opérations plus complexes. Par exemple, si on veut déterminer la moyenne pour l'ensemble des données de notre tableau `data` : 


```python
numpy.mean(data)
```

Cette valeur représente l'inflammation moyenne pour tous les patients durant toute la période de leur séjour. On pourrait aussi vouloir calculer la valeur maximale, minimale et l'écart-type.


```python

```

Pour en apprendre davantage sur une fonction, vous pouvez à tout moment appeler la fonction `help()` et fournir en argument le nom de la fonction d'intérêt.


```python
help(numpy.std)
```

Sachant que dans notre tableau, chaque ligne représente un patient. Comment pensez-vous qu'il serait possible de récupérer les données de séjour du premier patient?


```python

```

Calculez la valeur d'inflammation maximum pour ce patient:


```python

```

Le tableau n'a pas seulement des propriétés tel que `shape`, il dispose aussi des fonctions qui lui sont propres, ou de méthodes. Pour appeler ces méthodes, on utilise l'opérateur `.`.


```python
data[2, :].max()
```

Les opérations sur un tableau peuvent s'effectuer en fonction des lignes, des colonnes ou de l'ensemble du tableau. Les lignes et les colonnes sont ce qu'on appelle les axes du tableau.

![alt text](images/python-operations-across-axes.png)

Par exemple, calculons l'inflammation moyenne par jour pour l'ensemble des patients. À quel graphique cela correspond-il?


```python

```

Si on voulait plutôt calculer l'inflammation moyenne par patient, qu'est-ce qu'il faudrait changer?


```python

```

Les résultats de ces appels de fonctions sont toujours des tableaux numpy. Comment faire pour s'en convaincre?


```python

```

***
# Visualiser des données
### Objectifs
* Créer de simples graphiques rapidement à partir des données;
* Grouper des graphiques dans une seule figure.

La présentation de chiffres offre peu d'intuition pour comprendre ce qui passe véritablement avec nos données. Conjointement avec numpy, nous pouvons utiliser le module `matplotlib` pour produire une représentation graphique de nos données.

Importez matplotlib.


```python

```

Pour garantir l'affichage à l'intérieur de notre notebook. Il faut appelez une commande magique qui est propre à l'environnement actuel


```python
%matplotlib inline
```

On peut maintenant afficher nos données dans un premier temps comme un heatmap:


```python
matplotlib.pyplot.imshow(data)
matplotlib.pyplot.show()
```

On peut aussi afficher des courbes, par exemple la courbe de l'inflammation moyenne par jour pour l'ensemble des patients.


```python
inflam_mean = numpy.mean(data, axis=0)
matplotlib.pyplot.plot(inflam_mean)
matplotlib.pyplot.show()
```

À partir de l'exemple précédent, produisez un graphique pour l'inflammation maximum ainsi qu'un graphique pour l'inflammation minimum.


```python

```

Peut-on les superposer?


```python

```

Tout peut être modifié sur un graphique, du nom des axes au titre, en passant par la légende et le format du trait de la courbe. La seule limite est votre imagination et votre patience.

Jetez un oeil à la gallerie d'exemples de [matplotlib](http://matplotlib.org/gallery.html).

## Exercices

### 1. Créer votre propre graphique

Créez un graphique affichant l'écart-type (`numpy.std`) de l'inflammation pour chaque jour pour tous les patients. 


```python

```

### 2. Organiser ses graphiques

Modifiez le programme d'affichage des graphiques de manière à afficher chaque courbe dans un plan cartésien distinct.

Pouvez-vous refaire le graphique, mais cette fois en orientant les graphiques verticalement?


```python

```

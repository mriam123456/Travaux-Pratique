http://www.jvoegele.com/software/langcomp.html

#Programmation Objet , Concept et Design Patterns

## 1. Capacité d'abstraction de bas niveau

Au niveau assembleur (équivalence 1:1 avec le Langage Machine) ,le seul outil permettant l'abstraction fonctionnelle est la fonction , qui est implémentée par les concepts de Stack , Stack Pointer et Frame

Le stack (la Pile en français) est la zone de mémoire contigüe (du point de vue du système cf: ASLR) , assignée à un processus lors de sa création par l'OS.

Le Stack Pointer contient **la plus petite adresse _x_ considérant que:**
* **Toute adresse < x est considérée comme invalide par le process**
* **Toute adresse > x est considérée valide par le process**

Dans le diagramme suivant  la région grisée représente la partie valide du Stack

![Stack Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/stack1.png?raw=true)

* **Stack Bottom** La valeur d'adresse maximum considérée comme valide , lors de l'initialtisation d'un nouveau process , le Stack Pointer pointe vers cette addresse

* **Stack Limit** La valeur d'adresse minimum considérée comme valide par le stack si pour une raison quelconque la valeur du Stack Pointer est inférieure à cette valeur , il y a "Stack Overflow"

Il existe **2 opérations possibles pour un Stack :**
* Push , permet de copier le contenu d'un ou plusieurs registre processeurs sur le stack (SP -= 4* nb_registres)
![Stack Push Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/stack2.png?raw=true)
* Pop  , permet de copier les données contenue dans le stack vers les registres processeur (SP += 4* nb_registres)
![Stack Pop Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/stack3.png?raw=true)

###Stack et fonctions

Pour chaque appel de fonction , une section du Stack est réservée pour la fonction : une **Stack Frame**

Prenons l'exemple classique d'un programme en C/C++ , dont le point d'entrée est la fonction **main\(\)** , un SF existe dès le début de l'exécution d'une fonction et ce jusqu'a la fin de son execution.

![Stack Func1 Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/mstack1.png?raw=true)

Supposons maintenant que fonction **foo\(\)** qui prend 2 arguments est appellée au sein de la fonction **main\(\)** , l'une des méthodes pour passer les arguments à **foo\(\)** est par le biais du Stack , il faut donc que du code assembleur dans **main\(\)** effectue un "push" des arguments sur le Stack , ce qui ressemble à la figure suivante

![Stack Func2 Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/mstack2.png?raw=true)

Comme on peut le voir , en placant les arguments pour alimenter **foo\(\)** sur le Stack , le SF de **main\(\)** a augmenté en taille , on constate aussi que de l'espace à été réservé pour la valeur de retour de **foo\(\)** , l'assignation effective à lieu quand **foo\(\)** à terminé son exécution.

Une fois l'exécution de **foo\(\)** débutée , la fonction **foo\(\)** peut déclarer ses propres variable internes , **foo\(\)** va donc à son tour "push" quelque données sur le stack ce qui ressemble à 

![Stack Func3 Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/mstack3.png?raw=true)

**foo\(\)** peut accéder aux arguments placés sur le Stack par **main\(\)** car **main\(\)** place les arguments à une position connue de **foo\(\)** , représentée par le **Frame Pointer (FP)** .

Le FP pointe à l'endroit ou se trouvait le SP juste avant que **foo\(\)**




##2. Nécessité d'un paradigme de composition d'ordre supérieur




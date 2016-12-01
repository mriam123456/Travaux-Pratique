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

Le FP pointe à l'endroit ou se trouvait le SP juste avant que **foo\(\)** ne l'ai déplacé pour ses besoins internes . Le FP est pratique car si l'exécution de la fonction est susceptible de déplacer le SP plusieurs fois le FP reste fixe pendant toute cette durée. De fait en code assembleur il sert de point de référence pour déterminer les positions en mémoire des variables locales et des arguments.

Enfin , une fois l'exécution de **foo\(\)** terminée ,le SP peut être ramené à la position du FP , ce qui effectivement invalide l'ensemble du Stack réservé par **foo\(\)** . Ce qui nous ramène à la figure précédent l'exécution de **foo\(\)** , à la différence que la valeur de retour calculée par foo est désormais assignée 

![Stack Func2 Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/mstack2.png?raw=true)

Une fois que **main\(\)** à récupéré la valeur de retour , elle est "pop" vers les registre processeur ,le SP est replacé avant les arguments et la valeur de retour , ce qui les invalide sur le Stack.

![Stack Func1 Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/mstack1.png?raw=true)


###Fonctions récursives

Aucune modification dans le concept

###Heap

Le Heap (Tas en Français) est la section de mémoire que l'OS assigne pour l'allocation dynamique de mémoire , typiquement les structure de données dynamique sont programmée par des langage de Haut Niveau (C/C++) car leur conception est bien plus complexe en assembleur . Le Heap nécessite d'être controlé par le programmeur (requete d'une taille de mémoire , structure de données dynamique pour permettre de suivre à la trace la quantité de mémoire allouée à chaque cycle, etc ...) .

Historiquement , la complexité de la programmation des structures dynamiques (et les menaces qu'elles font planer sur la sécurité du code informatique) , ont motivé le développement des langages à mémoire managée (Java / C\# / ...)





##2. Evolution langage et runtime multi-plateforme

Les langages C et C++ offrent, grâce aux architectures processeurs et aux compilateurs modernes capables de produire et traiter du code machine hautement optimisé , des performances de très haut niveau avec virtuellement aucune perte vis-à-vis du code assembleur , reléguant ce dernier à l'écriture de drivers .

Le language C++ en particulier offre des capacités hybrides multi-paradigmes (Couche objet) et s'est imposé comme la référence pour toute applications pour lesquelles les performances sont cruciales.

Les languages tels que Java et C# propose quand à eux des capacités avancées en termes de programmation , de capacité de RAD et le Garbage Collection , ce qui réduit largement le temps requis pour le cycle de développement d'un programme . 

D'autre part , ces languages sont compilés non pas en code machine , mais dans un language intermédiaire (Java ByteCode ou MSIL) qui est executé par un runtime spécialisé (JVM ou CLR) . Cette stratégie permet de conquérir les problèmes de portabilité.

##3. La couche objet



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
* Pop  , permet de copier les données contenue dans le stack vers les registres processeur (SP += 4* nb_registres)






##2. Nécessité d'un paradigme de composition d'ordre supérieur


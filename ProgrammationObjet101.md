http://www.jvoegele.com/software/langcomp.html

#Programmation Objet , Concept et Design Patterns

## 1. Capacité d'abstraction de bas niveau

Au niveau assembleur (équivalence 1:1 avec le Langage Machine) ,le seul outil permettant l'abstraction fonctionnelle est la fonction , qui est implémentée par les concepts de Stack , Stack Pointer et Frame

Le stack (la Pile en français) est la zone de mémoire contigüe (du point de vue du système cf: ASLR) , assignée à un processus lors de sa création par l'OS.

Le Stack Pointer contient **la plus petite adresse __x__ considérant que: **
* **Toute adresse < x est considérée comme invalide par le process**
* **Toute adresse > x est considérée valide par le process **

![Stack Image](https://github.com/mriam123456/Travaux-Pratique/blob/master/img/stack1.png?raw=true)


##2. Nécessité d'un paradigme de composition d'ordre supérieur


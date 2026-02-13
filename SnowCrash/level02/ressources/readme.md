Level 02

1er tentative :
commande : find / -user flag02 2>/dev/null
resultat : rien trouve

2 tentative :
grep flag02 /etc/passwd
resutat : flag02:x:3002:3002::/home/flag/flag02:/bin/bash
flag02:x =  what ???

3 tentative :
grep flag02  /etc/shadow
resultat : grep: /etc/shadow: Permission denied

4 tentative :
'se situe dans la racine' : commande : ls
resutat : fichier existant = level02.pcap
contenu du fichier : fichier non lisible
�ò�@f&N.J'̊$E<��@@J>;���;��ߙO/Y������
 @f&N�JJ$E<@@�/;���;���/Y�O���A� 8����
�.� @f&N�B'̊$E4��@@JE;���;��ߙO/Y�º��B�sp
 �.�@f&N֡EE$E7ԣ@@�;���;���/Y�O���B���

Que faire ??

Copier le fichier level02.pcap dans ma machine local
pour l'ouvrir -> fichier -> open 
resulat : aucun resulat (decu)

Ha Ha ! voici ce que j'ai appris le mot clef "strings"
ce mot permet d'extraire tous les mots lisibles dans un fichier pratiquement illisible 
 commande : strings level02.pcap

il ny a plus qu'a filtrer pour trouver le mot de passe dans ce fichier 
commande : strings level02.pcap | grep -i pass (-i permet de trouver le mot peut importe la maniere dont il est ecrit)

resultat : Password: Nf&Na

Bravo !

Heu Non cela ne marche pas :/

ok on installe Wireshark

dans le terminal local : copier = scp -P 4242 level02@10.11.200.24:~/level02.pcap .
dans le logiciel -> file -> level02.pcap -> open 
clic droit -> shown ...


Youpi j ai trouve le VRAI mot de pass : 




Info : C’est quoi un fichier .pcap ?

Un fichier .pcap est un fichier de capture réseau.

👉 Il contient :

des paquets réseau

des échanges entre machines

par exemple : connexions, logins, mots de passe, requêtes HTTP, FTP, etc.

C’est comme un enregistrement vidéo du réseau.

pour aller plus loin :

🦈 Wireshark, c’est quoi ?

Wireshark est un logiciel qui permet de :

voir tout le trafic réseau

analyser les paquets

lire des mots de passe en clair quand ils ne sont pas chiffrés 

👉 C’est un analyseur de réseau.

Un fichier .pcap = un fichier que Wireshark comprend parfaitement.

Installation : sudo apt install wireshark

Ouvrir le fichier .pcap
Lance Wireshark
File → Open
Sélectionne level02.pcap
clic droit shown ....
trouver mot de pass 

Tu verras une liste de lignes (paquets).


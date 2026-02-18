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


Deuxieme explication :


Exercice 02

connection : level02
mot de pass :  f2av5il02puano7naaf6adaaf

mot de pass trouve : ft_waNDReL0L
token obtenu : kooda2puivaav1idi4f57q8iq

comment proceder :
tapez commande ls :
fichier : level02.pcap

fichier .cpap c'est quoi ? 

Les fichiers PCAP (Packet Capture) sont des fichiers utilisés 
pour capturer et stocker le trafic réseau.
Ils contiennent les paquets de données ainsi que leurs en-têtes, 
fournissant des informations essentielles comme l’heure, la source, 
la destination et le protocole utilisé. 
Ils sont largement utilisés en cybersécurité et en administration réseau pour le diagnostic, 
l’analyse de performance et la détection d’activités malveillantes.

Contenu du fichier illisible : caractere cache

Dans terminal local 
copier le fichier qui se touve dans la vm 
scp -P 4242 level02@192.168.1.14:/home/level02/level02.pcap .

scp -P <port> <name@Ip_vm:cheminDuFichier> <CheminLocalOuCopierLeFichier>

Que faire ? Installer Wireshark (Wireshark permet une analyse graphique détaillée)
 -> d'autres outils existent comme tcpdump offre une lecture en ligne de commande ou 
CloudShark pour analyser les fichiers sans installation.

lien installation : https://fr.linux-terminal.com/

apres installation 
tapez la commande : wireshark
fenetre s'ouvre 
-> file > choisir file > open
clique droit sur un TCP -> follow -> TCP stream

recherche mot en clair mot de pass :  ft_wandr...NDReL0l.L
. = backspace (a transforme)
mot de passe reel = ft_waNDReL0L

Wireshark permet de voir et analyser toutes les données réseau qui ne sont pas chiffrées

Info : 

TELNET est un protocole applicatif qui utilise TCP. pas de securite
Il sert à :
se connecter à distance à une machine
taper des commandes
comme un terminal distant (tout est en clair)

Aujourdhui SSH (Secure Shell) = chiffrement (securise)

FTP (File Transfer Protocol) = fichiers en clair
👉 Il sert à :
envoyer
recevoir
gérer des fichiers à distance

Particularité FTP
2 connexions TCP :
Contrôle (login, commandes)
Données (fichiers)

⚠️ Problème de sécurité

Login en clair :
Mot de passe lisible
Fichiers lisibles aussi

Aujourdhui on utilise SFTP / FTPS = chiffrement (securise)

TCP (Transmission Control Protocol) = transporteur de donnee dans lordre et controle les pertes en chemin

Aujourdhui TCP + TLS (Transport Layer Security) = (certificats);


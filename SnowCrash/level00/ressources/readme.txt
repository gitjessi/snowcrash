Snow crash LEVEL 00
Objectif : trouver le mot de pass de flag00

se connecter avec level00
mot de pass :level00

trouver tous les fichiers appartenant a flag00
commande : find / -user flag00 2>/dev/null

trouver mot de passe : 
commande : ls -la "dossier"

regarder fichier pouvant contenir un mot de passe (15 caracteres)
cat "fichier"

Trouve !! 
mot de pass : qui ne veut rien dire : cifdsfhdjfhsdf

Objectif dechiffrer ce mot de pass

Methode 1 :

Utiliser john : John the Ripper
Specialite: Capable de casser des mots de passe chiffrés

Installation : 
git clone https://github.com/openwall/john.git
cd john/src
./configure
make -s clean && make -sj4
cd ../run
./john --help -> voir toutes les facons de dechiffrer mot de pass HASH

Commande : 

Attaque : ./john hash.txt
attaque avec une wordlist précise : ./john --wordlist=password.lst hash.txt
voir mot de pass : ./john --show hash.txt

John pas adapter car le mot de passe n'est pas hashe 

Methode 2 : 

Utiliser : ROT / Caesar cipher
specialite : chiffrement par décalage

tester tous les ROT :

commande : for i in {1..26}; do
  echo "$i: $(echo cdiiddwpgswtgt | tr 'a-z' "$(printf '%s' {a..z} | cut -c$i-26)$(printf '%s' {a..z} | cut -c1-$((i-1)))")"
done

ou 

sur le site : https://www.dcode.fr/chiffre-cesar

resulat : nombre_decalage(ROT12) : mot_de_pass_logique_et_lisible (nottoohardhere)

Bravo !

connect sur Vm :
login flag00
mot de pass : nottoohardhere
whoami : flag00
getflag : token

Exercice Termine


Info :

dans Excercice tout dois ce faire dans la machine local
Installation de John

Copier des fichiers ou dossiers de la vm a la machine local 
commande : scp user@IP_VM:/chemin/du/fichier /chemin/local/

connecter la vm dans ma machine local : 
commande : ssh level00@10.14.200.5 -p 4242







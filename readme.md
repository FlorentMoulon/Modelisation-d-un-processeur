# Notre premier processeur 

Le but du projet est d’implémenter un circuit modélisant un processeur, qui pourra effectuer les instructions de base, ainsi qu'un programme permettant de traduire un code assembleur en code exécutable par notre processeur.


## Fonctionnalités 


Le processeur permet d'effectuer les instructions suivantes: 
- ADD, SUB, AND, OR, XOR, SL, SR, MUL (et leurs variantes immédiates) 
- STR, LD
- JMP, JEQU, JNEQ, JSUP, JINF
- CALL, RET, STOP. 
 
De plus, nous avons implémenté les labels et les commentaires qui sont géré via l'assembleur Python. 




## Documentation

Pour utiliser notre processeur, il faut suivre plusieurs étapes :
- Ecrire un programme en langage assembleur dans un fichier `entrees.txt` et exécuter le programme Python (`assembleur.py`). Cela génère un fichier `sorties.txt` qui contient le code hexadécimal correspondant au programme.
- Ouvrir le fichier `processeur.circ` avec Logisim, faire un clic droit sur le composant RAM et cliquer sur "Edit Contents", dans le menu qui s'ouvre, importez le fichier généré `sorties.txt` précédemment.
- Lancez maintenant la simulation dans Logisim en choisissant la fréquence d'horloge.


## Vecteurs de test 

Pour vérifier que notre processeur fonctionne correctement, nous avons utilisé les programmes de test suivants :

##### Programme basique
```x86asm
MAIN:   XOR R0 R0 R0 # test commentaire
        ADDi R0 R0 5
        CALL FCT
        STOP
FCT:    ADDi R0 R0 15
        RET
```
##### Programme Fibonnaci Itératif
```x86asm
        XOR R4 R4 R4
        ADDi R4 R4 2
        XOR R1 R1 R1
        XOR R2 R2 R2
        XOR R3 R3 R3
        XOR R0 R0 R0
        ADDi R0 R0 15
        CALL FIBO
        CALL AFF
        STOP
FIBO:   JINF R0 R4 END
        ADDi R1 R1 1
        ADDi R2 R2 1
LOOP:   ADD R3 R1 R2
        ADDi R1 R2 0
        ADDi R2 R3 0
        ADDi R4 R4 1
        JNEQ R4 R0 LOOP
END:    ADDi R0 R3 0
        RET
AFF:    XOR R7 R7 R7
        ADDi R7 R0 0
        RET
```
##### Programme pour tester les CALL imbriqués
```x86asm
    CALL F1
    STOP
F1: ADDi R2 R2 1
    CALL F2
    RET
F2: ADDi R2 R2 1
    RET
```
##### Programme pour tester les appels de fonctions successifs
```x86asm
    XOR R2 R2 R2
    CALL F1
    CALL F2
    CALL F3
    CALL F4
    CALL F5
F1: ADDi R2 R2 1
    RET
F2: ADDi R2 R2 1
    RET
F3: ADDi R2 R2 1
    RET
F4: ADDi R2 R2 1
    RET
F5: ADDi R2 R2 1
    RET
```


## Auteurs

- Aurélien Boissot 
- Nathan Bonada 
- Luc Brun
- Damien Laqueuvre
- Florent Moulon 

Sur la base d'un prototype de Théo Pierron
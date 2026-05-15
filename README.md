# LAB-6-Analyse-statique-d-un-APK-avec-MobSF-dans-la-VM-Mobexler
# démarrage de MobSF (Mobile Security Framework) version 4.0.6, un outil d'analyse de sécurité pour applications mobiles (Android/iOS).
<img width="897" height="488" alt="image" src="https://github.com/user-attachments/assets/c54ee860-5b5d-4404-8fd8-5da9d5880187" />
# Informations générales et scores de l'application
<img width="1016" height="167" alt="image" src="https://github.com/user-attachments/assets/549e191f-a0bb-4ad1-a33e-434e8c4fb473" />
# Composants de l'application
<img width="1028" height="211" alt="image" src="https://github.com/user-attachments/assets/71d63d93-fa4b-4e68-99b5-ad2e7e963930" />
<img width="1037" height="228" alt="image" src="https://github.com/user-attachments/assets/e384419d-3845-4488-8d8f-855e2c0b24bb" />
# analyse du certificat de signature de l’APK
<img width="1037" height="302" alt="image" src="https://github.com/user-attachments/assets/de20094a-956d-4f0a-8575-4150019dc159" />
# Détail des mesures de sécurité
<img width="1032" height="290" alt="image" src="https://github.com/user-attachments/assets/b358a0a5-d66d-43c7-a758-0a9085d4a45f" />
<img width="1020" height="155" alt="image" src="https://github.com/user-attachments/assets/59c2141f-abee-4d9b-b814-228ca1c25d68" />
1. NX (Never eXecute) –  Activé
La mémoire est marquée non exécutable sauf explicitement autorisé.

Empêche l’exécution de code injecté dans la data (ex: shellcode dans un buffer).

Sécurité bonne présente.

2. Stack Canary –  Activé
Une valeur « canari » est placée sur la pile avant l’adresse de retour.

Si un buffer overflow écrase cette valeur, le programme détecte la corruption et s’arrête.

Sécurité bonne présente.

3. RELRO (Relocations Read-Only) –  Full RELRO
Full RELRO signifie que la table GOT (Global Offset Table) devient lecture seule après le chargement de la bibliothèque.

Empêche les attaques de type GOT overwrite.

Sécurité très bonne.
4. RPATH / RUNPATH –  Absent
Pas de chemin de recherche de bibliothèques dynamiques personnalisé.

C’est bon signe : évite le détournement via un chemin modifiable par l’utilisateur.

5. Fonctions fortifiées –  Absent
Aucune fonction renforcée (ex: __strcpy_chk au lieu de strcpy).

Avertissement (Warning) affiché en bas :

The binary does not have any fortified functions. Fortified functions provides buffer overflow checks against glibc’s common insecure functions like strcpy, gets etc.

Conséquence : le code natif reste vulnérable aux dépassements de tampon classiques, malgré la présence d’un canary (qui protège la pile mais pas les variables locales hors canary ou les débordements dans le tas).

# l’onglet APKID Analysis de MobSF
<img width="1030" height="356" alt="image" src="https://github.com/user-attachments/assets/854d030c-b39d-4f0a-88ad-e65ad21824c7" />

#  informations générales de l’APK
<img width="855" height="507" alt="image" src="https://github.com/user-attachments/assets/373f062c-87ed-4c8b-b79b-bf279f4f9c77" />
Ce qui a changé / est nouveau
Par rapport à la capture précédente (fichier Screenshot 2026-05-15 105058.png), on voit ici :

Min SDK : 19 (précédemment non affiché).

Max SDK : 1 (valeur anormale – nous y reviendrons).

SHA256 complet (précédemment tronqué ?).

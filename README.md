# Exercices Docker - Jack Negrello; Ahmed Nidious; Florent Lavignasse

Exercice 1 — Premier contact avec Docker

1.1 
<img width="945" height="487" alt="image" src="https://github.com/user-attachments/assets/1084034b-4e86-4003-82e9-285ddc605522" />

1.2 - 1.3
<img width="1696" height="160" alt="image" src="https://github.com/user-attachments/assets/684ad6d1-c67c-41ec-8b4a-bd55e15a8fa7" />

La commande qui permet de lister les conteneurs en cours d'exécution est docker ps

1.4
<img width="859" height="399" alt="image" src="https://github.com/user-attachments/assets/25ce89ee-61c7-4dc3-85f8-c7e9a878842a" />

On voit la page d'accueil par défaut du serveur web Nginx

1.5
<img width="1888" height="983" alt="image" src="https://github.com/user-attachments/assets/c2e1c5e3-8275-4f67-86f2-596ef0c0f0a4" />

1.6
<img width="1470" height="183" alt="image" src="https://github.com/user-attachments/assets/f9e1a1a4-3da7-4249-9371-6d25ee765d80" />

On voit que le conteneur est arreté

1.7
<img width="891" height="177" alt="image" src="https://github.com/user-attachments/assets/b7b2c040-1680-4798-9b53-aa82bbe68cdf" />

1.8
La commande qui permet de lancer le conteneur de façon à ce qu'il soit automatiquement suppromé à l'arrêt est : docker run -d -p 8080:80 --name mon-nginx --rm nginx:alpine

Exercice 2 — Construire sa première image avec un Dockerfile

2.1
<img width="598" height="142" alt="image" src="https://github.com/user-attachments/assets/8396e540-aaf3-4b52-a8b2-46b0c9a79a78" />
<img width="701" height="319" alt="image" src="https://github.com/user-attachments/assets/9c893713-34cd-4bde-bc5e-0354bef28e10" />

2.2
<img width="584" height="57" alt="image" src="https://github.com/user-attachments/assets/b6a92382-79b3-480a-911b-c6aaf9fc6d0f" />
<img width="717" height="255" alt="image" src="https://github.com/user-attachments/assets/4e5f9169-fa45-48d2-b5af-64419072c8e8" />

2.3
Voici la construction de l'image.
<img width="925" height="468" alt="image" src="https://github.com/user-attachments/assets/e0493566-b466-4ab7-83e1-ff0e76ee2e90" />


2.4
Lancement  du conteneur basé sur cette image
<img width="939" height="1064" alt="image" src="https://github.com/user-attachments/assets/8c879144-34d0-4e31-9e91-295ccbef0313" />

http://localhost:9090 ouvert sur le navigateur, qui montre mon pénom
<img width="659" height="198" alt="image" src="https://github.com/user-attachments/assets/9eaa87f3-4029-43d3-953c-06d14cec950f" />


2.5
<img width="938" height="135" alt="image" src="https://github.com/user-attachments/assets/ce8667a5-5086-47d4-aa10-32495abceaed" />
mon-site:v1 sera légèrement plus lourde que nginx:alpine car j'ai ajouté un layer avec mon index.html.

2.6
<img width="940" height="351" alt="image" src="https://github.com/user-attachments/assets/674f87e9-c442-4b80-9fad-fe1e2b4683e3" />
2 layers ont été ajoutés par rapport à l'image de base nginx:alpine : le COPY qui copie index.html dans le conteneur, et le EXPOSE qui déclare le port 80.


2.7
<img width="529" height="242" alt="image" src="https://github.com/user-attachments/assets/e60f3840-1e77-4a9a-a818-43d0e5e62258" />
Changement du h1 (jack-version 2)

<img width="954" height="538" alt="image" src="https://github.com/user-attachments/assets/2d539b1f-04a3-4993-b6ae-45c90639adeb" />
Le layer FROM nginx:alpine a été rechargé depuis le cache car l'image de base n'a pas changé. Le layer COPY index.html a été réexécuté car le fichier source a été modifié.


2.8
supprimer le mon-site:v1
<img width="946" height="155" alt="image" src="https://github.com/user-attachments/assets/6b1e232a-f7c8-40b8-b62e-5852d8315df0" />

On peut voir le mon-site:v2 est toujours present
<img width="945" height="143" alt="image" src="https://github.com/user-attachments/assets/eeceaa65-b7fa-4fb8-8d0b-1c48b80dcf7f" />




Exercice 3 — Volumes et persistance des données

3.1
<img width="873" height="344" alt="image" src="https://github.com/user-attachments/assets/7f6fae6d-e815-4883-a0d2-0bf7d3424733" />

docker run -it --rm alpine ls /data
Cela affichera une erreur aucun fichier ou dossier de ce type parce que l’option --rm dans la commande précédente (docker run -it --rm alpine sh) indique de supprimer le conteneur dès que vous le quittez.

3.2

<img width="1371" height="576" alt="image" src="https://github.com/user-attachments/assets/8651bd84-af5c-4def-9fc0-a1a04a36d61d" />

Après avoir modifié index.txt

<img width="723" height="376" alt="image" src="https://github.com/user-attachments/assets/56de7a62-9b48-4228-9fdc-018b2d650e1d" />

Parce que nous avons utilisé un bind mount (-v) :
- Le dossier exercice-3/html sur votre machine est directement lié à /usr/share/nginx/html à l’intérieur du conteneur
- nginx sert les fichiers depuis ce dossier en temps réel
- Donc toute modification faite localement est immédiatement visible dans le conteneur


3.3

<img width="1692" height="478" alt="image" src="https://github.com/user-attachments/assets/be7665ea-0f5d-4b63-ad7b-d0a7bbf8d4c5" />

3.4

<img width="716" height="210" alt="image" src="https://github.com/user-attachments/assets/7cec3d43-5a30-45b9-b4da-463ae4eaf8e0" />

3.5
<img width="596" height="88" alt="image" src="https://github.com/user-attachments/assets/0a243c82-70ee-4f64-bafa-44303ddf7028" />

<img width="266" height="100" alt="image" src="https://github.com/user-attachments/assets/0ad5b6ba-9887-407d-ae30-33ad9ab9f417" />

3.6

<img width="655" height="310" alt="image" src="https://github.com/user-attachments/assets/6557879a-90b7-4463-9363-5069f0e6be83" />

3.7

<img width="655" height="310" alt="image" src="https://github.com/user-attachments/assets/5c49a9b7-a4b6-442d-9aef-790525783dec" />


Vous ne pouvez pas supprimer un volume s’il est actuellement utilisé par un conteneur. Vous devez d’abord supprimer le conteneur.
Assurez-vous toujours d’avoir une sauvegarde des données si elles sont importantes.






Exercice 4 — Réseaux Docker

4.1
<img width="532" height="138" alt="image" src="https://github.com/user-attachments/assets/41a6fc3d-8d5a-4b4e-b560-f9c7dc6a1a43" />

Les 3 réseaux de base sont bridge, host et none

4.2 
<img width="796" height="222" alt="image" src="https://github.com/user-attachments/assets/090c03eb-1552-4a2e-9f5f-d41075d5ea0a" />

4.3
<img width="996" height="61" alt="image" src="https://github.com/user-attachments/assets/e8bc8880-0efb-4612-9ccb-d68b3947088f" />

4.4
<img width="1036" height="811" alt="image" src="https://github.com/user-attachments/assets/5e31aec3-bf5a-4237-ae58-39c37dee6e55" />

On récupère le code HTML de la page "Welcome to nginx!" qui se trouve sur le conteneur "serveur-web"

Car docker inclut un serveur DNS embarqué. Dans un réseau personnalisé, Docker enregistre automatiquement le nom du conteneur. Il traduit serveur-web en l'adresse IP interne correspondante.

4.5
<img width="718" height="87" alt="image" src="https://github.com/user-attachments/assets/693ca81a-0c71-4a80-ab7d-30b28aa5c718" />

La commande échoue avec une erreur wget: bad address 'serveur-web'.

Car client-externe et serveur-web sont sur deux réseaux isolés. Ils ne peuvent pas communiquer sans une connexion explicite.

4.6 
<img width="897" height="776" alt="image" src="https://github.com/user-attachments/assets/bbb09420-fac9-4aa8-a94e-1b6a56497c18" />

Grace à la commande connect

4.7 
<img width="753" height="291" alt="image" src="https://github.com/user-attachments/assets/f882d311-9043-4cf5-91d3-10df219cdac6" />



Exercice 5 — Containeriser un serveur Flask


5.1
<img width="707" height="521" alt="image" src="https://github.com/user-attachments/assets/9db0c41d-4d5e-41e5-bb01-31dff09f1ae5" />
Création du fichier app.py


5.2
<img width="400" height="178" alt="image" src="https://github.com/user-attachments/assets/26341a59-cbfd-4410-8ff8-b0f9dbd1087e" />
Création du requirements.txt

5.3
<img width="565" height="382" alt="image" src="https://github.com/user-attachments/assets/07bf3e61-b881-4e7c-bbc4-c4a26b0d954e" />
Création du Dockfile


5.4
<img width="934" height="750" alt="image" src="https://github.com/user-attachments/assets/215f9089-d72a-4589-94af-7f1aeaa6a78e" />
Construction de l'image


5.5
<img width="925" height="86" alt="image" src="https://github.com/user-attachments/assets/de807dd1-b44c-4963-8e03-463a12acdd57" />
<img width="543" height="199" alt="image" src="https://github.com/user-attachments/assets/bf588d56-809d-4ab2-ab2f-a3418d8ae519" />
Sur http://localhost:5000/, la page affiche bien "Flask fonctionne !" avec "Environnement : production"

5.6
<img width="933" height="106" alt="image" src="https://github.com/user-attachments/assets/e1e32112-9858-4733-a542-149f0b6b2b7b" />
<img width="582" height="210" alt="image" src="https://github.com/user-attachments/assets/6e504402-3dfc-4d4a-802c-e30e1d8b1c81" />
Sur http://localhost:5000/, la page affiche bien "Flask fonctionne !" avec "Environnement : développement"


5.7
<img width="933" height="130" alt="image" src="https://github.com/user-attachments/assets/3e4190cb-2cdb-4038-9391-81e7900bea7c" />
L'image flask-app:v1 fait 197MB. Pour la réduire, on pourrait :
Utiliser une image de base plus légère comme python:3.12-alpine ou utiliser un multi-stage build pour ne copier que les dépendances nécessaires dans l'image finale, sans les outils de build







Exercice 6 — Docker Compose : stack multi-services

6.1
<img width="710" height="529" alt="image" src="https://github.com/user-attachments/assets/bc33b9be-45d4-4ee4-b827-7c9e4fa12db2" />
Création de app.py


6.2
<img width="402" height="169" alt="image" src="https://github.com/user-attachments/assets/dd317e06-7a59-4915-adf8-4fcee3fa45f6" />
Création du app\requirements.txt


6.3
<img width="537" height="358" alt="image" src="https://github.com/user-attachments/assets/341007b7-0eeb-4d83-9f2d-32313890d2cb" />
Création du ficher Dockerfile


Exercice 7 — Variables d'environnement, fichiers .env et surcharge de configuration

7.1 Création du fichier .env
<img width="465" height="222" alt="image" src="https://github.com/user-attachments/assets/20f3c2ca-cb72-46ec-9dc1-e76b34e5ad6d" />







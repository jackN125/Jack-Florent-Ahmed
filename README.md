# Jack-Florent-Ahmed
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







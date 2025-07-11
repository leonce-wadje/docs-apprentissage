GUIDE D'INSTALLATION D'UN SERVEUR NGINX SOUS LINUX OPENSUSE
Auteur : Leonce Wadje Kamgo

Introduction
Ce guide explique comment installer et configurer un serveur Nginx sous Linux OpenSUSE pour héberger un site web sur un serveur nommé kingpin. Chaque étape comprend les commandes nécessaires et des captures d'écran pour vérifier le bon déroulement de l'installation.

Prérequis
Avant de commencer, assurons-Nous d'avoir :
•	Un serveur fonctionnant sous OpenSUSE.
•	Un accès avec des privilèges root ou un utilisateur avec les droits sudo.
•	Une connexion Internet active.
Étapes d'installation

1. Renommage du serveur
Avant d’installer Nginx, nous allons renommer le serveur en kingpin.
Commande :
sudo hostnamectl set-hostname kingpin

 
2. Installation de Nginx
Nginx n'est pas installé par défaut sur OpenSUSE. Nous devons l’ajouter et l’activer.
Commandes :
sudo zypper install nginx

 

3. Activation et démarrage de Nginx
Après l'installation, nous devons activer et démarrer le service.
Commandes :
sudo systemctl start nginx

 




4. Configuration du pare-feu
Nous devons autoriser le trafic HTTP et HTTPS pour permettre l’accès au serveur.
Commandes :
	sudo firewall-cmd --add-service=https --permanent
	sudo firewall-cmd --reload

 

5. Création d’un répertoire pour le site web
Nous allons créer un répertoire pour notre site et y placer une page de test.
Commandes :
	sudo mkdir -p /srv/www/kingpin
	sudo echo "<h1>Bienvenue sur Kingpin</h1>" | sudo tee /srv/www/kingpin/index.html 

 

6. Configuration de Nginx
Nous allons configurer un hôte virtuel pour notre site kingpin.
Commandes :
sudo nano /etc/nginx/conf.d/kingpin.conf
 
Ajoutons le contenu suivant :
server {
    listen 80;
    server_name kingpin;
    root /srv/www/kingpin;
    index index.html;
    location / {
        try_files $uri $uri/ =404;
    }
}
Enregistrez et quittez (CTRL + X, Y, Entrée).
 
Vérification et redémarrage :
sudo nginx -t

 
7. Ajout du nom de domaine localement
Pour tester le site localement, nous devons modifier le fichier hosts.
Commande :
echo "127.0.0.1 kingpin" | sudo tee -a /etc/hosts

 

8. Preuve de fonctionnement
Nous allons tester notre site web via un navigateur ou la ligne de commande.
Commande :
curl http://kingpin
   Conclusion
Ce guide nous a permis d'installer et de configurer un serveur Nginx sur OpenSUSE pour héberger un site web sous le nom kingpin. 


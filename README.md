__!Attention : Durant tout le tuto, utilisez sudo pour toutes les commandes faites dans le terminal.__


### Commencez par faire les MAJ système :

`sudo apt-get update && sudo apt-get upgrade`


### Installez Apache 2 et MariaDB :

`sudo apt-get install apache2 libapache2-mod-php mariadb-server`

Ensuite on lance l'installation sécurisée de MariaDB :

`sudo mysql_secure_installation`

### Configuration de Apache2 :

Pour configurer apache2, on va utiliser le fichier de configuration basique téléchargé par défaut a l'installation de Apache2.
On commence donc par le copier le fichier de config basique pour l'utiliser comme template:

`sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/kytkat.conf`

J'ai donc appelé ma configuration __kytkat.conf__

On va maintenant __editer le fichier de configuration que l'on viens de copier__:

Ouvrez ce fichier avec votre editeur de texte préféré: 

`/etc/apache2/sites-available/kytkat.conf`

__Décommentez la ligne "ServerName"__ puis mettez `localhost` en URL.
Pour __ServerAdmin__ mettez `webmaster@localhost`
Et enfin, pour __DocumentRoot__ mettez le chemin du dossier qui contiendras les fichier du site internet, donc ceux de PrestaShop. Personnellement je met le dossier du site sur mon bureau :

`/home/lepipotron/Bureau/prestashop/`

On va donc maintenant dire a Apache2 de __prendre en compte notre nouvelle configuration__ et non pas l'ancienne.
Pour cela on va utiliser les commandes :

`sudo a2dissite 000-default.conf`

Puis:

`sudo a2ensite kytkat.conf`

Maintenant, nous devons autoriser l'accès de notre dossier serveur à Prestashop, retournez dans le fichier de configuration `kytkat.conf` et ajoutez ces lignes a la fin:

 `
<Directory /var/www/html/example.com>
    AllowOverride All
</Directory>
`

L'attribut __AllowOverride__ permet a prestashop d'avoir les droit en ecriture et lecture dans le dossier du serveur.

La commande `sudo chown www-data: /var/www/html/example.com/` permettra a prestashop d'activer des plugins et de faire des mises a jour automatiques.

A la fin n'oubliez pas de redémarrer le serveur apache2 pour qu'il prenne en compte toutes les modifications:

`sudo /etc/init.d/apache2 restart`

### Téléchargez Prestashop :

Allez dans le dossier du serveur, pour ma part :

`cd /Bureau/prestashop/`

Pour la prochaine commande il faut que vous verifiez quelle est la dernière version de Prestashop disponible, sur ce lien: https://www.prestashop.com/fr/download

Verfiez qu'il correspond bien a cette commande :

`sudo curl -O https://download.prestashop.com/download/releases/prestashop_1.7.5.1.zip`

Si le numéro de version a la fin de la commande n'est pas le même, __remplacez le__. Mon numéro de version actuel est le 1.7.5.1.

Décompressez l'archive grace a la commande unzip :

`sudo unzip prestashop_1.7.2.1.zip` (si vous n'avez pas unzip : `sudo apt-get install unzip`)


### On va maintenant installer PHP7.0 :

Actuellement pour le bon fonctionnement de Prestashop, il est conseillé d'installer PHP7.0.
Suivez ces commandes pour installer PHP7.0 :

`sudo add-apt-repository ppa:ondrej/php`
`sudo apt-get update`
`sudo apt-get install -y php7.0`
`sudo apt-get install -y php7.0 php7.0-fpm php7.0-cli php7.0-common php7.0-mbstring php7.0-gd php7.0-intl php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-zip`
`sudo apt-get install php7.0-zip php7.0-simplexml`
`sudo apt-get install php7.0-curl`
`sudo a2enmod rewrite`

Redémarrez apache2 :

`sudo /etc/init.d/apache2 restart`

### Configuration de la base de données :

Accedez a la console mySQL :

`sudo mysql`

On va donc créer une base de données avec la commande:

`CREATE DATABASE kytkatDB;`

Puis on créer un user :

`CREATE USER 'kytkatUSER'@'localhost' IDENTIFIED BY 'kytkatMDP';`

Et pour finir on donne tous les droits a cet utilisateur:

`GRANT ALL ON kytkatDB.* TO 'kytkatUSER'@'localhost';`
 
puis on quitte la console mySQL avec `exit`;


### Installation de Prestashop :

Vous n'avez plus qu'a vous rendre sur localhost et a suivre l'installateur de Prestashop.

__Et voilà votre Prestashop est installé sur votre machine !__ 

installation de apache:

sudo apt-get install apache2 libapache2-mod-php mariadb-server
sudo mysql_secure_installation
sudo apt-get --reinstall install apache2-bin -y




installation de php : 

sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install -y php7.0
install -y php7.0 php7.0-fpm php7.0-cli php7.0-common php7.0-mbstring php7.0-gd php7.0-intl php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-zip
apt-get install php7.0-zip php7.0-simplexml
sudo apt-get install php7.0-curl


Restart apache :

sudo /etc/init.d/apache2 restart



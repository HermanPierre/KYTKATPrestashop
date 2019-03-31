!Attention : Durant tout le tuto, utilisez sudo pour toutes les commandes faites dans le terminal.


Commencez simplement par 



installation de apache:

sudo apt-get install apache2 libapache2-mod-php mariadb-server
sudo mysql_secure_installation





installation de php : 

sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install -y php7.0
install -y php7.0 php7.0-fpm php7.0-cli php7.0-common php7.0-mbstring php7.0-gd php7.0-intl php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-zip
apt-get install php7.0-zip php7.0-simplexml
sudo apt-get install php7.0-curl


Restart apache :

sudo /etc/init.d/apache2 restart



# pc-web-deploy

## App in laravel 

Os comandos iniciais estão no grupo do WPP

e aqui é a config do apache:

cd /var/www/html/
sudo chown -Rf ec2-user:ec2-user html/
sudo mkdir -p /etc/httpd/sites-available
sudo mkdir -p /etc/httpd/sites-enabled
sudo nano /etc/httpd/conf/httpd.conf
sudo nano /etc/httpd/sites-available/meusite.conf

Colocar esse conteudo:

<VirtualHost *:80>
    ServerName laravel.local
    DocumentRoot /var/www/html/public

    <Directory /var/www/html/public>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/laravel-error.log
    CustomLog ${APACHE_LOG_DIR}/laravel-access.log combined
</VirtualHost>


sudo ln -s /etc/httpd/sites-available/meusite.conf /etc/httpd/sites-enabled/meusite.conf
sudo chown -Rf apache:apache /var/www/html/
sudo chmod -R 755 /var/www/html/

sudo systemctl restart httpd
sudo apachectl configtest
sudo nano /etc/httpd/conf/httpd.conf
sudo systemctl restart httpd
cd /var/www/html/
sudo chmod 777 -Rf storage/
sudo cp .env.example .env
sudo chown -Rf ec2-user:ec2-user .env
sudo vim .env

e altere de:

SESSION_DRIVER=database

para:

SESSION_DRIVER=file

## Comandos ubuntu

## Como instalar o PHP

```
sudo apt update

sudo add-apt-repository ppa:ondrej/php

[ENTER]

sudo apt install php8.2 php8.2-mysql php8.2-intl php8.2-curl php8.2-mbstring php8.2-xml php8.2-zip php8.2-ldap php8.2-gd php8.2-bz2 php8.2-sqlite3 php8.2-redis -y

```


## Como instalar o apache

```
sudo apt install apache2 -y
```


## como instalar o composer

```
curl -sS https://getcomposer.org/installer -o composer-setup.php

HASH=`curl -sS https://composer.github.io/installer.sig`

php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

```

## Como instalar o node

```
sudo apt install nodejs -y
sudo apt install npm -y
```


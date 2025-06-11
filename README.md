# pc-web-deploy

## App in laravel 

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


## Como criar a configuração do HOST

```
cd /etc/apache2/sites-available
sudo touch app.conf
```

E colocar o seguinte conteudo lá dentro o app.conf

com o comando 

sudo nano app.conf

```
<VirtualHost *:80>
    ServerName [ip-da-sua-vm]
    DocumentRoot /var/www/html/public

    <Directory /var/www/html/public>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/laravel-error.log
    CustomLog ${APACHE_LOG_DIR}/laravel-access.log combined
</VirtualHost>
```

Agora basta executar os seguintes comandos

```
cd /etc/apache2/sites-enabled/
sudo ln -s ../sites-available/app.conf app.conf

cd /var/www/
sudo chown -Rf ubuntu:ubuntu html
cd html
mkdir public

sudo service apache2 restart
```


## Comandos que precisam ser executados uma unica vez no servidor

```
cd /var/www/html
cp .env.example .env
php artisan key:generate
php artisan migrate
sudo chmod 777 -Rf storage
```


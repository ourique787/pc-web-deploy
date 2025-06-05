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

    ErrorLog /var/log/httpd/laravel-error.log
    CustomLog /var/log/httpd/laravel-access.log combined
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

# Видео
[![Установка Foundry VTT на виртуальный сервер Ubuntu 22.04 +nginx+SSL](https://i9.ytimg.com/vi/rMPRLyrs1t0/mqdefault.jpg?v=63d04313&sqp=CNSUwZ4G&rs=AOn4CLCgaKDOiIxrJl1U7CzHALCCgtciBQ)](https://youtu.be/rMPRLyrs1t0)


## Обновление системы

`sudo apt-get update`

`sudo apt-get upgrade`

`reboot`

## Установка Node.js

`curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

`sudo apt-get install -y nodejs`

`node --version`

`npm --version`

## Установка unzip

`sudo apt-get install unzip`

## Создание пользователя

`adduser foundry`

`usermod -aG sudo foundry`

## Войти под новым пользователем

`su - foundry`

## Установка PM2

`sudo npm install pm2 -g`

# Установка Foundry

## Создание папок

`mkdir foundryvtt`

`mkdir foundrydata`

## Скачивание архива

`wget -O foundryvtt.zip 'LINK'`

## Распаковка

`unzip foundry.vtt`

## Запуск Foundry

`node $HOME/foundryvtt/resources/app/main.js --dataPath=$HOME/foundrydata`

# Добавление Foundry в PM2

## Настрйока PM2

`pm2 startup`

#### Скопировать и выполнить команду, которая выдаст команда выше, должно получится что-то вроде этого:

`sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu`

## Добавить команду запуска Foundry в PM2

`pm2 start "node $HOME/foundryvtt/resources/app/main.js --dataPath=$HOME/foundrydata" --name foundry`

# Настройка NGINX

## Установка NGINX

`sudo apt-get install nginx`

## Настройка Firewall

`sudo ufw allow 'Nginx Full'`

`sudo ufw status`

`sudo ufw enable`

`systemctl status nginx`

## Создание конфига

`sudo nano /etc/nginx/sites-available/foundry.example.com`

## Скопировать и вставить блок ниже

``server {``

    # Enter your fully qualified domain name or leave blank
    server_name             foundry.example.com www.foundry.example.com;

    # Listen on port 80 without SSL certificates
    listen                  80;

    # Sets the Max Upload size to 300 MB
    client_max_body_size 300M;

    # Proxy Requests to Foundry VTT
    location / {

        # Set proxy headers
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # These are important to support WebSockets
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";

        # Make sure to set your Foundry VTT port number
        proxy_pass http://localhost:30000;
    }
``}``

Заменить `foundry.example.com` на ваш домен, и заменить `localhost` на ip вашего сервера.

## Узнать ip

`curl -4 icanhazip.com`

## "Включить" конфиг
`sudo ln -s /etc/nginx/sites-available/foundry.example.com /etc/nginx/sites-enabled/`

## Дополнительная настройка
`sudo nano /etc/nginx/nginx.conf`

Найти и расскомментировать (убрать '#') перед стройчкой:

`server_names_hash_bucket_size 64;`

## Валидация настроек

`sudo nginx -t`

## Перезапуск NGINX

`sudo systemctl restart nginx`

# Настройка SSL

## Установка certbot

`sudo apt install certbot python3-certbot-nginx`

## Создание сертификата для домена
`sudo certbot --nginx -d foundry.example.com -d www.foundry.example.com`

## Перезапуск NGINX

`sudo systemctl restart nginx`



## Полезные ссылки

1. [How To Create a Self-Signed SSL Certificate for Nginx in Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-22-04)
2. [How To Install Nginx on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04)
3. [Ubuntu VM](https://foundryvtt.wiki/en/setup/hosting/Ubuntu-VM)
4. [Recommended Linux Installation and Usage Guide](https://foundryvtt.wiki/en/setup/linux-installation)
# Видео
[![Установка Foundry VTT на виртуальный сервер Ubuntu 22.04 +nginx+SSL](https://i.ytimg.com/vi/rMPRLyrs1t0/hqdefault.jpg?sqp=-oaymwEcCPYBEIoBSFXyq4qpAw4IARUAAIhCGAFwAcABBg==&rs=AOn4CLC7P2a6R9PDS7jOEWG91WIRWfVxoQ)](https://youtu.be/rMPRLyrs1t0)

## Требуемые технические характеристики к серверу

**Минимальные:**
* 1 vCPU
* Место на диске: 1GB
* 2 GB RAM
* Firewall и настройки безопасности настроены так, что позволяют игрокам зайти на сервер на необходимый порт.

**Рекомендуемые:**
* 2 vCPU
* Место на диске: 1GB
* 4 GB RAM
* Firewall и настройки безопасности настроены так, что позволяют игрокам зайти на сервер на необходимый порт.

_Объем памяти, требуемый серверным процессом, зависит от объема данных, включенных в игровую систему и модулей, которые активны в вашем мире. Для более крупных систем или миров, в которых используются более ресурсоемкие модули, потребуется больше оперативной памяти._

**Рекомендую сервера AEZA, сам ими пользуюсь. По этой [реферальной ссылке](https://aeza.net/?ref=352255) вы получите +15% к пополнению в первые 24 часа.**


## Обновление системы

`sudo apt-get update`

`sudo apt-get upgrade`

`reboot`

## Установка Node.js

`sudo apt-get install -y ca-certificates curl gnupg`

`sudo mkdir -p /etc/apt/keyrings`

`curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg`

`NODE_MAJOR=21`

`echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list`

`sudo apt-get update`

`sudo apt-get install nodejs -y`

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

Для начала надо войти в папку **foundryvtt**

`cd foundryvtt`
> [!IMPORTANT]
> Войдите в вашу учетную запись на **https://foundryvtt.com/**, перейти в раздел **Purchased Licenses**, в **Operating System** выбрать **Linux/NodeJS**, затем нажать на кнопку **Timed URL**. В буфер обмена скопируется ссылка.

`wget -O foundry.zip 'ССЫЛКА_КОТОРУЮ_МЫ_ПОЛУЧИЛИ_ВЫШЕ'`

## Распаковка

`unzip foundry.zip`

# Добавление Foundry в PM2

## Настрйока PM2

`pm2 startup`

#### Скопировать и выполнить строку, которая выдаст команда выше, должно получится что-то вроде этого:

`sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu`

> [!WARNING]
> _Не копируйте эту строку, вашу строку вам выдаст комманда выше, это лишь пример_

## Добавить команду запуска Foundry в PM2

`pm2 start "node $HOME/foundryvtt/resources/app/main.js --dataPath=$HOME/foundrydata" --name foundry`

**СЕРВЕР РАБОТАЕТ, ДАЛЬНЕЙШИЕ НАСТРОЙКИ ОПЦИОНАЛЬНЫ, ЕСЛИ ИМЕЕТСЯ СВОЙ ДОМЕН**

# Настройка NGINX

## Установка NGINX

`sudo apt-get install nginx`

## Настройка Firewall

`sudo ufw allow 'Nginx Full'`

> [!NOTE]
> опционально, если еще не сделали это ранее на своем сервере:
> `sudo ufw allow OpenSSH`

`sudo ufw status`

`sudo ufw enable`

`systemctl status nginx`

## Создание конфига

`sudo nano /etc/nginx/sites-available/foundry.example.com`

## Скопировать и вставить блок ниже

``server {``

    # Enter your fully qualified domain name or leave blank
    server_name             foundry.example.com www.foundry.example.com; #ВАШИ ДОМЕНЫ

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

> [!IMPORTANT]
> Заменить `foundry.example.com` на ваш домен.

## "Включить" конфиг
`sudo ln -s /etc/nginx/sites-available/foundry.example.com /etc/nginx/sites-enabled/`

> [!IMPORTANT]
> Заменить `foundry.example.com` на ваш домен.

## Дополнительная настройка
`sudo nano /etc/nginx/nginx.conf`

Найти и расскомментировать (убрать '#') перед строчкой:

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

> [!IMPORTANT]
> Заменить `foundry.example.com` на ваш домен.

## Перезапуск NGINX

`sudo systemctl restart nginx`



## Полезные ссылки

1. [How To Create a Self-Signed SSL Certificate for Nginx in Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-22-04)
2. [NodeSource Node.js Binary Distributions | Installation Instructions](https://github.com/nodesource/distributions#installation-instructions)
3. [Ubuntu VM](https://foundryvtt.wiki/en/setup/hosting/Ubuntu-VM)
4. [Recommended Linux Installation and Usage Guide](https://foundryvtt.wiki/en/setup/linux-installation)

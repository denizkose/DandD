`apt update`
`apt upgrade`

`reboot`

`curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -`
`sudo apt-get install -y nodejs`

`node --version`
`npm --version`

`sudo apt-get install unzip`

`adduser foundry`
`usermod -aG sudo foundry`

`sudo npm install pm2 -g`

`mkdir foundryvtt`
`mkdir foundrydata`

`wget -O foundryvtt.zip 'LINK'`

`unzip foundry.vtt`

`node $HOME/foundryvtt/resources/app/main.js --dataPath=$HOME/foundrydata`

`pm2 start "node $HOME/foundryvtt/resources/app/main.js --dataPath=$HOME/foundrydata" --name foundry`


`sudo apt-get install nginx`

`sudo ufw allow 'Nginx Full'`
`sudo ufw status`
`sudo ufw enable`
`systemctl status nginx`

`sudo nano /etc/nginx/sites-available/foundry.example.com`


`# Define Server
server {

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
}`

`curl -4 icanhazip.com`

`sudo ln -s /etc/nginx/sites-available/foundry.example.com /etc/nginx/sites-enabled/`

`sudo nano /etc/nginx/nginx.conf`


`...
http {
    ...
    server_names_hash_bucket_size 64;
    ...
}
...`

`sudo nginx -t`

`sudo systemctl restart nginx`


`sudo apt install certbot python3-certbot-nginx`


`sudo certbot --nginx -d foundry.example.com -d www.foundry.example.com`
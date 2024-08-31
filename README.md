# deployment



### Installing Node.js, NPM, and Nginx
```ruby
sudo apt-get update -y
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
sudo apt install npm -y
sudo apt install nginx -y

```
### giving access to user 
```ruby
sudo chown username:groupname /path/to/directory_or_file
sudo npm install pm2@latest -g

```
### create nginx file 
```ruby
cd /etc/nginx/sites-enabled/
sudo rm -rf default

sudo vim /etc/nginx/sites-available/<nginx-file-name>

```



### run mongo db locally 
```ruby
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -

sudo apt-get install gnupg

wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list

sudo apt-get update

sudo apt-get upgrade


sudo apt-get install -y mongodb-org


echo "mongodb-org hold" | sudo dpkg --set-selections
echo "mongodb-org-database hold" | sudo dpkg --set-selections
echo "mongodb-org-server hold" | sudo dpkg --set-selections
echo "mongodb-org-shell hold" | sudo dpkg --set-selections
echo "mongodb-org-mongos hold" | sudo dpkg --set-selections
echo "mongodb-org-tools hold" | sudo dpkg --set-selections


sudo systemctl start mongod

sudo systemctl daemon-reload

sudo systemctl status mongod

sudo systemctl enable mongod



sudo systemctl restart mongod



mongosh


### SET MONGO TO ACCESS GLOBALLY

### 1. NEED TO CHANGE IN /etc/mongod.conf

    sudo vim /etc/mongod.conf

    net:
    port: 27017
    bindIp: 0.0.0.0
```

#paste this code to sites-available<site-name>
```ruby
server {
        listen 80;
        listen [::]:80;

        server_name 10min.in www.10min.in;

  location / {
        root /var/www/build;
        index  index.html index.htm;
        try_files $uri $uri/ /index.html;



  }
    location /api/ {
        proxy_pass http://localhost:5001;
 proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;

    }



### Activate the configuration using the following command:
```ruby
sudo ln -s /etc/nginx/sites-available/<nginx-file-name> /etc/nginx/sites-enabled/
```
### Start the Application 
```ruby
sudo systemctl restart nginx
sudo service nginx restart
```

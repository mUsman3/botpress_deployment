# bottpress deployemnt with ssl certificate using letsencrypt

#### Step 1: Clone the Repo
#### Step 2: Change Directory in the directory 
#### Step 3: Run the command 
**docker-compose up -d**
#### Step 4: Go to the browser and verify that either you can see admin page on "your_ip:3000"
###Note: Make sure you have allowd traffice by opening port 3000
#### Step 5: Now Its time to install NGINX
**sudo apt-get update**
**sudo apt-get install nginx**
#### Step 6: Now Start NGINX as A Service
**sudo systemctl start nginx**
#### Step 7: Allow Ports from your systems
**sudo ufw allow http (Port 80)**
**sudo ufw allow https (Port 443)**
#### Step 8: Configure nginx 
**sudo nano /etc/nginx/sites-available/default**
**Add the following to the location part of the server block**
    
    server_name yourdomain.com www.yourdomain.com;
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
#### Step 9: Verify that either configs are successful and restart nginx 
**sudo nginx -t**
**sudo systemctl restart nginx**
#### Step 10: Register you domain from any Domain Registrar and configure with your hosting/server
#### Step 11: Add SSL with letsencrypt 
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com

**Note** Here you will be asked for email and after you have to choose 1 or 2, you need to choose 2 so that it will auto redirect your traffic from http to https

**Only valid for 90 days, test the renewal process with command**
certbot renew --dry-run
---
### Congratulations, You have Configured your Domain and now you can visit your domain
### If you have any issue or questions you can reach me out

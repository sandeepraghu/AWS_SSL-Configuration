# AWS_SSL-Configuration

Pre requisites:
We need to create permission first on the non sudo user
##sudo usermod -aG sudo ubuntu
Setting up a basic firewall
##sudo ufw app list ( it will list all Applications)
##sudo ufw allow OpenSSH  it will open the OPENSSH conncection 
##sudo ufw enable   (command to enable the firewall)
##sudo ufw status  (to check the status of open application)


Installing Certbot
##sudo snap install --classic certbot
##sudo ln -s /snap/bin/certbot /usr/bin/certbot   (it will ensure that the certbot command can run correctly on your server)

Confirming Nginx’s Configuration
##sudo nano /etc/nginx/sites-available/default  (to update the server name )
For example enter the domain name in server field but do not enter *.aisv.in it will not validate enter the exact website name 
...
server_name aisv.in www.aisv.in;
...
 ##sudo nginx -t  (to check what syntax written in nginx is correct)
 ##sudo systemctl restart nginx  ( always restart the server after making any changes in the nginx)
 
 ADD DOMAIN NAME 
 add same domain name in A OR AAA in Route53 or other service you ar using with public IP of your instance otherwise it willl through an error
 
 
 ALLOW HTTPS Through the Firewall
 #sudo ufw status   to check firewall status and running ports
 ##sudo ufw allow 'Nginx Full'  (To let in additional HTTPS traffic, allow the Nginx Full profile)
#sudo ufw delete allow 'Nginx HTTP'  ( delete the redundant Nginx HTTP profile if exist )
#sudo ufw status   (to confirm that it has been added)


OBTAINING an SSL Certificate

##sudo certbot --nginx -d aisv.in
(It will ask for a email id provide the email id and you will get a success message)


AUTO RENEWAL OF CERTBOT
##sudo certbot renew --dry-run  #it it runs successfully it will update CERTFOT CERTIFICATE when needed 


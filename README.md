### How to install on Digital Ocean
Completed November 2019 by Raymond Ao

SSH: username=root, password=TotalDealer2019
Strapi admin: username=totaldealer, password=TotalDealer2019
DB superuser role name: totaldealer
DB name: totaldealer


1. Clone Strapi starter from raymond53892 github and develop server
2. Clone the Strapi app to deply onto to the digital ocean server at ~ (/root/)
3. Create a database for the app (sudo -u postgres createdb [dbname])
4. Create a new linux user with the same name and role as the database (sudo adduser [username]). Note down name and password
5. If forgot database password, run the following: sudo -u postgres psql --> ALTER USER your-name PASSWORD 'password'; --> \q
6. sudo nano ./config/environments/production/server.json and specify the desired port for the application. Note this, and ensure that it does not conflict with other applications.
7. cd ~, then sudo nano ecosystem.config.js, and create another object for the new process, importing database details including host, port, database name, database username, and database password
8. cd ~, then pm2 start ecosystem.config.js to start the processes
9. pm2 startup systemd to make the processes run automatically on startup
10. pm2 save
11. Create an nginx server block: sudo nano /etc/nginx/sites-available/default (only need to do this if you want to use a subdomain)
12. sudo systemctl restart nginx
13. Allow the port using: sudo ufw allow 1337/tcp (replace 1337 with the port).

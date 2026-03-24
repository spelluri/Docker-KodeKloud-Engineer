1. check for existing containers and images 
docker ps 
docker images 
2.  access  the container kkloud 
docker exec -it kkloud /bin/bash
3. after loggin to kkloud container do the system update and install apache 2
apt update 
apt install -y apache2
4. change the listening port to 6100 
Apache's default port is defined in the ports.conffile. You need to change 80to 6100.
4.a. Open the configuration file:
sed -i 's/Listen 80/Listen 6100/' /etc/apache2/ports.conf
4.b. Update the Default VirtualHost
sed -i 's/<VirtualHost \*:80>/<VirtualHost *:6100>/' /etc/apache2/sites-enabled/000-default.conf
5. start the service and verify
service apache2 start
netstat -tuln | grep 6100  or curl -I localhost:6100
6. Once you have verified the service is running, you can exit the container shell
exit
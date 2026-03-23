docker stop nautilus
docker rm nautilus
docker run -d --name nautilus -p 8085:80 -v /var/www/html:/usr/local/apache2/htdocs httpd:latest

Investigation :
1. checked for the voulme mount :
docker inspect -f '{{ json .Mounts }}' nautilus 

found that the volume was correctly mounted .

2. checked for port mapping 
docker inspect -f '{{ .NetworkSettings.Ports }}' nautilus

found that there was no port mapping done at all . 

3. So had to stop , remove the existing faulty container and create a new one with correct port mapping and mount volumes .
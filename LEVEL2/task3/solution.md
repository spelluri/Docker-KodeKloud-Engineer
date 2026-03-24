1. check cureent docker images and containers .
docker images 
docker ps 
2. stop the ubuntu_latest container .
docker stop ubuntu_latest 
3. create a new image from existingcontainer ubuntu_latest
docker commit ubuntu_latest official_devops
4. start ubuntu_latest container again and check .
docker start ubuntu_latest 
docker ps 

Note :

1. when you create a brand new docker container use docker run .
2. when you create a new image from an existing container use docker commit .

Comparision of commands 

docker run       image->container    starts a new process from a template 
docker commit    container->image    creates a template from a modified container process.
docker build     dockerfile->image   creates a template from a written script 

The lifecycle flow:
Here i show the logic flows for this specific devops task :
1. original state : you have an image (eg:ubuntu)
2. working state : you use docker run to create the container ubunut_latetst . The developer makes changes here .
3. Saving State : you use docker commit to save those manual changes into a new image called official:devops.
4. future state : now you can use docker run oficial:devops to start a new container that already has all of those developer changes inside it.
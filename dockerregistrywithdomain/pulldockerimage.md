# Pull Docker image from docker registry
If we want to pull docker image we need credentials of docker registry
First we need to login and then pull image

login into docker:
--------
    docker login nexus.vamsitechtuts.tk
    Username: admin
    Password: admin123
![4](https://user-images.githubusercontent.com/63221837/83323167-9e135b80-a27a-11ea-80fe-7811944723da.png)
pull docker image from docker registry:
-----------
    docker pull nexus.vamsitechtuts.tk/dockerrepo/nginx
 ![1](https://user-images.githubusercontent.com/63221837/83323528-0bc08700-a27d-11ea-9d45-cfa23700178b.png)

# Push docker image to docker registry
To push docker image to docker registry we need to create docker repository with in the docker registry
Goto Docker Registry and click on settings
![1](https://user-images.githubusercontent.com/63221837/83322866-9357c700-a278-11ea-8cac-2f42b7062868.png)

click on Repostitories

![2](https://user-images.githubusercontent.com/63221837/83322867-9357c700-a278-11ea-9f19-8f30deeba34a.png)

Click on Create Repository

![3](https://user-images.githubusercontent.com/63221837/83322905-d023be00-a278-11ea-949e-de01d28e9260.png)

Click on docker(hosted)

![4](https://user-images.githubusercontent.com/63221837/83322907-d0bc5480-a278-11ea-8535-0faaf91f8ea6.png)

Give details as shown in figure and Click on Create Repository

![1](https://user-images.githubusercontent.com/63221837/83322985-3f99ad80-a279-11ea-84d8-fee1ced5026d.png)

Now go to command line interface and pull "Nginx" image:
---------
    docker pull nginx
![1](https://user-images.githubusercontent.com/63221837/83323185-aec3d180-a27a-11ea-9979-550f7e20617d.png)

Push docker image to our docker registry:
--------------
We need to login to our docker registry

    docker login nexus.vamsitechtuts.tk
    Username: admin
    Password: admin123
![4](https://user-images.githubusercontent.com/63221837/83323167-9e135b80-a27a-11ea-80fe-7811944723da.png)
Now we need to tag docker image with docker registry

    docker tag nginx:latest nexus.vamsitechtuts.tk/dockerrepo/nginx:latest

Check docker images:

    docker images
![2](https://user-images.githubusercontent.com/63221837/83323211-d0bd5400-a27a-11ea-9241-d8ff7fa7fbf7.png)
Now we need to push to our docker registry

    docker push nexus.vamsitechtuts.tk/dockerrepo/nginx:latest
![5](https://user-images.githubusercontent.com/63221837/83323168-9f448880-a27a-11ea-95d4-4729607efb8d.png)

Now we can image with in docker registry
---------
![1](https://user-images.githubusercontent.com/63221837/83323305-7cff3a80-a27b-11ea-9a55-c978cd6dbefa.png)


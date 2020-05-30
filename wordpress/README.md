Pre-requisites:
-------
    - Install Java
    - Install Git
    - Install Docker
    - Install Docker-Compose
Install Java:
------
    yum install java-1.8.0-openjdk-devel -y
Install Git:
-------
    yum install git -y
Install Docker:
------
    yum install docker -y
    service docker start
Install Docker-Compose
------
    sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
    docker-compose --version
Clone code from github:
-------
    git clone https://github.com/Naresh240/docker.git
    cd docker/wordpress
Deploy wordpress using docker compose:
-----------
    docker-compose up -d
Check docker container:
-----
    docker ps 
Allow 8000 Port Number with in security group:
--------------
![1](https://user-images.githubusercontent.com/63221837/82864052-3ccd4e80-9f41-11ea-9956-0221eb9622c0.png)
Goto Web UI and check whether its working or not:
---------------
![2](https://user-images.githubusercontent.com/63221837/82870059-f4b42900-9f4c-11ea-991e-417828123aa4.png)
Provide details which it require
![4](https://user-images.githubusercontent.com/58024415/82871299-fa127300-9f4e-11ea-8634-45cbdefc583b.png)
Click on Install Wordpress
![4](https://user-images.githubusercontent.com/63221837/82870382-799f4280-9f4d-11ea-8f86-ff9eb0a4b0ee.png)
Click on Log In
![5](https://user-images.githubusercontent.com/58024415/82871412-26c68a80-9f4f-11ea-8041-1c47b42a6b74.png)
Give Username and Password then click on LoginIn
![6](https://user-images.githubusercontent.com/58024415/82871514-537aa200-9f4f-11ea-9260-defc79e50d1d.png)
CleanUP:
------
    docker-compose down

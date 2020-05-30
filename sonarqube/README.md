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
    cd docker/sonarqube
Deploy wordpress using docker compose:
-----------
    docker-compose up -d
Check docker container:
-----
    docker ps
Allow Port Number:9000 with in the security group:
--------------
![2](https://user-images.githubusercontent.com/58024415/82880310-ddc90300-9f5b-11ea-8a05-00deb9c1c7d0.png)
Goto WebUI and Check whether we get sonarqube or not:
-------------
    http://100.26.120.230:9000/
![1](https://user-images.githubusercontent.com/58024415/82880366-f2a59680-9f5b-11ea-94ee-b12d5c342f7a.png)
Credentials:
--------
    Username: admin
    Password: admin
CleanUP:
------
    docker-compose down

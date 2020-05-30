Pre-requisites:
-------
Docker Swarm Master:
    
    - Install Java
    - Install Git
    - Install Maven
    - Install Docker
Docker Swarm Node server:
    
    - Install Docker
How to Create Docker Swarm Cluster:
-------
Goto master server and give below command:
    
    docker swarm init
Here we get token. This token we need to give in node servers

Goto node server and give token which we get in master:
	
    docker swarm join --token SWMTKN-1-3f3587of2i73u16owsc8uly9ji0simkj36358dezuatged6fy7-cj2b280qw1yxr5yoheb9kemlu 172.31.80.230:2377
Check nodes in Master server:
	
    docker node ls
Install Java:
------
    yum install java-1.8.0-openjdk-devel -y
Install Git:
-------
    yum install git -y
Install Apache-Maven:
-------------
    wget https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
    tar xvzf apache-maven-3.6.3-bin.tar.gz
    
    vi /etc/profile.d/maven.sh
    --------------------------------------------
    export MAVEN_HOME=/opt/apache-maven-3.6.3
    export PATH=$PATH:$MAVEN_HOME/bin
    --------------------------------------------
	
    source /etc/profile.d/maven.sh
    mvn -version

Install Docker:
------
    yum install docker -y
    service docker start

Clone code from github:
-------
    git clone https://github.com/Naresh240/docker.git
    cd docker/employee-jdbc-dockerswarm  
Build Maven Artifact:
-------
    mvn clean install
Build Docker image for Springboot Application
--------------
    docker build -t naresh240/employee-jdbc-dockerswarm:latest .
Docker login
-------------
    docker login
Push docker image to dockerhub
-----------
    docker push naresh240/employee-jdbc-dockerswarm:latest
Deploy employee-jdbc application on Master server:
-----------
    docker stack deploy --compose-file deploy-stack.yml employee-jdbc
Check docker container:
-----
    docker ps 
Connect to mysql container and Create employeee table:
-------------
    docker exec -it <containerid> /bin/bash
    mysql -u naresh -p
    create table employee(empId varchar(40), empName varchar(40));
POST Method you can check in POSTMAN App:
-------
    http://100.25.181.219:8080/insertemployee
![1](https://user-images.githubusercontent.com/58024415/82552146-2ad55f80-9b7f-11ea-9526-89ea01e4fb6b.png)
GET Method you can check in WebUI(Using with Master Server):
---------
    http://100.25.181.219:8080/employees
![2](https://user-images.githubusercontent.com/58024415/82552150-2c068c80-9b7f-11ea-89d5-e93074704d92.png)
GET Method you can check in WebUI(Using with Node Server):
---------
    http://100.26.221.44:8080/employees
![3](https://user-images.githubusercontent.com/58024415/82557071-9ff96280-9b88-11ea-852f-ce5b8dd1693f.png)
CleanUP:
------
    docker stack rm employee-jdbc

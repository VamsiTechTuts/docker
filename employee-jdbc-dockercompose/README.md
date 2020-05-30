Pre-requisites:
-------
    - Install Java
    - Install Git
    - Install Maven
    - Install Docker
    - Install Docker-Compose
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
Install Docker-Compose
------
    sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
    docker-compose --version
Clone code from github:
-------
    git clone https://github.com/Naresh240/docker.git
    cd docker/employee-jdbc-dockercompose  
Build Maven Artifact:
-------
    mvn clean install
Build Docker image for Springboot Application
--------------
    docker build -t naresh240/employee-jdbc-dockercompose .
Docker login
-------------
    docker login
Push docker image to dockerhub
-----------
    docker push naresh240/employee-jdbc-dockercompose
Check docker container:
-----
    docker ps 
Connect to mysql container and Create employeee table:
-------------
    docker exec -it <containerid> /bin/bash
    mysql -u naresh -p
    create table employee(empId varchar(40), empName varchar(40));
Deploy employee-jdbc application using docker run command:
-----------
    docker-compose up -d
POST Method you can check in POSTMAN App:
-------
    http://100.25.181.219:8080/insertemployee
![1](https://user-images.githubusercontent.com/58024415/82552146-2ad55f80-9b7f-11ea-9526-89ea01e4fb6b.png)
GET Method you can check in WebUI:
---------
    http://100.25.181.219:8080/employees
![2](https://user-images.githubusercontent.com/58024415/82552150-2c068c80-9b7f-11ea-89d5-e93074704d92.png)
CleanUP:
------
    docker-compose down

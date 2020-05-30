Pre-requisites:
-------
    - Install Java
    - Install Git
    - Install Maven
    - Install Docker
    - Install Mysql
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
Install Mysql:
-----
    wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
    yum localinstall mysql57-community-release-el7-11.noarch.rpm -y
    yum install mysql-community-server -y
    systemctl start mysqld.service
Here we get pwd
---
    cat /var/log/mysqld.log
Mysql Login
----
    mysql -u root -p
Change password for root user:
--------
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'Test#240';
Create User and Provide Remote access:
-----------
    create user 'vamsitechtuts'@'localhost' IDENTIFIED BY 'Test#240';
    GRANT ALL PRIVILEGES ON *.* TO 'vamsitechtuts'@'localhost' WITH GRANT OPTION;
    create user 'vamsitechtuts'@'%' IDENTIFIED BY 'Test#240';
    GRANT ALL PRIVILEGES ON *.* TO 'vamsitechtuts'@'%' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
Create Database in Mysql:
------
    CREATE DATABASE mysqldb;
    USE mysqldb;
Create Table:
-----
    create table employee(empId varchar(40), empName varchar(40));

Clone code from github:
-------
    git clone https://github.com/Naresh240/docker.git
    cd docker/employee-jdbc-docker   
Build Maven Artifact:
-------
    mvn clean install
Build Docker image for Springboot Application
--------------
    docker build -t vamsitechtuts/employee-jdbc-docker .
Docker login
-------------
    docker login
Push docker image to dockerhub
-----------
    docker push vamsitechtuts/employee-jdbc-docker
Deploy employee-jdbc application using docker run command:
-----------
    docker run --name employee-jdbc-docker -p 8080:8080 -d vamsitechtuts/employee-jdbc:latest
POST Method you can check in POSTMAN App:
-------
    http://100.25.181.219:8080/insertemployee
![1](https://user-images.githubusercontent.com/58024415/82552146-2ad55f80-9b7f-11ea-9526-89ea01e4fb6b.png)
GET Method you can check in WebUI:
---------
    http://100.25.181.219:8080/employees
![2](https://user-images.githubusercontent.com/58024415/82552150-2c068c80-9b7f-11ea-89d5-e93074704d92.png)

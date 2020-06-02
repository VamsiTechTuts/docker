# spring-boot-hello

Pre-requisites:
-----
    - Install Java
    - Install GIT
    - Install Maven
    - Install Docker
    - Install Nexus
Allow ports in first server:
--------
![2](https://user-images.githubusercontent.com/63221837/83428679-7d046380-a450-11ea-849d-69ee87a3e9ab.png)
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
Installation of Nexus:
-----------------
Download nexus tar file:
	  
    cd /opt
    wget https://sonatype-download.global.ssl.fastly.net/nexus/3/nexus-3.0.2-02-unix.tar.gz
Extract tar file:

    tar xvzf nexus-3.0.2-02-unix.tar.gz
Change name of Nexus file:
	
    mv nexus-3.0.2-02 nexus
Add nexus user: 
	  
    useradd nexus
Change owner ship for nexus file:
	  
    chown -R nexus:nexus nexus
Open /opt/nexus/bin/nexus.rc file and update data like as below:
    
    vi /opt/nexus/bin/nexus.rc
    run_as_user="nexus"

Make Soft link:

    ln -s /opt/nexus/bin/nexus /etc/init.d/nexus
Login to nexus user:
  
    su - nexus
Start nexus server:

    service nexus start
Check status of nexus:

    service nexus status
Open Web UI and check whether docker private registry open with domain name or not:
------------
	http://54.82.177.131:8081/
![1](https://user-images.githubusercontent.com/63221837/83426599-03b74180-a44d-11ea-8c18-c71674a93723.png)

Sign in details:
--------
    Username: admin
    Password: admin123
![2](https://user-images.githubusercontent.com/63221837/83426601-04e86e80-a44d-11ea-9278-21d9b0d48230.png)
Create docker Repository with docker registry:
---------
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

![1](https://user-images.githubusercontent.com/63221837/83427110-d4550480-a44d-11ea-95c1-2a166f3b8381.png)

Now create "/etc/docker/daemon.json" file and keep data like as show below
--------------
	vi /etc/docker/daemon.json
	-----------------------------------------------------
	{ "insecure-registries" : [ "54.82.177.131:5000" ] }
	------------------------------------------------------
Then Reastart Docker:
--------
	service docker restart

Clone code from github:
-------------
    git clone https://github.com/Naresh240/spring-boot-hello.git
    cd pring-boot-hello
Build Maven Artifact:
------------
    mvn clean install
Build Docker image for Springboot Application:
------------
    docker build -t spring-boot-hello:latest .
Docker login:
-------
    docker login http://54.82.177.131:5000
Tag docker image with docker registry:
-------------
    docker tag spring-boot-hello:latest 54.82.177.131:5000/dockerrepo/spring-boot-hello:latest
Push docker image to dockerhub:
--------
    docker push 54.82.177.131:5000/dockerrepo/spring-boot-hello:latest
Check whether the image pushed to docker registry or not:
-------------
![1](https://user-images.githubusercontent.com/63221837/83427951-2cd8d180-a44f-11ea-8b65-21b595361288.png)

Now pull docker image from another server:
------------
Allow ports with in 2nd server
![2](https://user-images.githubusercontent.com/63221837/83429055-19c70100-a451-11ea-9eb3-f5833c03027b.png)

Install docker with in second server also.
Now create "/etc/docker/daemon.json" file and keep data like as show below

	vi /etc/docker/daemon.json
	-----------------------------------------------------
	{ "insecure-registries" : [ "54.82.177.131:5000" ] }
	------------------------------------------------------
Then Reastart Docker:
--------
	service docker restart
Docker login:
-------
    docker login http://54.82.177.131:5000
Pull docker image:
--------
    docker pull 54.82.177.131:5000/dockerrepo/spring-boot-hello
Run spring-boot application with in 2nd server:
----------
    docker run --name spring-boot-hello -p 80:8080 -d 54.82.177.131:5000/dockerrepo/spring-boot-hello:latest
Goto web UI and check output of spring boot application:
-------
    http://52.3.244.222/
![1](https://user-images.githubusercontent.com/63221837/83429057-1a5f9780-a451-11ea-89ca-49ea14579d2e.png)

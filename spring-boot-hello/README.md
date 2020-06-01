# spring-boot-hello

Pre-requisites:
-----
    - Install Java
    - Install GIT
    - Install Maven
    - Install Docker
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

![1](https://user-images.githubusercontent.com/63221837/83322985-3f99ad80-a279-11ea-84d8-fee1ced5026d.png)

Clone code from github:
-------------
    git clone https://github.com/Naresh240/spring-boot-hello.git
    cd pring-boot-hello
Build Maven Artifact:
------------
    mvn clean install
Build Docker image for Springboot Application:
------------
    docker build -t naresh240/spring-boot-hello:latest .
Docker login:
-------
    docker login
Push docker image to dockerhub:
--------
    docker push naresh240/spring-boot-hello:latest

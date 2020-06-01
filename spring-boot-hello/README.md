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
Install Docker:
------
    yum install docker -y
    service docker start
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

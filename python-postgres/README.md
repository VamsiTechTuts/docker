## python-postgres-dockercompose

Pre-requisites:
------
    - Install Git
    - Install Docker
    - Install Docker-compose
Clone SCM from Git:
------
    git clone https://github.com/Naresh240/docker.git
    cd docker/python-postgres-dockercompose
Build docker image:
-------
Now, to get the containers running, build the images and then start the services:
    
    docker-compose build
Start all the containers

    docker-compose up -d
![1](https://user-images.githubusercontent.com/58024415/82636589-94f21100-9c20-11ea-86c6-76f612b18473.png)
Check Stopped and Running containers:
![2](https://user-images.githubusercontent.com/58024415/82636580-928fb700-9c20-11ea-8941-a909e3b1c360.png)
Output to this command will show all the four containers coming up
Connect to PostgreSQL:
----------
    docker exec -it 0a9318b906ef /bin/bash
    psql -U postgres --password
default password: postgres
![3](https://user-images.githubusercontent.com/58024415/82636583-93c0e400-9c20-11ea-9b10-8b8faa648825.png)
Check Database Tables:
![4](https://user-images.githubusercontent.com/58024415/82636585-93c0e400-9c20-11ea-9c2b-aaa6ebb997f6.png)
Create Database Table:
---------
We also need to create the database table:
    
    docker-compose run web /usr/local/bin/python create_db.py
Once connected to the DB you can run the following command to see the table created
![5](https://user-images.githubusercontent.com/58024415/82636587-94597a80-9c20-11ea-9835-e0d494c50298.png)
Open your browser and navigate to the IP address:
    http://34.229.71.50/
![6](https://user-images.githubusercontent.com/58024415/82636588-94597a80-9c20-11ea-8be5-0d83e85b3e64.png)

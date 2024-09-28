# How to run MS SQL Server on Mac

If you want to practise your SQL skills this guide will help you to get started with microsoft adventure works database on SQL Server.
This is a step by step guide for running SQL Server on M1 or latest Mac using azure-sql-edge Docker image.
Follow these steps:

## 1 - Download Docker Desktop

## 2 - Download Azure Data studio

## 3 - Open terminal and run this command: 'docker pull mcr.microsoft.com/azure-sql-edge' this will pull/download container image to local machine

## 4 - Once the download is completed, run the following command to launch an instance of the Docker image you just downloaded: 
    'sudo docker run --cap-add SYS_PTRACE -e 'ACCEPT_EULA=1' -e 'MSSQL_SA_PASSWORD=bigStrongPwd' -p 1433:1433 --name sqledge -d mcr.microsoft.com/azure-sql-edge'

## 5 - Be sure to change bigStrongPwd in the above command to a strong password of your choice. You can also change the value of the --name parameter if you wish.
    By default, the container is run with the Developer Edition. You can run the Premium Edition by adding -e 'MSSQL_PID=Premium'.

## 6 - To start a container use this command in cmd 
    
    '''docker container start <containername>''' 
    
    (if you already have the container setup, in our case container name is sqledge) 

    '''docker container start sqledge'''

    To stop a container use 
    
    '''docker container stop <containername>'''

    type 'docker ps' to confirm the container is running, also in docker desktop you can see the container running

## 7 - Go to Azure Data Studio to connect to the sqledge server [alt text](image.png)
    Server Name: localhost
    Authentication Type: SQL Login
    User name: sa
    Password: reallyStrongPwd123
    Database Name: <default>
    Server Group: <default>

## 8 - Run 'SELECT @@VERSION' to make sure the connection is up and running you will get the SQL Server version in result

## 9 - Now you have SQL Server up and running, you can either create your own database or download a database

## 10 - Go to https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms 
     Download AdventureWorks2019.bak 
     Run the command below in terminal 
     docker cp PATH containerid:/var/opt/mssql/data/
     replace PATH and containerid with the right values
     docker cp ~/Downloads/AdventureWorks2019.bak 8a4231a51bad5e1c91f771809f0f263a379ce9c767e72672ca69152852e47c43:/var/opt/mssql/data/

## 11 - After this refresh connection in Azure data studio and right click on database and click on restore database
     Select restore from backup file
     Select file from path and click restore
     After restore is finished you should see AdventureWorks under databases, thats it you can open a query editor and start writing sql!

### Resource:
-  https://hub.docker.com/r/microsoft/azure-sql-edge
-  https://database.guide/how-to-install-sql-server-on-an-m1-mac-arm64/
-  https://database.guide/how-to-install-sql-server-on-a-mac/

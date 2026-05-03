# Studing Docker Container concept:

### Note: For a reference we have take MERN as a project setup:
1. Docker Container

	1. Docker Hub 
	```
 	docker login 
	docker tag rchirutkar:v1.0 rchirutkar/batch16a
	docker push rchirutkar/batch16a:v1.0

 	#v1.0: Pulling from prashantdey/batch16atm
 	docker pull prashantdey/batch16atm:v1.0 

	#Build image
 	docker build -t node-backend .

 	#AWS
 	aws configure
	aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/m8f3cbp5

 	docker run -d -p 27019:27017 mongo
	```
 
 	2.  Docker Volume
	#Docker Volume for persistent storage
	```
	 docker volume create mongodata
	 docker volume ls
	 docker volume inspect mongodata
	 docker volume rm mongodata => remove mongodata
	 docker volume prune => auto delete unused data
	 docker run -d -p 27019:27017 -v1 mongodata:/data/db mongo
    ```
 	3. Data backup
    ```
	 docker run --rm -v mongodata  => 
	 docker run -v D:\project\docker\myproject:app/data mongo => bind mount to local computer to copy any file from container
	 docker run -it -v D:\teaching\batch16A\dockerLearning\TravelMemory:/app/data mongo bash => to access container from local machine in terminal
	```
    4. Mounting and mapping db dir and local dir in mongo container
 	```
	 docker run -v mongodata:/data -v D:\teaching\batch16A\dockerLearning\TravelMemory:/app/data mongo => 
	 
	 docker exec -it <container_id> bash | tar -czf /data > backup.tar.gz | cp backup.tar.gz /app/data/
	 docker run --rm -v mongodata:/data -v D:\teaching\batch16A\dockerLearning\TravelMemory:/backup mongo sh -c "cd /data && tar czf /backup/mongodata-backup.tar.gz ."
	 docker run --rm -v mongovolume:/data   -v "/$(pwd)":/backup   busybox   sh -c "cd /data && tar czf /backup/mongodata-backup.tar.gz ."
	 docker run --rm -v mongodb:/data/db -v ${PWD}:/backup mongo tar -czvf /backup/mongodb_backup1.tar.gz -C /data db
	 docker run --rm -v mongodata:/data:ro -v /Users/sairaavi/Documents/MyLearnings/DevOps/projects/MERN/TravelMemory:/app/data alpine tar -czvf /app/data/mongodata-backup.tar.gz -C /data .
    ```
   
2. Docker Network
     1. Bridge Network is default nw type in docker
      	when we create container it uses Bridge network by default. there is also custom network available to use.
      	It is single host and every single host try to connect with bridge network. It is in same host.
	```
		docker network create b16a_tm
		docker run -d -p 8081:80 --name nginx_b16a_nw --network b16a_tm nginx
		docker run -d --name busybox_b16a_nw --network b16a_tm sleep 3600 bash
		ping nginx_b16a_nw:8081
	```
	
      2. Host Network: Host computer OS network.
	```
		docker run --network host nginx
	```
		
      4. None Network (No network) : to create a process running in container isolated from network we use none network. for eg. create a thumbnail.
	```
		docker run --network none nginx                                       
	```
		
      6. Overlay - used for swarm / outdated
         When container run with multiple docker use Overlay docker. Docker swarm is manage VM. Kubernet created by Google and it is gaining popularity than Docker swarm. Now Docker new version comes with kubernates. It is for diff host connectivity
        	
      7. MacVLan network:
	 ```
	 	docker network crate -d macvlan --subnet 192.168.1.0/24 --gateway 192.168.1.1 -o parent=eth0 macvlan-net
	 ```
3. Docker Compose

   
4. Docker MCP

   
5. Interaction with AI (GPT)

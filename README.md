# Studing Docker Container concept:

### Note: For a reference we have take MERN as a project setup:
1. Docker Container
2. Docker Network
     1. Bridge Network is default nw type in docker
      	when we create container it uses Bridge network by default. there is also custom network available to use.
      	It is single host and every single host try to connect with bridge network. It is in same host.
        - docker network create b16a_tm
      	- docker run -d -p 8081:80 --name nginx_b16a_nw --network b16a_tm nginx
      	- docker run -d --name busybox_b16a_nw --network b16a_tm sleep 3600 bash
      	- ping nginx_b16a_nw:8081
	
      2. Host Network 
        	Host computer OS network
        	docker run --network host nginx
        	
      3. None Network
        	No network : to create a process running in container isolated from network we use none network. for eg. create a thumbnail 
        	docker run --network none nginx
        	
      4. Overlay - used for swarm / outdated
        	When container run with multiple docker use Overlay docker. Docker swarm is manage VM. Kubernet created by Google and it is gaining popularity than Docker swarm. Now Docker new version comes with kubernates. It is for diff host connectivity
        	
      5. MacVLan network: 
        	docker network crate -d macvlan --subnet 192.168.1.0/24 --gateway 192.168.1.1 -o parent=eth0 macvlan-net

3. Docker Compose
4. Docker MCP
5. Interaction with AI (GPT)

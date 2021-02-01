Credit: (https://github.com/mbzama)
 
 ## Installation
Please refer to this repo for instructions: [docker-setup](https://github.com/mbzama/docker-setup)
   
      
## Cheatsheet

  To view active containers
  
	   docker ps 
	
  To view all containers
  
	   docker ps -a
	
  To view images
  
	   docker images

  To remove container
  
	   docker rm -f {container_name}
	
  To remove image
  
	   docker rmi --image {image_name}
    

  To view logs
  
       docker logs -f {container_name}
       docker logs -f {container_name} --tail 100

  To clean up un-used resources
  
	   docker system prune
       
For more commands please refer to this [cheatsheet](https://github.com/mbzama/docker-training/blob/master/docker-cheatsheet.pdf)
     
     
       
## Working with Volumes
Create folder and file

	     mkdir data
	     nano run.sh
	
    
Add this content 

	echo '<EMP_ID> Running run.sh file - '$(date)
    
	
Copy from Host machine to Docker Container:

    docker cp /host_dir container_name:/container_dir
    

Copy from Docker Container to Host machine:

    docker cp container_name:/container_dir /host_dir
   
    Example:
    	Copy file from host machine to container 
	   		docker cp data/ container_name:/data	
	
     	Login to the docker container
	   		docker exec -it container_name
	
     	Verify the file
	   		ls -l data
	   		cat data/run.sh
	
     	Run the file
	   		sh run.sh
 


## Upload image to public registry (dockerhub)

   1. Create account in [Docker Hub](https://hub.docker.com) using your personal email. 
   
                  	
  2. Login to dockerhub registry from command prompt using this command:
  
	      docker login --username={user_name} 

  3. Tag the image
  
	     docker tag {image_name} {user_name}/{image_name}

  4. Upload the image to public docker registry:
  
	     docker push {user_name}/{image_name}
	     

--------------------------------------------------------------
ALL PROJECTS
--------------------------------------------------------------
-------------
1_standalone
-------------
     -------------
     Build binary
     -------------
         cd 1_standalone
         mvn clean compile jar:jar

     -------------
     Run binary
     -------------
          java -jar target/standalone-1.0.jar

     -------------
     Build docker image
     -------------
          Java 8
               docker build -t java8-app .

          Java 9 
               docker build -f Dockerfile-9 -t java9-app .

          Java 10 
               docker build -f Dockerfile-10 -t java10-app .

          Java 11
               docker build -f Dockerfile-11 -t java11-app .

     -------------
     Run app as Docker container
     -------------
          Java 8
               docker run --name java8-app-c1 java8-app 

          Java 9
               docker run --name java9-app-c1 java9-app

          Java 10
               docker run --name java10-app-c1 java10-app

          Java 11
               docker run --name java11-app-c1 java11-app		


-------------
2_spring-boot
-------------
     -------------
     Build the executable
     -------------
     cd 2_spring-boot
     mvn -DskipTests=true package && java -jar target/spring-boot-demo-1.0.jar
       
     Access the app using
        Windows: http://192.168.99.100:8085/greet?name=zama
        Ubuntu : http://localhost:8085/greet?name=zama

     -------------
     Build docker image
     -------------
     docker build -t spring-boot-demo .

     -------------
     Run app as Docker container
     -------------
     docker run -p 9999:8085 --name springboot-c1 spring-boot-demo
       
     Access the app using
       Windows: http://192.168.99.100:9999/greet?name=zama 
       Ubuntu : http://localhost:9999/greet?name=zama

  

-------------
Using Maven for docker tasks
-------------
We can use `dockerfile-maven` plugin from spotify for build/tag/publish docker images 

To build and tag image
  
    mvn dockerfile:build
    
To deploy or publish image
    
    mvn dockerfile:push
        


-------------
Docker Compose
-------------

To build and start:

	docker-compose up --build


To build:

	docker-compose build


To create/run containers:

	docker-compose up


To stop containers:

	docker-compose stop
	
	
To stop and remove all containers:

	docker-compose down


To start particular service:

	docker-compose up {service_name}

-------------
Scaling
-------------
We can scale the containers easily using docker-compose

        For standalone:
               docker-compose scale standalone=5


-------------
Upload image to public docker registry (dockerhub)
-------------
   Please refer to [this](https://github.com/mbzama/docker-training/blob/master/README.md#upload-image-to-public-registry-dockerhub)
   

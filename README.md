

Demo 1 : 

Objectives : 
- Getting started with a basic app.
- Run it using docker run
- See the result in browser
- Discover basic ways to launch / stop containers

Basic app python app running on port 5000 
Uses Redis for cache data persistance on port 6379

	- Launch the app
	// Go to demo-1 folder
	cd Desktop/Docker/demo-1

	// Build the image
	//This will use by default the Dockerfile in the current directory
	docker build -t "simple_flask:dockerfile" .

	
	// Run the container
 	docker run -p 5000:5000 simple_flask:dockerfile python app.py
 		
	- Look at running containers : 
	docker ps
	// There should be 1 containers :  app.py, from the image simple:flask
	// Discuss the ports opened in relation to the Dockerfile and the docker-compose files
	
	- Open a browser and go to localhost:5000
	// Error : no redis container running
	
	- We need to run a container for redis
	HELP HERE : the container is created and immediatly stops??
	docker run --name redis-instance -d redis redis:alpine -p 6379:6379
	
	- Look at running containers : 
	docker ps
	// There should be 2 containers :  app.py and redis:alpine
	
Once container is launched, go to localhost:5000 to increment a count and display the result

	- Stop all running containers
	docker stop $(docker ps -a -q)
	
	- Look at running containers
	// Should be none
	
	- Look at all containers
	docker ps -a
	// Should be our containers in the Exit state
	
	- Go back to localhost:5000 to see that nothing is running there




Demo 2 :

Objectives : 
- Use docker-compose
- Show how it is easier than the previous one

	- Launch the app
	// Go to demo-2 folder
	cd ../demo-2
	
	- Show / Discuss docker-compose file
	// HELP HERE : what to say??

	// Run the containers using docker-compose
	docker-compose up

	
	// Run the container
 	docker run -p 5000:5000 simple_flask:dockerfile python app.py
 		
	- Look at running containers : 
	docker ps
	// There should be 1 containers :  app.py, from the image simple:flask
	// Discuss the ports opened in relation to the Dockerfile and the docker-compose files
	
	- Open a browser and go to localhost:5000
	// Error : no redis container running
	
	- We need to run a container for redis
	HELP HERE : the container is created and immediatly stops??
	docker run --name redis-instance -d redis redis:alpine -p 6379:6379
	
	- Look at running containers : 
	docker ps
	// There should be 2 containers :  app.py and redis:alpine
	
Once container is launched, go to localhost:5000 to increment a count and display the result

	- Stop all running containers
	ctrl+C
	
	- Go back to localhost:5000 to see that nothing is running there
	
	- Restart all containers : 
	docker restart $(docker ps -a -q)
OR  docker-compose up
	// Show in the output that images are not totally rebuilt? 

	- See that the cache was flushed (count to 0)
	//HELP HERE : why is cache not flushed if I stop/restart the containers using docker stop then docker restart??
	
	
	
	
Demo 3 :	

Objectives :
- Show version upgrade / image change

	- Clear containers
	docker rm $(docker ps -a -q)
	// Can show that of containers are running, this will display error
	OR 
	docker container prune
	// This will display a warning and delete only stopped containers
	
	- Update docker-compose.yml
	Change reddis:apline -> reddis
	// Will take latest by default
	
	- Run the containers
	docker-compose up
	// Show output : new container is created
	
	- list all containers
	// Show output : old container reddis:alpine is not here. It was updated when we updated our yml file
	
	- Show on localhost:5000 that all works fine
	
	
Demo 4 : 

Objectives : Edit the Compose file to add a bind mount

	- Clear existing containers
	docker stop $(docker ps -a -q)
	docker prune
	y
	
	- Show updated docker-compose.yml file
	// Point out the added Volume
	
	- Rebuild using docker-compose
	docker-compose up
	
	- Go to localhost:5000
	// Show expected result
	
	- Go update the app.py file
	// Hello World -> Hello Olympp
	// cache.incr('hits') -> cache.incr('hits', 2)
	
	- Go back to browser
	- Reload and show the changes
	
// Explain
 


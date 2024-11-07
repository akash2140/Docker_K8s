# Docker_K8s
This contains sample Docker &amp; K8s scripts for varioous projects like NodeJs, React and Java


Docker is a container technology. A tool for creating and managing containers.

What is Container??
Container is a standarized unit of sotware. A package of code and dependencies to run that Code(eg NodeJS Code + NodeJs runtime). The same container always yield the same exact same application and execution behaviour. No matter by where or by whom It might be executed. 
  
Docker is just a tool for building these containers.

Rather than installing dependencies locally we would want them to run them in a container.
Support for containers is built within new operating systems.Docker basically simplifies the creation and management of such containers.


Why do we need Independent , Standardized packages in software developement?????

	Diff Development and Production environment. We want t o build and test in the same environment. To have same Dev and Prod env can be achieved using Docker and Containers.
	
	Diff Working vobnrionemnt within the same company. All Team members should have same working environment to achieve same results. 

  Clashing tools and Versions among diff project in which a Single Guy Is working on, Which indeed could be confusing and can result in unwanted errors. ex:- Tools and libraries requiree for porject A are often not the same/Clashing with Project B.
  
  
 With the help of Dockers and Containers, Switching projects is as easy as launching new containers.
 


Virtual Machines Vs Docker Containers:-
			
	--------------------------------------------------------------------------------------------------------------------------------------
							APP1                         			APP2                         
						Libraries/Dependencies				Libraries/Dependencies
						Virtual OS(Linux)				Virtual OS(Linux)
			
									HOST Operating System
----------------------------------------------------------------------------------------------------------------------------------------------


-
Virtual Machines/ Vrutal Operating Systems:-
		Machines running on our machines with VOS encapsulated within their shell, isolated from our OS.....
		
		Every VM is like s standAlone computer. A standalone machine which is running on top of our machine. If we have multiple such machine, there is a lot of space on our harddrive and tends to be very slow. 
		
		We will have to install a virtual OS for any application which needs to be setup on our virtual machine.
		
		
		For each Application we need to encapsulate it with an Virtual OS , no matter if the Same OS is to be used by another Application. They are basically as Isolated Virtial Machines. 
		
		Pros
		
	Separated Environments.
	Environment specific config possible
	Environment configuration can be shared and reproduced easily.
		
	Cons:
		Redundant duplication and waste of space.
		Performance can be slow , Boot times can be very long. 
		Reproducing on another computer/server is possible but could be tricky. There is no single config file which can be shared to duplicate the environment.
		

Docker and Containers is the solution here. The key Concept here are containers and not the Docker. Docker is just defacto for creating and managing containers. 
		
		
		

-----------------------------------------------------------------------------------------------------------------------------------------
							APP1                         			APP2                         
						Libraries/Dependencies				Libraries/Dependencies
											
								Docker Engine(Light weight small Tool)
								OS Built-in/Emulated Container Support
									HOST Operating System
-------------------------------------------------------------------------------------------------------------------------------------------
		
The APP1/APP2 might contain small layer of OS inside it but it isnt as big like bloated OS in the case of VM's...

Inorder to describe the container , we can share the Config file,(DockerFile) or we can share the image with others to ensure everywhere same container is running.

Containers:-
	low impact on our OS, very fast, minimal disk space. 
	sharing, re-building, and distribution is easy
	Encapsulate apps/environemtns instead of whole machines.


Virtual Machines:-

	Bigger impact on OS,slower, higher disk space usage.
	sharing, rebuilding , distribution can be challenging.
	Encapsulate whole machines instead of just apps.
		

Linux natively supports Docker engine. We can directly install Docker Engine in it and use it. 

 
 Lets create the image first.

 DockerFile:-

 	FROM node:14
 	WORKDIR /app
 	COPY package.json .
 	RUN npm set strict-ssl false
 	RUN npm install
 	COPY . .
 	EXPOSE 3000
 	CMD [ "node", "app.mjs" ]

 	We would specifry to docker how our container should be setup

 			>>>>>  docker build .		[ This creates the docker image from the docker file, It finds in the directory ]

 	We can see id for this image after image gets successfully built.

 			>>>>>  docker run -p p1:p2 [imageid]

 					p1-localhost port
 					p2-container port

 	There is no connection netween our local system and the container. we would want the port to be exposed of the container. Else it is a locked environment from outside.


 	STOPPING THE CONTAINER :-

 		List all container:-
		 		     >>>>>	docker ps       [We see only the Running Processes]

 		CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                    NAMES
 		7c6904c563ec   81e9a767c05a   "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   0.0.0.0:8080->3000/tcp   romantic_sanderson

 	Shut Down Running Container:-
			>>>>>> docker stop  [container_name]

	Example:-
 			>>>>>> docker stop  romantic_sanderson
 				  

 	What it does is , it grabs the node:14 from the docker repository/Hub. Then it setups an image , which would run all the steps written in the docker file to be executed inside the image, for running it as container.
So it gives us the image, which is prepared to be started as a container.
FOUNDATION SECTION:-

					1. Images & Containers
					2. Data & Volumes(in Containers)
					3. Containers and Networking

Real Life Projects:-
					1. Multi Continer Projects
					2. Docker Compose.
					3. Utility Containers.
					4. Deploying Docker Containers with AWS.

Kubernetes:-
					1. K8s Introduction and Basics
					2. K8s: Data and Volumes
					3. K8s networking
					4. Deploying a K8s Cluster.


Lets first start with FOUNDATION Section:-

We will be going on dive into Images and containers(The core Building Block).

Images are the templates/blueprint for containers. It is actually the image which contains the code/required tools/runtime for running the code.
Container is a running Unit of Software.


1. What are images, How can we use inbuilt images, How we can we create our own images and how the containers and images are associated to each other and at what level.

2. There is concept of Data and Voluimes inside containers. We need to understand about that also. In that we can learn on how the data is managed in the containers and how the data persists inside the containers. Basically data is not lost in case container gets shut down, or removed or something happens to the container.

3. Containers and Networking:- How multiple containers can interact with each other.


REAL LIFE PART:-

	1. WE will have a closer look at multi container based projects.
	2. Using docker compose.
	3. Utility Containers.
	4. Deploying Docker container.

K8S':-


	1. K8s Introduction and Basics
	2. K8S Data and Volumes
	3. K8s Networking
	4. Deploying k8s clusters



SECTION : 2 
Docker IMAGES & CONTAINERS: THE CORE BUILDING BLOCKS


This section is about dealing with 2 fundasmental concepts related to docker , i.e , Working with Images and containers.
We will learn how these two concepts are related to docker.
Using Prebuilt and Custom Images.
Creating and managing containers.


----------------------------------------------------------------------------


Images, Containers What & Why?


We just dont have containers, we also have images while working with Docker. 

What is the difference and why do we need both.

Docker:

		Containers: The running "Unit of software". This is what we run in the end.
		Images    : These arwe teh templates or the blueprint of containers.  It containes the code + required tools to execute the code. 
		
Its the containers which then runs and executes the code. So we can say Containers are the runnable form of Images.

We have segregated these concepts so that we can create the images and basically create multiple containers based out of that image & run on diff servers/machines.



---------------------------------------------------------------------------------------------------

Finding & creating Images:-

We mentioned that the containers are based out of Images.

	We need an Image.

		1st Way:- use an existing, pre built Image(Docker hub, hub.docker.com)

		Lets say we search for Node docker image, We could find the official Node image in the Docker Hub,
		It is basically created, distributed and maintained by official Node Team.

		Lets get started by Using Node Image:-
		
					$		>>>>>> docker run node$
		
		This command shall run the node image as container.  This will first try to find the images locally in our system, If not found, will connect to the docker hub to fetch the image.

		This will offer us Interactive Mode of Node("Interactive Mode") where we can run basic node commands (the "REPL").

This will download the image locally into our system and run it as container. 

We cannot much see whats happening right now witht he container. This is important because container is actually very Isolated from the sorrounding environment.



we can check running containers as :-
							>>>>>>>> docker ps -a     [ ps stands for proocesses -a would list all the processes docker created for us]
							
							CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
							ccfb8feed944   node           "docker-entrypoint.s…"   26 seconds ago   Exited (0) 3 seconds ago              condescending_kowalevski
							07b87bd2c0be   node           "docker-entrypoint.s…"   34 seconds ago   Exited (0) 32 seconds ago             lucid_hawking    
							741725edb510   2c0cdd83f443   "docker-entrypoint.s…"   23 hours ago     Exited (137) 23 hours ago             practical_saha 

We can seee that the node container exited and we cannot interact with it. This is because containers are isolated and we didnt specify it to interact with it.

						>?>>>>>>>  docker run -it node [ This indicates we need an interactive shell with the Node Container which is in running state from inside the container to the hosting machine]

Hereww if we come out of the interactive shell, Then basically WE can check for the container running and it doesnt run anymore.

So we can say Images are required behind ths scene to hold all the logic/tools that a container needs.
Then we create the  instances of the images using the run command.


2ND WAY  :- 
			
Basically we normally doesnt run the images as the first Way. We need those images as the base and we build upon those images.
We pull in those Official Images and we add that image as the base on top of our coder to execute the code with that image.

If we want to run the Nodejs Project Locally which requires dependencies like express and body-parser.We would require to install NodejS.

		then we would require to download all dependencies using >>>>> npm install
		These dependencies go to the Node_>Mopdules package of our project.
		To start the server we would require to run the command as >>>>>> node server.js
		
				localhost:80 [] 

Based on above Knowledege we would develop our DOCKER File as well:-

With Docker what we need is, We wouldn't need to download and installl Node on our system. Also we dont have to chasnge over our Node versions if required by different Projects:-

So how do we run it? We will see how we utilise the docker image to buse the official Node image from the docker hun and run our code using that in our host machine.


STEPS:-

File-----> Dockerfile[ Special name which would be identified by the Docker ]
The file contains the instructions wjhat we want to use for building our image.
So it contains the setup instructions for our own image.


	1.We typically start from the "FROM" keyqword. It basically allows us to build our image from the base image(In our case Node image) It is not compulsory even we can build it from scratch by download Node and using that , but It is not required.

					FROM node  [ Docker will first search the image with "node" name in our system , Or else Docker will search it on Docker Hub. This command Indicates that before creating my own image , I want to have "node" image and then I wish to continue ]

	2. In the next step we want to tell docker , what files in our project we want to put into our image.


					COPY . .   [ The "first dot" indicates we want to copy all files/folders from the directory which contains the docker file excluding the docker file though.    ]

Every image create / container running has the internal file system which is totally detached from our file machine. It's hidden away inside of the docker container. Thwe "second dot" indicates that we want to copy all our files into the container root(.) path. We can copy as COPY . /app. It will copy our files into /app path of Docker file system

A container[or therefore the image] contains the environment + code . Hence we need to copy our code as well.	

	3. Actually all these commands will run under the working directory of our Docker image. By default it is the root directory whcih is the working directory. If we want to specify the working directory as /app , we want to run all tjhe commands like npm install inside the /app directory.

					WORKDIR /app  [ Specifies our working directory for our image ]

	4.  We had to have run npm install to have all the dependencies for our Node Express APP.

					RUN npm install [ Will run these commands under the working directory ]

	5. We want to start our server 

					RUN node server.js		

[ This is incorrect because this will run with the process of setting up of Docker image But we dont want that we want to run our image as container, We want our sderver to be UP at that time only, not in the process of setting up the server. ]

We have to keep in mind that Image must be the template for our container. Image  is not what we run in the end, We run the comntainer based on that image.
						
What we want in the docker image is: all the code, all the configs, all the environments versions properly setup and thats it. We dont want anything else. We dont want to run our image in the process of setting up the image.

							
Thus we have a different insdtruction here.

			CMD ["node", "server.js"]  If we dont specify the CMD, the CMD of the base image will get executed. With no Base image and no CMD, we would probably get an error.

[ This will not run when the image is created , But when the container starts on this image ].
This is exactly we want , we want to run our Node server at that point.



iF we run it like that only, we wouldnt be able to access our application due to one key Reason. We are not specifying the port. And we know that our Docker container is isolated on our local environment.
We dont have accesss to it normally. As a result it has it's own internal Network.

We have written in our Node app app.listen(80), In this case the running contain doesnt expore its port 80 to our host machine. Due to wghich we wont be able to listen on this port  , doesnt matter that something inside the container is listening inside of it.

Thus before specifying the command CMD, we want to specify another instruction which would specify how we want to listen that application in our local system.
				EXPOSE 80  , Now we will be able to rumn the container in a way that we can listen on it.

This is where we have finished our docker file with all the setup and instructions for our docker image. Now lets see how we can utilise this custome image, build it and run it.


----------------------------------------------------------------------------------------------------

RUNNING A CONTAINER BASED ON OUR OWN IMAGE:-

Lets see how we can turn this into an image and into the container ultimately.


				>>>>>>> docker build .
				[ docker build command tells, the docker to build docker  image baseed on the docker file]
				["." indicates the path which we need to specify where is the docker file  ]

Inorder to run this generate image as container, we need to use the below command:
														>>>>>>> docker run [image_id]   {Image_Id could be foudn when we had built the image}


CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                    PORTS      NAMES
5b6679599963   c2920a084bb7   "docker-entrypoint.s…"   46 seconds ago   Up 45 seconds             3000/tcp   heuristic_carver


NOTE:- When we see and try to listen omn the EXPOSED port , we see we cannot see the Node server. Why is that? This is because if we specify the Port on the Dopcker File, It doesnt really expose our Localport to the container port. It is just for Documentation purpose and optional. Hence we need to do a bit more , when we want  to run the container. 

				>>>>>>> docker run -p 3000:80 [image_id]
				3000 -> hiost maxchine port
				80 : on which container application is running on.


In the last lecture, we started a container which also exposed a port (port 80).

I just want to clarify again, that EXPOSE 80 in the Dockerfile in the end is optional. It documents that a process in the container will expose this port. But you still need to then actually expose the port with -p when running docker run. So technically, -p is the only required part when it comes to listening on a port. Still, it is a best practice to also add EXPOSE in the Dockerfile to document this behavior.

As an additional quick side-note: For all docker commands where an ID can be used, you don't always have to copy / write out the full id.

You can also just use the first (few) character(s) - just enough to have a unique identifier.

So instead of

docker run abcdefg
you could also run

docker run abc
or, if there's no other image ID starting with "a", you could even run just:

docker run a
This applies to ALL Docker commands where IDs are needed.

  


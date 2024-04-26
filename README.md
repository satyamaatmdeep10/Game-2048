# Overview

The 2048 Game project is a web-based implementation of the popular 2048 puzzle game, built using HTML, CSS, and JavaScript. After containerizing the game using Docker, it was seamlessly hosted on Azure App Service. Leveraging Docker for containerization and Azure App Service for hosting, the game offers a seamless and scalable gaming experience. Players can enjoy the addictive gameplay on any device, while contributors are welcome to enhance the project through collaboration and contributions.

## TASK TO PERFORMED:-
### The task is to containerize the game using Docker and then utilize Azure App Service for hosting.

## Solution:- 

### Step1 :- 
FROM ubuntu:22.04: This line specifies the base image to use for building the Docker container. In this case, it's Ubuntu version 22.04, which is the operating system on which our application will run.

### Step2 :- 
**RUN apt-get update && **: This line updates the package lists for Ubuntu's package manager (apt-get). The && \ allows us to chain multiple commands together in a single line.

### Step3 :- 
**apt-get install -y nginx zip curl && **: This line installs the necessary packages for our application: nginx, zip, and curl. The -y flag automatically answers "yes" to prompts during installation.

### Step4 :- 
echo "daemon off;" >> /etc/nginx/nginx.conf: This line adds the configuration daemon off; to the nginx configuration file. This configuration ensures that nginx runs in the foreground, which is required for Docker.

### Step5 :- 
RUN curl -o /var/www/html/master.zip -L https://github.com/gabrielecirulli/2048/archive/master.zip: This line downloads the source code of the 2048 game from GitHub and saves it as a zip file (master.zip) in the /var/www/html/ directory.

### Step6 :- 
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/ . && rm -rf 2048-master master.zip*: This line changes the directory to /var/www/html/, unzips the downloaded zip file, moves the contents of the unzipped folder (2048-master) to the current directory (.), and then removes the unnecessary files (2048-master folder and master.zip file).

### Step7 :- 
EXPOSE 80: This line specifies that the container will listen on port 80. This is important because nginx typically listens on port 80 by default.

### Step8 :- 
CMD [ "/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf" ]: This line specifies the command that should be executed when the container starts. It starts the nginx server using the configuration file located at /etc/nginx/nginx.conf.

### Step9 :- 

Then, in the terminal, we need to run Docker commands to build and run the Docker container containing our game.

### Command1 :-
The command docker build -t 2048-games . builds a Docker image with the tag 2048-games using the Dockerfile located in the current directory (.).

### command2 :-
The command docker image ls is used to list Docker images stored on your local system. It provides information such as the repository, tag, image ID, and creation time for each image.

### Command3 :-
The command docker run -d -p 80:80 <image_id> runs a Docker container in detached mode (-d), forwarding port 80 from the host to port 80 in the container (-p 80:80), using the specified Docker image (`

### Step10 :- 
Open Google Chrome and navigate to localhost:80 to access the game running locally.

### Screenshot of 2048-Game

![image](https://github.com/satyamaatmdeep10/Game-2048/assets/137147966/0219d5f4-b2a5-42ff-936c-3e4b69502069)


### Step11 :-
 To deploy your Docker container to Azure app service:- 
 
 ### Step A. 
 Prepare Docker Image: Push your Docker image to a container registry that Azure App Service can access. so first we have created Azure Container Registry and the Steps are:- 
 Create an Azure Container Registry: Go to the Azure portal, navigate to "Create a resource" > "Containers" > "Azure Container Registry" and follow the prompts to create a new registry.
 Login On your local machine.
 
#Command:- 1. az login
 2. az Command:- acr login --name <your_registry_name> 
 3.Tag your Docker image: Tag your local Docker image with the address of your Azure Container Registry:
 4. docker tag your_image_name <your_registry_name>.azurecr.io/your_image_name:tag
 5. Push the Docker image to ACR: #docker push <your_registry_name>.azurecr.io/your_image_name:tag

## screenshot

![image](https://github.com/satyamaatmdeep10/Game-2048/assets/137147966/841158c4-ffd1-4334-999f-1a5b3ae23e5b)

### Step B
Create an App Service:
1) Go to the Azure portal (portal.azure.com).
2) Click on "Create a resource" and search for "App Service".
3) Click on "Create" and fill in the required details like app name, subscription, resource group, etc.
4) Under "Publish", choose "Docker Container" and select the appropriate options for your container registry and image.
5) Configure any necessary settings such as environment variables, application settings, or connection strings in the Azure portal under the configuration section for your web app.
6) Deploy: Click on "Review + create" and then "Create" to deploy your app service.
7) Verify Deployment: After deployment, visit your web app's URL to verify that your application is running correctly.
   
This method allows you to deploy your Dockerized application to Azure App Service directly through the Azure portal without needing to use the command line.

## screenshot of Game2048

![image](https://github.com/satyamaatmdeep10/Game-2048/assets/137147966/3a656e0e-d5b7-4e78-94c9-9dd19a369ef8)


The game is running smoothly and plays without any issues.










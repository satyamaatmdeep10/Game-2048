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
 To deploy your Docker container to Azure:- 
 
 












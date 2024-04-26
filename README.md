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

Task 3.6c.1: Automation L1 - Start the Sparta app with a script (no database)
The Bash script should setup everything needed to run app on a fresh VM (as well as run the app), including:

apt update & upgrade

install nginx

(don’t worry about it) setup the reverse proxy

re-start + enable nginx

install nodejs (correct version)

copy app folder to VM

run Sparta test app in the background (try & to understand what happens, eventually you will probably need pm2)

Requirements to run Sparta app:

Linux VM - Ubuntu 18.04 LTS
update & upgrade
web server - nginx (dependency)
right version node js - version 12.x works fine (dependency)
get app folder
(if posts/connection to db) set DB_HOST env variable
Command: export DB_HOST=mongodb://20.162.216.117:27017/posts
in app folder, run 2 commands: npm install node app.js OR npm start
Bash SCript
#!/bin/bash

# update source list
sudo apt update -y

# upgrade all the packages and installs them in the kernal
sudo apt upgrade -y

# install nginx
sudo apt install nginx -y

# Start nginx on boot
sudo systemctl enable nginx

# start nginx
sudo systemctl start nginx

# status nginx
# sudo systemctl status nginx

# restart nginx
sudo systemctl restart nginx

# enable nginx - auto runs on startup
sudo systemctl enable nginx

# download node js
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

# install node js
sudo apt install nodejs -y

# update source list
sudo apt update -y

# install pm2
sudo npm install -g pm2

# git clone app
git clone https://github.com/jungjinggg/tech241_sparta_app app-github-automation

# get into app folder
cd ~/app-github-automation/app

# install node js inside folder
npm install -y

# start app
pm2 start app.js --name "sparta app"
Explanation
The provided script automates the setup and execution of a web application on a fresh Ubuntu 18.04 LTS VM. Let's go through the different steps and the purpose of each:

Update the package sources and upgrade all packages: This ensures that the system has the latest package information and that all installed packages are up to date.

nstall Nginx: Nginx is a popular web server that will be used to serve the web application to clients. It acts as a reverse proxy and handles HTTP requests.

Enable and start Nginx: These commands enable Nginx to start automatically on system boot and then start it immediately.

Download and install Node.js: Node.js is a JavaScript runtime that allows us to run JavaScript code on the server-side. The provided script downloads and installs the Node.js version 12.x using the curl command and the provided setup script.

Update the package sources again: After adding the Node.js repository, it's necessary to update the package sources to include the Node.js packages.

Install PM2: PM2 is a process manager for Node.js applications. It helps manage the application's lifecycle, including starting, stopping, and monitoring the application. Installing PM2 globally allows us to use it to manage our application.

Clone the application from a GitHub repository: The script clones the specified GitHub repository containing the application's source code.

Navigate to the application folder: The script changes the current working directory to the location of the cloned application folder.

Install the Node.js dependencies: The script uses npm (Node Package Manager) to install the dependencies required by the application. This command reads the package.json file in the application's directory and installs all the specified dependencies.

Start the application using PM2: The script uses PM2 to start the Node.js application. PM2 starts the application as a background process, manages its lifecycle, and ensures that it continues running even after the script finishes executing. The --name "sparta app" option assigns a name to the application process within PM2.

Node.js is needed because it provides the runtime environment for running JavaScript code on the server-side. It allows developers to build scalable and efficient web applications using JavaScript, a language traditionally associated with client-side scripting.

Npm (Node Package Manager) is a command-line tool bundled with Node.js. It manages dependencies for Node.js projects and provides a way to install, update, and manage the required packages/modules for an application. In the script, npm install -y installs the dependencies specified in the package.json file of the application.

PM2 (Process Manager 2) is a production-grade process manager for Node.js applications. It provides features like process monitoring, automatic restarts on failure, and load balancing. Using PM2, we can easily manage and monitor the application, ensuring its stability and availability in a production environment. The pm2 start app.js --name "sparta app" command starts the application using PM2, assigning the name "sparta app" to the PM2 process.

Together, Node.js, npm, and PM2 form a powerful ecosystem for building, managing, and running server-side JavaScript applications efficiently and reliably.

Scrip with &
#!/bin/bash

# update source list
sudo apt update -y

# upgrade all the packages and installs them in the kernal
sudo apt upgrade -y

# install nginx
sudo apt install nginx -y

# Start nginx on boot
sudo systemctl enable nginx

# start nginx
sudo systemctl start nginx

# status nginx
# sudo systemctl status nginx

# restart nginx
sudo systemctl restart nginx

# enable nginx - auto runs on startup
sudo systemctl enable nginx

# download node js
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

# install node js
sudo apt install nodejs -y

# update source list
sudo apt update -y

# install pm2
sudo npm install -g pm2

# git clone app
git clone https://github.com/jungjinggg/tech241_sparta_app app-github-automation

# get into app folder
cd ~/app-github-automation/app

# install node js inside folder
npm install -y

# start app in the background
nohup npm start &
Explanation
The provided script automates the setup and execution of a web application on a fresh Ubuntu 18.04 LTS VM. Here's a breakdown of the steps performed:

Update the package sources and upgrade all packages.
Install Nginx, a web server.
Enable and start Nginx.
Download and install Node.js version 12.x.
Update the package sources again.
Install PM2 globally, a process manager for Node.js applications.
Clone a specific GitHub repository containing the application.
Navigate to the application folder.
Install the dependencies required by the application.
Start the application in the background using nohup and npm start.
To run the application command using & to run it in the background, you can use the following command:
nohup npm start &
The nohup command is used to run a command immune to hangups, and & is used to run the command in the background.

Before you can run the same command again, you need to ensure that the previous instance of the application is stopped or terminated. Otherwise, attempting to run the command again will result in an error because the application is already running.

To stop the application running in the background, you can use the kill command followed by the process ID (PID) of the application. You can find the PID by using the ps command to list running processes and locating the process corresponding to the application. the port is already being used

Here's an example of how you can stop the application running in the background:

Find the PID of the application process::

ps aux | grep "node app.js"
This will display the process details, including the PID.

Use the PID to stop the application::

kill <PID>
Replace with the actual process ID of the application.

After stopping the previous instance of the application, you can run the same command (nohup npm start &) again to start a new instance of the application in the background.

Please note that this explanation assumes that the script is executed within the context of a Node.js application and that the necessary dependencies and configuration files are already present.
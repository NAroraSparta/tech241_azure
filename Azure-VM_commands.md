# What is Bash?
## Bourne Again SHell Unix was a text based operating system. Bash is an upgraded version of what was used in Unix.

/bin/bash

# What is a Shell?
## It is a software that basically provides interface to run commands.

###  There are multiple shells

cat /etc/shells -       listing all different shells installed in your os

ps -p $$ -              shows the processes that we are running (-p $$ specyfing current process)

!22 -                   ran the command from history under the number 22

# For making a bash script, create a file with .sh extension. This is for nginx.

##   #!/bin/bash

# update the sources 
sudo apt update -y

# upgrade (sometimes you dont want to upgrade because it installs new packages that might be incompatible with the existing softwares versions.)
sudo apt upgrade -y

# install nginx
sudo apt install nginx -y

# To view status of your Nginx server
sudo systemctl status nginx

# restart nginx
sudo systemctl restart nginx

# enable nginx    #- nginx will auto start on restart/reboot
sudo systemctl enable nginx

curl <url> --output <name of the file we want to save the data> - saving the data to the actual file we specified


rm -r <directory name> - removing directory -r means recursive. It will remove wverything inside the folder as well

apt install tree - to install packages e.g tree package

add sudo for super user permission

tree commands       
tree -                       tree structure for files and folders for where you currently are

sudo apt update -y -        update sources list just in case package is not on the list. -y to agree for the questions

# Scripting
## Making a script file

touch provision.sh - 
.sh - script files 
nano provision.sh -                  open editor to write commands

## if you are owner of the file you dont need to use sudo

#!/bin/bash -                       always start to mention which shell we want to use

./provision.sh                       To run a script

# Nginx (engine-x) is a popular open-source web server and reverse proxy server. Commonly used in web hosting environments to serve websites and web applications.

## systemctl is a command-line tool used to control and manage systemd services in Linux. Systemd is a system and service manager that provides a range of funcionalities including, starting, stopping and monitoring services.

## In the given script, systemctl is used to interact with Nginx service.

# Environment variables
value stored in memory, it can be accessible by other tools in Linux

printenv -                              printing all environment variables and values e.g USER, PATH,

printenv USER -                         printing specific variable USER

unset <name of your variable> -         removes variable

### Editing .bashrc file to make environmental variables persistent (so they won't dissapear after logging out)

nano .bashrc -                      opening editor with the file

and add at the bottom of the file environmental variable e.g:

export CATSNAME=Bobby

source .bashrc - reload edited configuration file

After all these steps env variable will be persistent after next time we log in

# IP addressess:
Public IP address (associated VM)

### static - (default Azure) stays the same even when VM is restarted
### dynamic - (default AWS) - changes IP every restart of your VM

## Processes
2 types:

### system processes: ps aux
### user processes: ps
Process is like a program that loaded to RAM. If your CPU has 1 core basically CPU can run 1 process at the time. Multicores can do more. OS needs to prioritize processes. Which one most important.

PID - process ID (every process has a process ID)

How to start and kill the process
sleep <number of seconds> - puts terminal to sleep (puts foreground) for certain amount of time

sleep 5000 & - puts terminal to sleep for 5000 sec but in the background

jobs - lists processes running in the background

jobs -l - list of processes with the process ID

kill -1 <process ID> - kills the proecss in the most gentle way (signal 1) - hanging up

kill <process ID> - kill the process, terminating (signal 15) - it will kill parent process and also child processes

kill -9 <process ID> - the harshest way of killing the process. Brute force stubborn process. (signal 9) - it will kill the parent process but child processes will turn up zombie processes that might still running and taking up the memories

ps -ef - shows parent process ID

sudo systemctl - way to control system processes

## Sparta test app
Node js app
port 3000
2 features
a front page (no database if we just want to display front page)
posts page that shows some information from database
Requirements to run Sparta app

### Linux VM - Ubuntu 18.04 LTS
web server - nginx
right version node js - version 12.x works fine (dependency)
app folder
in app folder, run 2 commands:
npm install
node app.js or npm start
getting folder to VM azure
git clone

create a gitrepo - tech241-sparta-app
create a folder "tech241-sparta-app" on your local machine
copy app folder to your local reo
sync with your remote repo on GitHub
SSH into VM & git clone
scp command

will need the private key
path to folder
adminuser@IP address
scp -i ~/.ssh/tech241-neha-az-key -r ./app adminuser@40.120.57.73:/home/adminuser/tech241-sparta-app

rsync

### Steps to access the Sparta_App using nodejs #####

rm -rf <file_name>              To delete the named file/folder forcefully and recursively.

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

sudo apt install nodejs -y              To install node.js on your local Ubuntu Linux machine

sudo npm install pm2 -g                 pm helps run apps in the background (PM2 is an advanced process manager for running Node.js applications. That provides an easier option to automate a Node.js application.)

cd tech241_sparta_app/              You need to be inside the sparta_app to run/install npm commands

ls
npm install                         saves any specified packages into dependencies by default
ls
node app.js                         Node.js is a platform for building fast and scalable server applications using JavaScript. Node.js is the runtime and npm is the Package Manager for Node.js modules.

Go to azure networking and add port 3000 and TCP so that you can access the sparta_app.

ctrl + z                        is used to suspend a process. (This means that the program or command you are running will be temporarily halted and put in the background, taking up no resources. This can be useful if you need to free up RAM or CPU cycles for other tasks.)

ps aux                          To monitor processes running on your Linux system.

npm start                       To start the process again

kill -1 <PID>                   To kill process, go slow first.
kill <PID>                      To kill process forcefully
kill -9 <PID>                   To kill with brute force

### ctrl c is used to kill a process. It terminates your program.
### ctrl z is used to pause the process. It will not terminate your program, it will keep your program in background. You can restart your program from that point where you used ctrl z.

## Requirements to run Database VM

1. sudo apt update -y
2. sudo apt upgrade -y
3. wget -qO - https://www.mongodb.org/static/pgp/server-3.2.asc | sudo apt-key add -
4. echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
5. sudo apt update -y
6. sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20
7. sudo nano /etc/mongod.conf
8. Change the bindip from 127.0.0.1 to bindI.0.0.0.0    (save n exit from Nano editor)
9. cat /etc/mongod.conf
10. sudo systemctl status mongod
11. sudo systemctl start mongod
12. sudo systemctl enable mongod
13. export DB_HOST=mongodb://20.254.109.117:27017/posts
14. printenv DB_HOST
15. npm install
16. npm start
17. go to the ip address from Azure VM and paste it into google address bar as <ip address>:3000/posts
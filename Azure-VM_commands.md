## What is Bash?
## Bourne Again SHell Unix was a text based operating system. Bash is an upgraded version of what was used in Unix.

/bin/bash

## What is a Shell?
## It is a software that basically provides interface to run commands.

###  There are multiple shells

cat /etc/shells -       listing all different shells installed in your os

ps -p $$ -              shows the processes that we are running (-p $$ specyfing current process)

!22 -                   ran the command from history under the number 22

## For making a bash script, create a file with .sh extension. This is for nginx.

##   #!/bin/bash

## update the sources 
sudo apt update -y

## upgrade (sometimes you dont want to upgrade because it installs new packages that might be incompatible with the existing softwares versions.)
sudo apt upgrade -y

## install nginx
sudo apt install nginx -y

## To view status of your Nginx server
sudo systemctl status nginx

## restart nginx
sudo systemctl restart nginx

## enable nginx    #- nginx will auto start on restart/reboot
sudo systemctl enable nginx

curl <url> --output <name of the file we want to save the data> - saving the data to the actual file we specified

rm -r <directory name> - removing directory -r means recursive. It will remove wverything inside the folder as well

apt install tree - to install packages e.g tree package

add sudo for super user permission

tree commands       
tree -                       tree structure for files and folders for where you currently are

sudo apt update -y -        update sources list just in case package is not on the list. -y to agree for the questions

## Scripting
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

## Environment variables
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

## IP addressess:
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

## scp command

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
13. Go to Sparta_app git bash and run commands 14-18 there.
14. export DB_HOST=mongodb://20.254.109.117:27017/posts(Go to your DB VM and add port 27017 there)
16. printenv DB_HOST
17. Go inside tech241-sparta_app and run npm install and npm start there.
18. npm install
19. npm start
20. go to the ip address from Azure Sparta_app VM and paste it into google address bar as <ip address>:3000/posts



## Automation -Start the Sparta app with a script (no database)

### Edit the provision.sh file:
 
 #!/bin/bash

### update
sudo apt update -y

### upgrade
sudo apt upgrade -y

### install nginx

sudo apt install nginx -y

### restart nginx

sudo systemctl restart nginx

### enable nginx - make sure that when the virtual machine restarts nginx will automatically start

sudo systemctl enable nginx

### setup node

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

### install node

sudo apt install nodejs -y
sudo npm install pm2 -g

### copy app.js folder

cd ~
git clone https://github.com/NAroraSparta/tech241_sparta_app.git
cd sparta_app
cd app

### run test app in the background

npm install
pm2 start app.js


### Starting sparta app with script
#!/bin/bash

### update
sudo apt update -y

### upgrade
sudo apt upgrade -y

### install nginx
sudo apt install nginx -y

### restart nginx
sudo systemctl restart nginx

### enable nginx - will auto start on reboot
sudo systemctl enable nginx

### access correct node source
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

### add in env
export DB_HOST=mongodb://172.187.178.145:27017/posts

### install node.js
sudo apt install nodejs -y

### run app in background
sudo npm install -g pm2

### enable node.js - will auto start on reboot
sudo systemctl enable nodejs

### copy app folder
git clone https://github.com/NAroraSparta/tech241_sparta_app.git

# Run app in the background using PM2
cd /home/adminuser/app/app2
pm2 start app.js --name "sparta app"


### Configure Mongo DB VM (including bindIp) with a script

#!/bin/bash

# update
sudo apt update -y

# upgrade
sudo apt upgrade -y

# Import the public key used by the package management system.
wget -qO - https://www.mongodb.org/static/pgp/server-3.2.asc | sudo apt-key add$

echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse"$

sudo apt update -y

## Install a specific release of MongoDB Enterprise
sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=$

## Configure the bindIp to 0.0.0.0 (Hint: use sed command)
sudo sed -i 's/bindIp: 127.0.0.1/bindIp: 0.0.0.0/g' /etc/mongod.conf

## Restart Mongo Db
sudo systemctl restart mongod

## Enable Mongo DB
sudo systemctl enable mongod

## To run the script in git bash
./provision.sh 

## Connect VMs

export DB_HOST=mongodb://:27017/posts
Add import rule to allow port 27017
npm start
npm install


## Running node app in the background using &

nohup node app.js </dev/null &>/dev/null &

without </dev/null> we would get the message:

nohup:ignoring input and appending output to 'nohup.out'

nohup means no hang up - which means that process will be still running even if we log out from the terminal. if we don't mention nohup the user processes will hang up when we exit the terminal.

and terminal would be occupied.

ps2 is a better solution because we can force rerunning the app. with nohup keyword port 3000 would be occupied.

when you run a bash script shell in bash it kind of create subshell. after the script finishes it hang up the subshell and all the user processes withing. to prevent that you need to add nohup.


## Automate MongoDB with an automatic script
1. nano provision.sh

#!/bin/bash

# update
sudo apt update -y

# upgrade
sudo apt upgrade -y

# install the correct version of Mongo DB
wget -qO - https://www.mongodb.org/static/pgp/server-3.2.asc | sudo apt-key add -

echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20

# configure the bindIp to 0.0.0.0 (Hint: use sed command)
cd /
sudo sed -i 's/bindIp: 127.0.0.1/bindIp: 0.0.0.0/g' /etc/mongod.conf
cd ~

# start and enable Mongo DB
sudo systemctl start mongod

sudo systemctl enable mongod
2. Come back to Git Bash and run the following commands.

sudo nano /etc/mongod.conf
sudo systemctl status mongod
./provision.sh



## Blob Storage

### Accessing the API

az login

### creating storage account

az storage account create --name tech24nehastorage --resource-group tech241 --location uksouth --sku Standard_LRS

sku is redundancy type

### list all storage accounts

az storage account list --resource-group tech241

### choose the bits you want to take from json

az storage account list --resource-group tech241 --query "[].{Name:name, Location:location, Kind:kind}" --output table

### creating container. \ is to break commands up into lines (not necessary)

az storage container create \ --account-name tech24nehastorage \ --name democontainer

### Create a text file
touch test.txt

### uploading file we created

az storage blob upload --account-name tech24nehastorage --container-name democontainer --name newname.txt --file test.txt --auth-mode login

### check blobs in container

az storage blob list --account-name tech24nehastorage --container-name democontainer  --output table --auth-mode login

### Adding an image to the sparta app from Blob
SSH into your Azure VM

Install Azure CLI on your Azure VM - this will give you access to the az command.

Login to Azure

Download a cat picture (jpg) of your choice to your VM - name is newcat.jpg

Upload the cat picture to Azure blob storage (Hint: You will first need a storage account + container) - in blob storage the same file should be called uploadedcat.jpg

Set access permissions so it can be viewed by the public

Modify the file index.ejs (found in views folder inside the app folder) - add an  tag to the HTML so display the uploadedcat.jpg image on the Sparta front page.

Run the app (no database) to check your blob image displays on the Sparta test app's front page.

### Documentation of the process
1. Use curl to download the image directly from a URL onto the VM.

2. To add new files and edit existing ones, you have to change permission for some files and directories in the app folder.






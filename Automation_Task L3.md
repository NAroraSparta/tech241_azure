## Automation L3 - Modify app VM script to use database VM

This script modifies the app VM script from "Automation L1 - Start the Sparta app with a script (no database)" to use a separate database VM for the Sparta app. The database VM script should be executed first before running this script.

## Prerequisites
Linux VM running Ubuntu 18.04 LTS
Database VM script successfully executed

## Instructions

1.Update and upgrade the system:

 sudo apt update -y
 sudo apt upgrade -y

2. Install nginx web server:

 sudo apt install nginx -y

3. Start nginx:
 sudo systemctl start nginxI

4. Install Node.js:
 curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

 sudo apt install nodejs -y

5. Set the DB_HOST environment variable:

 export DB_HOST=<database_vm_ip>:<database_vm_port>/posts

Replace <database_vm_ip> and <database_vm_port> with the actual IP address and port of the database VM.

6. Clone the app repository:
 cd ~/<sparta_app>/app

7. Install the app dependencies:
 npm install -y

8. Start the app using pm2 process manager:
  sudo npm install -g pm2

 pm2 start app.js --name "sparta app"

9. Save the script and execute it after the DB VM script has successfully run on the database VM.
    ctrl + s to save
    ctrl + x  to exit from the nano editor

10. Verify that the Sparta app, including the posts page, comes up in the web browser when you go to the app VM's public IP.
   Use ./provision.sh  to run the script
    
By s etting the DB_HOST environment variable, the app VM is configured to connect to the database VM, allowing the Sparta app to interact with the database successfully.

Task 3.6c.2: Automation L2 - Configure MongoDB VM (including bindIp) with a script
This script is designed to completely configure the MongoDB VM, making it ready for the app VM to connect to the database when the DB VM is started. It automates the process of setting up MongoDB by performing the necessary steps.

Prerequisites
To run the script, ensure that you have the following:

Linux VM with Ubuntu 18.04 LTS.
Administrative privileges or ability to run commands with sudo.
Script
The script performs the following steps::

Update and upgrade the Linux VM::

sudo apt update -y
sudo apt upgrade -y
Install MongoDB:

wget -qO - https://www.mongodb.org/static/pgp/server-3.2.asc | sudo apt-key add -
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt update -y
sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20
Retrieve the public GPG key for MongoDB version 3.2.x:

wget -qO - https://www.mongodb.org/static/pgp/server-3.2.asc | sudo apt-key add - retrieves the public GPG key for MongoDB version 3.2.x and adds it to the system's keyring. The GPG key is used to verify the authenticity of the MongoDB packages during installation. Add the MongoDB repository to the package manager's sources list:

echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list adds a new repository file named mongodb-org-3.2.list to the /etc/apt/sources.list.d/ directory. The repository URL specifies the MongoDB version (3.2) and the Ubuntu distribution (xenial) to fetch the appropriate MongoDB packages.

Update the package lists to include the MongoDB repository:

sudo apt update -y updates the package lists, including the newly added MongoDB repository. This ensures that the system is aware of the MongoDB packages available for installation. Install the specified versions of MongoDB and its related components:

sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20 installs the specific versions of MongoDB components. The package names are provided with their respective versions to ensure the installation of MongoDB version 3.2.20 and its associated tools.

Configure MongoDB to accept connections from any IP address:

sudo sed -i 's/bindIp: 127.0.0.1/bindIp: 0.0.0.0/g' /etc/mongod.conf
The sed command modifies the /etc/mongod.conf file, replacing the line bindIp: 127.0.0.1 with bindIp: 0.0.0.0. This change allows MongoDB to accept connections from any IP address, enabling communication with the app VM. Configure MongoDB to accept connections from the app VM:

sudo sed -i 's/bindIp: 127.0.0.1/bindIp: 0.0.0.0/g' /etc/mongod.conf modifies the /etc/mongod.conf file using the sed command. The sed command substitutes the IP address 127.0.0.1 (which restricts connections to localhost) with 0.0.0.0 (which allows connections from any IP address). This change enables MongoDB to accept connections from any IP address. 4. Start and enable MongoDB:

```
sudo systemctl start mongod
sudo systemctl enable mongod
```
These commands start MongoDB and configure it to start automatically on boot.
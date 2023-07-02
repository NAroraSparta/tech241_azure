Running node app in the background using &
nohup node app.js </dev/null &>/dev/null &
without </dev/null> we would get the message:

nohup:ignoring input and appending output to 'nohup.out'

### nohup means no hang up - which means that process will be still running even if we log out from the terminal. if we don't mention nohup the user processes will hang up when we exit the terminal.

### nohup prevents the process from being terminated when terminal session ends, doesn't engage terminal, it always changes process ID so you need to kill previous command to run it again. Doesn't run again as port is in use.


and terminal would be occupied.

ps2 is a better solution because we can force rerunning the app. with nohup keyword port 3000 would be occupied.

when you run a bash script shell in bash it kind of create subshell. after the script finishes it hang up the subshell and all the user processes withing. to prevent that you need to add nohup.

reverse proxy research and task:
What are ports?
ports are virtual endpoints that enable communication between different programs or services on a computer or across a network. They allow for the transfer of data packets between applications or devices.

WHat is proxy?
A proxy, in the context of computer networking, is an intermediary server that acts as a gateway between a client device and a target server. It facilitates communication between the client and the server by forwarding client requests and receiving server responses. The proxy server operates on behalf of the client and provides several benefits, including enhanced privacy, security, and performance optimization.

What is the reverse proxy
A reverse proxy is a server or a software application that sits between client devices and web servers. It acts on behalf of the web servers to handle client requests and distribute them to the appropriate backend servers. Unlike a normal proxy, which forwards client requests to remote servers, a reverse proxy accepts requests on behalf of servers and returns the responses to clients.

Here are the key differences between a reverse proxy and a normal proxy:

Direction of communication: A normal proxy acts as an intermediary between a client device and a remote server. It forwards client requests to the server and relays the server's responses back to the client. In contrast, a reverse proxy acts as an intermediary between clients and backend servers. It receives client requests and forwards them to the appropriate server, then returns the server's responses to the clients.

Load distribution: One of the primary functions of a reverse proxy is load balancing. It distributes incoming client requests across multiple backend servers to achieve better performance and scalability. By intelligently distributing the workload, a reverse proxy can optimize resource utilization and prevent any single server from becoming overwhelmed. A normal proxy typically does not provide load balancing capabilities.

Content caching: Reverse proxies often implement content caching, which involves storing copies of server responses locally. When subsequent requests for the same content are made, the reverse proxy can serve the cached copy directly to clients without forwarding the request to the backend server. This can significantly improve response times and reduce the load on the backend servers. Normal proxies may also support caching, but it is not as commonly used.

SSL termination: Reverse proxies can handle Secure Sockets Layer (SSL) encryption and decryption, relieving the backend servers from this resource-intensive task. The reverse proxy can establish the SSL connection with the client and then communicate with the backend server over an unencrypted connection. This allows the backend servers to focus on processing requests and responses without the overhead of SSL encryption. Normal proxies generally do not perform SSL termination.

Overall, a reverse proxy is specifically designed to handle client requests on behalf of backend servers, providing load balancing, caching, SSL termination, and other features to optimize performance, security, and scalability. In contrast, a normal proxy primarily forwards client requests to remote servers without the additional functionalities typically found in a reverse proxy.

reverse-proxy

How Do you setup nginx reverse proxy
Install Nginx on your Windows or Linux server (prerequisite).
Add the Nginx proxy_pass setting in a virtual host or the default config file.
Map a context root to the URL of a backend server.
Optionally set headers for the Nginx reverse proxy to use with the backend.
Restart Nginx reverse proxy and test the reverse proxy setup.
#!/bin/bash


# update
sudo apt update -y

# upgrade
sudo apt upgrade -y
# install nginx
sudo apt install nginx -y
# restart nginx
sudo systemctl restart nginx
# enable nginx
sudo systemctl enable nginx
The most important configuration step in an Nginx reverse proxy configuration is the addition of a proxy_pass setting that maps an incoming URL to a backend server.

sudo nano /etc/nginx/sites-available/default
in the default file we need to change the line in location starting with:

try_files $uri $uri/ =404;

for

proxy_pass http://localhost:3000;

after that we need to restart nginx:

sudo systemctl restart nginx

Command to setup nginx as a reverse proxy:

sudo sed -i 's@try_files .*;@proxy_pass http://localhost:3000;@' /etc/nginx/sites-available/default

app VM script that automates reverse proxy
#!/bin/bash


# update
sudo apt update -y

# upgrade
sudo apt upgrade -y
# install nginx
sudo apt install nginx -y
# restart nginx
sudo systemctl restart nginx
# enable nginx
sudo systemctl enable nginx
# setup nginx as a reverse proxy
sudo sed -i 's@try_files .*;@proxy_pass http://localhost:3000;@' /etc/nginx/sites-available/default
# restart nginx again
sudo systemctl restart nginx
# get from url needed version of node
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
# install nodejs
sudo apt install -y nodejs
#installing pm2 that helps run apps in the background
sudo npm install pm2 -g
# getting app folder to the VM
git clone https://github.com/majeranowski/tech241-sparta-app.git app3
#getting inside app folder
cd app3/app
#Creating DB_HOST env variable
export DB_HOST=mongodb://20.162.216.138:27017/posts
# installing the app
npm install
# starting the app
pm2 -f start app.js

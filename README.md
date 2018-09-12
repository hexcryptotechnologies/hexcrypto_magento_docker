# Hexcrypto Technologies Magento2 Docker
# Docker Local Magento/ PHP Environment - Sample
# Docker With PHP 7+ MySql + Apache + phpMyAdmin

===========Magento2 setup using Docker Compose===========

Installing Docker and Docker-Compose:

Docker is available in two editions: Community Edition (CE) and Enterprise Edition (EE).
We can use them according to our requirements. Here We’ll use Docker CE.
So to install Docker CE on our desired platform/OS we can follow Official Documentation.
In this Doc I’m assuming our host OS is Ubuntu 16.04.
1. Choose CE or EE edition for Ubuntu from here.

2. Uninstall older docker versions.(if any) 
    sudo apt-get remove docker docker-engine docker.io

3. Although there are various ways to install docker CE we’ll follow Installation using the repository.
    i) Update the apt package index: sudo apt-get update
    ii) Install packages to allow apt to use a repository over HTTPS:
        sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
    iii) Add Docker’s official GPG key: 
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    iv) to set up the stable repository a/c to Ubuntu distribution:
    sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"
    v) To install the latest version of Docker CE:
    sudo apt-get update && sudo apt-get install docker-ce
    vi) verify docker installation by running docker -v


4. Install Docker-Compose:
    i) To download latest docker-compose version:
    sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

 ii) make it executable: sudo chmod +x /usr/local/bin/docker-compose
iii) Optionally, install command completion for the bash and zsh shell.
iv) verify docker-compose installation using docker-compose -v
v) add docker in normal user’s usergroup so we don’t have to add sudo every time executing any docker command.
    sudo usermod -aG docker normaluser
Note: This requires a logout and login again to work properly.



2. Building and Running Magento2 local development environment using Docker-Compose
 
 i) with Apache, PHP7, MySQL & phpMyAdmin

1. Clone the repository:
git clone https://github.com/hexcryptotechnologies/hexcrypto_magento_docker.git && cd magento2_docker


2. Make necessary changes in docker-compose.yml according to convenience like ports to be exposed, directories etc. 
Also make sure host machine’s mysql and web server are stopped or running on different port than exposed in .yml file.
Extract Magento setup tar.gz or .zip archive in web/htdocs and give proper permissions.

Finally hit sudo docker-compose up -d

Step 3. This will start 3 containers one of PHP & web-server and others for MySQL and PhpMyAdmin

Verify if all 3 containers are up and running with sudo docker ps

Step 4. Your Magento2 code will be in web/htdocs folder and that of DB will be in db folder.

Step 5: Install Magento2 setup at http://127.0.0.1 and 
Access PhpMyAdmin at http://127.0.0.1:8080

We can access MySQL via CLI either by logging into container (docker exec -it mysql_container_id  /bin/bash) and using mysql -uroot -p there.
OR we can access it directly by running this mysql -h127.0.0.1 -uroot -p

P.S.: use docker ps to get container id

If everything worked fine till now, you’ll be seeing Magento2 installation page right now at http://127.0.0.1,Just follow the steps and we’ve got our Magento2 local development environment with Apache up and running powered by docker containers.

NOTE: To run php commands like php bin/magento setup:upgrade you have to login into PHP container and run these commands there. To do this:
i) find and copy container id of PHP container by sudo docker ps
ii) run sudo docker exec -it container_id /bin/bash
                    
============================Cheers..!!============================
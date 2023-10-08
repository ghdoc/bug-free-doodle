## Commands

- stop and remove all containers - #oneliner:docker  
    docker stop $(docker ps -a -q)
- docker rm $(docker ps -a -q)
- remove all images - #oneliner:docker  
    docker rmi $(docker images -q)
- remove all containers that aren't currently running - #oneliner:docker  
    docker rm $(docker ps -a -q -f "status=exited*")
- run container and share host folder - #oneliner:docker  
    docker run -i -t -v C:/DOCKER/Share:/host_share 15a940de /bin/bash

## DockerFile

- contains instructions to build an image, copy context=files, run commands

## Docker-Training

- Jess Fraz - Docker blog  
    https://blog.jessfraz.com/post/docker-containers-on-the-desktop/
- https://github.com/jessfraz
- Docker Deep Dive Plural Sight Course  
    https://app.pluralsight.com/library/courses/docker-containers-big-picture/table-of-contents
- Docker Beginner Course  
    https://app.pluralsight.com/player?course=docker-containers-big-picture&author=nigel-poulton&name=docker-containers-big-picture-m2&clip=2&mode=live

## Setting up docker in WSL2

- Install wsl2  
    [https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
- Install Docker Engine  
    [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)

- Since installing from scratch - Setup the repository  
    1. sudo apt-get update

- 2. sudo apt-get install \
     apttransporthttps \
     cacertificates \
     curl \
     gnupg \
     lsbrelease

- 3. curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

- 4. echo \
   "deb [arch=amd64 signedby=/usr/share/keyrings/dockerarchivekeyring.gpg] [https://download.docker.com/linux/ubuntu](https://download.docker.com/linux/ubuntu) \
   $(lsb_release cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

- Install docker engine  
    1. sudo apt-get update	
    2. sudo apt-get install docker-ce docker-ce-cli [containerd.io](http://containerd.io/)

- Verify docker engine is installed - **sudo docker run hello-world**

	sudo docker run hello-world gives error

	- docker: Cannot connect to the Docker daemon at [unix:///var/run/docker.sock](unix:///var/run/docker.sock). Is the docker daemon running?.
	- based on [https://github.com/MicrosoftDocs/WSL/issues/457](https://github.com/MicrosoftDocs/WSL/issues/457) we can run 
	
	- sudo /etc/init.d/docker start  
	    starts docker daemon
	- then again run **sudo docker run hello-world**
	
## Install Docker Compose

- Get current stable release of Docker Compose  
    sudo curl -L "[https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname](https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname) -s)-$(uname -m)" -o /usr/local/bin/docker-compose
- Apply executable permissions to the binary  
    sudo chmod +x /usr/local/bin/docker-compose
- Install Command Completion  
    [https://docs.docker.com/compose/completion/](https://docs.docker.com/compose/completion/)

- Copies script to bash completion  
    sudo curl \
     -L [https://raw.githubusercontent.com/docker/compose/1.29.1/contrib/completion/bash/dockercompose](https://raw.githubusercontent.com/docker/compose/1.29.1/contrib/completion/bash/dockercompose) \
     o /etc/bash_completion.d/dockercompose

 sudo setfacl Rm d:g::rwx,d:o:rwx,g::rwx,o:rwx /path/to/logs/dir gives setfacl: command not found

 sudo aptget update y
 sudo aptget install y acl
- give proper dir address instead of /path/to/logs/dir

- adding ssh key in wsl

	- exec ssh-agent bash
	- ssh-add => this adds the private key that was previously created using ssh-agent

- docker info gives => Got permission denied while trying to connect to the Docker daemon socket at [unix:///var/run/docker.sock](unix:///var/run/docker.sock)  
    sudo usermod -a -G docker $USER
- reboot system
- docker: Cannot connect to the Docker daemon at [unix:///var/run/docker.sock](unix:///var/run/docker.sock). => redo commands from [how to setup docker inside wsl2 without docker desktop](https://workflowy.com/#/dd524c74c3c9) 
- how to setup docker inside wsl2 without docker desktop

- 1. complete steps in [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)
- 2. complete steps in [https://docs.docker.com/engine/install/linux-postinstall/](https://docs.docker.com/engine/install/linux-postinstall/)
- 3. systemctl start docker
- 4. add/create /etc/wsl.conf  
    [boot]
- systemd=true
- 5. logout and login
- 6. complete setps in [https://docs.docker.com/compose/install/other/](https://docs.docker.com/compose/install/other/)

- docker: Cannot connect to the Docker daemon at [unix:///var/run/docker.sock](unix:///var/run/docker.sock). => redo commands from [how to setup docker inside wsl2 without docker desktop](https://workflowy.com/#/dd524c74c3c9) 

- Run gui app in linux docker container on windows host  
    [https://dev.to/darksmile92/run-gui-app-in-linux-docker-container-on-windows-host-4kde](https://dev.to/darksmile92/run-gui-app-in-linux-docker-container-on-windows-host-4kde)

- choco install vcxsrv

- Save it to one of the following locations:

- %appdata%\Xming
- %userprofile%\Desktop
- %userprofile%

- build new container => **docker build -t firefox:1.0 .**
- set ip to yours => **set-variable -name DISPLAY -value 10.11.128.118:0.0**
- run container => **docker run -ti --rm -e DISPLAY=$DISPLAY firefox**

- VSCode C++ and WSL
- Update docker images

- docker images => to list images with repo and tag
- docker pull repo:tag
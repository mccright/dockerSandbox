# Install docker -- Various Environments  

## Install docker on Ubuntu 20.04  

### Install via snap
```
matt@mylt:~/Downloads$ sudo snap install docker
docker 19.03.13 from Canonical✓ installed
matt@mylt:~/Downloads$ docker --version
Docker version 19.03.13, build cd8016b6bc
```

### Post-Install tasks
```
matt@mylt:~/Downloads$ sudo addgroup --system docker
Adding group `docker' (GID 133) ...
Done.
matt@mylt:~/Downloads$ sudo adduser $USER docker
Adding user `matt' to group `docker' ...
Adding user matt to group docker
Done.
matt@mylt:~/Downloads$ newgrp docker
Current OS: Ubuntu 20.04.2 LTS 'focal' (GNU/Linux 5.4.0-80-generic x86_64) - 5746928K
matt@mylt:~/Downloads$ sudo snap disable docker
docker disabled
matt@mylt:~/Downloads$  sudo snap enable docker
docker enabled
matt@mylt:~/Downloads$ docker info
<lots of info == success>

matt@mylt:~/Downloads$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete 
Digest: sha256:df5f5184104426b65967e016ff2ac0bfcd44ad7899ca3bbcf8e44e4461491a9e
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

matt@mylt:~/Downloads$
```

## Install docker-ce on Ubuntu 18.04  

Don't use the Docker installation package available in the official Ubuntu 18.04 repository (it will not reliably be the latest version).  
Instead install the latest Docker package from Docker’s repositories.  

## Enabling Docker repository  

a. Update the packages list and install the dependencies necessary to add a new repository over HTTPS:  

```
sudo apt update  
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common  
```

b. Import the repository’s GPG key with:  

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -  
```

c. Add the Docker APT repository with:  

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"  
```

## Install docker-ce  

Install the latest version of Docker with:  

```
sudo apt update  
sudo apt install docker-ce  
```

Install a specific version by listing available versions in the Docker repository, then installing a specific version:

```
apt list -a docker-ce  
```

Command output includes the available Docker versions in the second column.  

```
Listing... Done  
docker-ce/bionic 5:19.03.7\~3-0\~ubuntu-bionic amd64  
docker-ce/bionic 5:19.03.6\~3-0\~ubuntu-bionic amd64  
docker-ce/bionic 5:19.03.5\~3-0\~ubuntu-bionic amd64  
<many rows removed>  
docker-ce/bionic 5:18.09.3\~3-0\~ubuntu-bionic amd64  
docker-ce/bionic 5:18.09.2\~3-0\~ubuntu-bionic amd64  
docker-ce/bionic 5:18.09.1\~3-0\~ubuntu-bionic amd64  
docker-ce/bionic 5:18.09.0\~3-0\~ubuntu-bionic amd64  
docker-ce/bionic 18.06.3\~ce~3-0\~ubuntu amd64  
docker-ce/bionic 18.06.2\~ce~3-0\~ubuntu amd64  
docker-ce/bionic 18.06.1\~ce~3-0\~ubuntu amd64
docker-ce/bionic 18.06.0\~ce~3-0\~ubuntu amd64
docker-ce/bionic 18.03.1\~ce~3-0\~ubuntu amd64
```

To install version 18.06.3:  

```
sudo apt install docker-ce=18.06.3\~ce\~3-0~ubuntu  
```

Prevent the Docker package from being automatically updated by marking it as held back:  

```
sudo apt-mark hold docker-ce  
```

When the installation finishes the Docker service will start automatically.  

Verify it with:  

```
sudo systemctl status docker  
```

The output will look something like this:

```
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: e
   Active: active (running) since Sat 2020-05-02 09:53:27 CDT; 4h 13min ago
     Docs: https://docs.docker.com
 Main PID: 6095 (dockerd)
    Tasks: 17
   CGroup: /system.slice/docker.service
           └─6095 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/contain
```

## Executing docker command without sudo  

By default managing docker requires administrator privileges.  

Run docker commands as a non-root user by adding yourself to the docker group.  

```
sudo usermod -aG docker $USER  
```

Log in again to refresh group memberships.  

Verify your work with:  

```
docker run hello-world  
```

The output should include a "Hello from Docker" message and exit.  

## Upgrade Docker  

Update the package with the standard upgrade process:  

```
sudo apt update  
sudo apt upgrade  
```

## Uninstall Docker

Before you uninstall Docker remove all your containers, images, volumes, and networks.  

Uninstall Docker using standard package removal practices with apt:  

```
sudo apt purge docker-ce  
sudo apt autoremove  
```

The starting point for this document was: "How to Install and Use Docker on Ubuntu 18.04." Updated Aug 27, 2019 [https://linuxize.com/post/how-to-install-and-use-docker-on-ubuntu-18-04/](https://linuxize.com/post/how-to-install-and-use-docker-on-ubuntu-18-04/) fetched on 02-05-2020, with my experience/mistakes added...  



-------------------------------------------- 
## docker Daemon on Ubuntu Linux (the old way)

Initial notes:   

Update apt with:  

```
sudo apt update
```
Get your platform up-to-date with:  

```
sudo apt upgrade
```
NOTE: kernel upgrades need a reboot with:  

```
sudo reboot
```
Install Docker with:  

```
sudo apt install docker.io
```
For a variety of reasons, you may not want to run docker as root or grant users sudo permissions.  

If you already have a docker group, add users to it with:  

```
sudo usermod -a -G docker $USER
```

## Operating Docker

enable the Docker daemon at boot with:  

```
sudo systemctl start docker
sudo systemctl enable docker
```

If you need to stop or restart the Docker daemon:  

``` 
sudo systemctl stop docker  
sudo systemctl restart docker
```

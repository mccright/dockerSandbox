# distro-box  

Experimenting with a new operating system or maintaining several different complex development environments are common challenges.  

Distrobox is a wrapper around podman or docker to create and start containers that are highly integrated with their hosts -- sharing your host's $HOME directory, external storage, external USB devices, as well as supporting graphical apps (X11/Wayland) and audio.  

This has been especially helpful for me when doing some early experimentation with a given Linux variant.  If a docker-enabled idea appears to be something worth pursuing, then you can then invest in a more proper docker-enabled configuration.  

* Project Home: [https://github.com/89luca89/distrobox/](https://github.com/89luca89/distrobox/)  
* Tested container images: https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#containers-distros](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#containers-distros)  

Distrobox guest containers are not designed to be secure environments -- rather to be convenient environments, with shared access to your home directory.  This idea and implementation supports [a range of use cases](https://github.com/89luca89/distrobox/#why).  

Distrobox makes it easy to install packages in a number of [contained environments](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#containers-distros) on [a range of host operating systems](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#host-distros).  It also makes a lot of the host operating system and our home directory files easy to access as well (*again, this is a cautionary notice as well*).  

Installing Distrobox is also easy.  

```bash
# Assuming an Ubuntu-based OS
# install docker
sudo apt install curl docker.io 
# so you can run docker commands, rqd for distro-box
sudo adduser $USER docker 
# If needed, create the directory required for distro-box executables
mkdir -p ~/.local/bin
curl https://raw.githubusercontent.com/89luca89/distrobox/main/install > install
chmod 755 install
./install -P /home/$USER/.local

# If needed, update your $PATH 
# Add an '~/.local/bin' entry required for distro-box
export PATH=$PATH:~/.local/bin 
```

Use the following command to start a container:  
```bash
    distrobox create --image debian:stable --name debian
```
This downloaded a Debian:stable Docker container and labeled it "debian."  
To enter that container, use:  
```bash
    distrobox enter --name debian 
```
That worked too.  

Now, set up a keyboard shortcut to open a qterminal and enter the debian container.  

Open your keyboard shortcut mapper (mine is Lubuntu's Global Action Manager) set a key combination (I used Ctrl-Shift-D) to execute the following:  
```bash
/usr/bin/qterminal -e '/home/$USER/.local/bin/distrobox enter --name debian'
```

Then when you press Ctrl-Shift-D the system will present you with a new debian:stable OS.  

After a container is started or entered it remains running in the background.  

List the installed containers with:  
```bash
    distrobox list 
```

If it is important to stop a container, use the Docker command:  
```bash
    docker stop debian 
```

You can stop and remove a running container with:  
```bash
    distrobox rm --name debian --force 
```


#### Supporting References:  

* "Run Distrobox on Fedora Linux." by Luca Di Maio, Dec 29, 2021 [https://fedoramagazine.org/run-distrobox-on-fedora-linux/](https://fedoramagazine.org/run-distrobox-on-fedora-linux/)  

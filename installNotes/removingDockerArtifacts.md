# Removing Docker Artifacts

When you are not yet a Docker expert, there are lots of ways to create a mess of your docker environment.  The most common symptom for me has been that given docker images will no longer build, but you may have a different docker artifact-related symptom.  Sometimes it seems to work best if you just delete some of your old work and begin again.  The content below covers some ways to delete docker-related artifacts.  

# Removing images  

Remove one or more specific images:  

List:  

```
docker images -a
```

Remove:  

```
docker rmi Image Image
```

Remove dangling images:  

Docker images consist of multiple layers. Dangling images are layers that have no relationship to any tagged images. They no longer serve a purpose and consume disk space. They can be located by adding the filter flag, -f with a value of dangling=true to the docker images command. When you’re sure you want to delete them, you can use the docker images purge command:

Note: If you build an image without tagging it, the image will appear on the list of dangling images because it has no association with a tagged image. You can avoid this situation by providing a tag when you build, and you can retroactively tag an images with the docker tag command.

List:  

```
docker images -f dangling=true
```

Remove:  

```
docker images purge
```

Removing images according to a pattern  

You can find all the images that match a pattern using a combination of docker images and grep. Once you’re satisfied, you can delete them by using awk to pass the IDs to docker rmi. Note that these utilities are not supplied by Docker and are not necessarily available on all systems:

List:  

```
docker images -a |  grep "pattern"
```

Remove:  

```
docker images -a | grep "pattern" | awk '{print $3}' | xargs docker rmi
```

Remove all images:  

List:  

```
docker images -a
```

Remove:  

```
docker rmi $(docker images -a -q)
```



# Removing containers  

List All Your Containers:  

```
docker ps -a -q  
```

Then remove those that are not in use with:  

```
docker rm $(docker ps -q -f status=exited -f status=created)  
```
NOTE: Created is a state which can result when you run a container with an invalid command.  

# Remove containers according to a pattern:  

List:  

```
docker ps -a |  grep "pattern"
```

Remove:  

```
docker ps -a | grep "pattern" | awk '{print $3}' | xargs docker rmi
```

# Stop and remove all containers

List:  

```
docker ps -a
```

Remove:  

```
docker stop $(docker ps -a -q)  
docker rm $(docker ps -a -q)
```

# Clearing the docker cache  

Recent versions of docker include a command that clears the cached build layers.  

To remove all unused build cache, not just those dangling:  

```
docker builder prune --all
```

There are a couple options that will also be helpful:

```
--force , -f 		Do not prompt for confirmation
```
and
```
--filter 		Provide filter values (e.g. ‘dangling=true’)
```

# Purging All Unused or Dangling Images, Containers, Volumes, and Networks

This is a close relative to to the command above, but will remove:  
    - all stopped containers  
    - all volumes not used by at least one container  
    - all networks not used by at least one container  
    - all images without at least one container associated to them  
*CAUTION: This is pretty distructive, so think about what you want to accomplish before executing this command...*  

```
docker system prune
```

There are a few other ways to remove all of them.  

This way looks slick, but does not seem to clean up everything for me:  

```
docker rm $(docker ps -a -q)
```

This way 
Remove dangling (none:none) images:  

```
docker rmi $(docker images -f "dangling=true" -q)
```

If your use case requires fresh data, use the 'no-cache' command:  

```
docker build –no-cache=true
```

# Remove one or more volumes

List:  

```
docker volume ls
```

Remove:  

```
docker volume rm volume_name volume_name
```

# Remove dangling volumes

When a container is removed, a volume is not automatically removed.  

List:  

```
docker volume ls -f dangling=true
```

Remove:  

```
docker volume prune
```

-------------------------------------
REFERENCES
Docker documentation, and  
[https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)  

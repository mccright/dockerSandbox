## Example with Python Docker [Official]  

Fetch the Python Docker Image  
```
matt@mylt:~/importantProj$ docker pull python
```
Run the image, mounting a local code directory (the local directory in this example)  
```
matt@mylt:~/importantProj$ docker run -d -it --name pydev --mount type=bind,source="$(pwd)",target=/code python
```
Get the container ID
```
matt@mylt:~/importantProj$ docker ps
CONTAINER ID    IMAGE       COMMAND      CREATED             STATUS          PORTS     NAMES
1cfc54bd3a37    python      "python3"    12 minutes ago      Up 12 minutes             pydev
matt@mylt:~/importantProjs$
```
Enter the running container and begin development with a '*clean*' Python environment
```
matt@mylt:~/importantProj$ docker exec -it 1cfc54bd3a37 bash
```

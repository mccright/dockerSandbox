# Removing Docker Artifacts

List All Your Containers:  

```
docker ps -a -q  
```

Then remove all of them with:  

```
docker rm $(docker ps -q -f status=exited)  
```

Remove all of them with:  

```
docker rm $(docker ps -a -q)
```

Remove dangling (<none>:<none>) images:  

```
docker rmi $(docker images -f "dangling=true" -q)
```

If your use case requires fresh data, use the 'no-cache' command:  

```
docker build –no-cache=true
```


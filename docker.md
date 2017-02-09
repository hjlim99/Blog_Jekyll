[Docker Official Hub](https://hub.docker.com/)
[Docker Material Links](http://documents.docker.co.kr/ )
[eBook](http://www.pyrasis.com/private/2014/11/30/publish-docker-for-the-really-impatient-book)


# Install
```
sudo wget -qO- https://get.docker.com/ | sh
```


# Image search on the server
```
docker search ubuntu
```

# Image Download
```
docker pull ubuntu:latest
```
Remove the Image `docker rmi ubuntu:latest`
# List the DL images  
```
docker images
```

# Create Container 
```
docker run -i -t --name Ubuntu ubuntu /bin/bash
```

Remove the Container `docker rm Ubuntu`

# Check the running status 
```
docker ps -a
```

# Start the Container
```
docker start Ubuntu
```

# Connect/Use the Container 
```
docker attach Ubuntu
```

# Exit the container
```
Ctrl + C
```

# Stop the Container 
```
docker stop Ubuntu
```





# QuarkusDemo
Quarkus-vs-Springboot


## Inspect containers
To inspect the running containers I use Portainer
Web based and easy to set up:
```
docker run -d -p 9000:9000 \
-v /var/run/docker.sock:/var/run/docker.sock \
portainer/portainer
```
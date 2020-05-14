
### Build Spring boot app
```
mvn install
```

### Run Spring boot app
```
mvn spring-boot:run
```

### Create Docker Image for Spring boot app
```
mvn install dockerfile:build 

```

### Run created Docker image Springboot app
```
docker run -i --rm -p 8082:8082 demo/springboot-echo
```

# Start Both Docker Containers
```
docker run --name springboot --rm -p 8082:8082 demo/springboot-echo
docker run --name quarkus --rm -p 8081:8081 demo/quarkus-echo
```
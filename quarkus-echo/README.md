#### Use the Maven Plugin to create a Quarkus skeleton app
```bash
mvn io.quarkus:quarkus-maven-plugin:1.0.0.CR2:create \
    -DprojectGroupId=demo.combat.quarkus \
    -DprojectArtifactId=quarkus-echo \
    -DclassName="demo.combat.quarkus.EchoResource" \
    -Dpath="/echo"
```

#### Test Quarkus app locally
```
mvn compile quarkus:dev

curl -sw "\n\n" http://localhost:8081/echo/quarkus | jq .
```

### Download and decompress the GraalVM
```
https://github.com/graalvm/graalvm-ce-builds/releases
For Quarkus 1.0 - GraalVM Version must be 19.2.1

```

#### We need the GraalVM environment variable set
```
export GRAALVM_HOME=[location]/graalvm-ce-19.2.1/Contents/Home/
```


## Running Quarkus Application - Native Executable 
#### Create a Native App of current Platform (MacOS) 
```
mvn package -Pnative
```
#### Create a Native App on a specific Plataform (Linux) - With this command we have a Native Linux executable of the this MicroServices (Everything in once file - JVM, App and Dependencies)
```
mvn package -Pnative -Dquarkus.native.container-build=true
```


### Generate the Docker Image of our App
```
docker build -t demo/quarkus-echo -f src/main/docker/Dockerfile.native .
```

#### Generate distroless image of app
```
docker build -t demo/quarkus-echo -f src/main/docker/Dockerfile.native-distroless .
```

### Create a Container from our generated Docker Image
```
docker run -i --name quarkus-echo --rm -p 8081:8081 demo/quarkus-echo 
```

### Docker Image for SpringBootBenchmarkApp
```
mvn install dockerfile:build  
docker run -i --rm -p 8082:8082 demo/springboot-app

# Start Both Docker Containers
docker run --name springboot --rm -p 8082:8082 demo/springboot-echo
docker run --name quarkus --rm -p 8081:8081 demo/quarkus-echo
```



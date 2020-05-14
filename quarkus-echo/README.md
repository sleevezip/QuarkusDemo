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

### Install GraalVM
```
https://www.graalvm.org/getting-started/
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
docker build -t demo/quarkus-echo-distroless -f src/main/docker/Dockerfile.native-distroless .
```

### Create a Container from our generated Docker Image
```
docker run -i --name quarkus-echo --rm -p 8081:8081 demo/quarkus-echo 
```



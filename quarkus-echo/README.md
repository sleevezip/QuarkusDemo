#### Use the Maven Plugin to create a Quarkus skeleton app
```
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
or just navigate to http://localhost:8081/echo/quarkus

By running the application with `dev` profile it allows so called Hot Deployments, which means when you make changes to any Java, resource or configuration files and re-hit the application, your new changes will immediately take effect – no downtime. Re-hitting the application essentially triggers a scan of the workspace and if there are any changes detected by Quarkus then the affected files are recompiled, and the application is redeployed, and your new request is then handled by the recompiled code.

### Install GraalVM
```
https://www.graalvm.org/getting-started/
```

## Running Quarkus Application - Native Executable 
#### Create a Native App on a specific Plataform (Linux) - With this command we have a Native Linux executable of the this MicroServices (Everything in one file - JVM, App and Dependencies)
```
mvn package -Pnative -Dquarkus.native.container-build=true
```


### Generate the Docker Image of App
```
docker build -t demo/quarkus-echo -f src/main/docker/Dockerfile.native .
```

#### Generate distroless image of app
```
docker build -t demo/quarkus-echo-distroless -f src/main/docker/Dockerfile.native-distroless .
```

### Run the generated Docker Image
```
docker run -i --name quarkus-echo --rm -p 8081:8081 demo/quarkus-echo 
```



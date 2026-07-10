
## Make EC2 Machine

```bash
sudo apt-get update
sudo apt-get install docker.io
sudo systemctl status docker
```


## check running container
```bash
docker ps
```
## check username
```bash
whoami
```
## Add current user in docker group 
```bash
sudo usermod -aG docker $USER
newgrp docker
```


## Login Docker hub for image pull and push 

## Generate Personal access Token
```bash
docker login -u amitsaini4210
password: ***********
```
```bash
mkdir projects
cd projects
git clone https://github.com/amitsaini4210/simple-java-docker.git
```

## Make Dockerfile
```bash
# pull a base image which gives all required tools and libraries
FROM openjdk:17-jdk-alpine

# create a folder where the app code will be stored
WORKDIR /app

# Copy the source code from your HOST machine to your container
COPY src/Main.java /app/Main.java

# compile the application code
RUN javac Main.java

# run the application
CMD ["java", "Main"]
```

## Build image using Dockerfile
```bash
docker build -t java-app .
```
## show all images
```bash
docker images
```
## Run your application
```bash
docker run java-app
```










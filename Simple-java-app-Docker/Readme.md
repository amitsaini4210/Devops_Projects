
## Make EC2 Machine

```bash
sudo apt-get update
sudo apt-get install docker.io
sudo systemctl status docker
```


## check running container
```bash
Docker ps
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



### Login Docker hub for image pull and push 

## Generate Personal access Token
```bash
Docker login -u amitsaini4210
password: ***********
```
```bash
mkdir Projects
cd Projects
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
Docker build -t java-app .
```
## show all images
```bash
Docker images
```
## Run your application
```bash
Docker run java-app
```

<img width="589" height="35" alt="3" src="https://github.com/user-attachments/assets/c9404a85-894c-4e7c-9b22-c6ed288ee68e" />










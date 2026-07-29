# Deploy two tier flask app using Jenkins with sending email 

<img width="2040" height="512" alt="project_flow" src="https://github.com/user-attachments/assets/7aacc7bc-da1b-4cfa-aaa7-5f092adb6493" />


# Make a ubuntu machine

### Install Docker
```bash
sudo apt-get update
sudo apt-get install docker.io
```

### Install Java
Jenkins requires Java to run first install java

```bash
sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version 
```


## installing jenkins

```bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins 
```


### Add 8080 port in AWS give right to itself IP

### get Login password of Jenkins
```bash
  /var/lib/jenkins/secrets/initialAdminPassword
```



### Add Current logged in user and Jenkins  in Docker group 
```bash
Sudo usermod -aG docker $USER
Newgrp docker 
Sudo usermod -aG docker jenkins 
sudo apt install docker-compose-v2
```

### Save DockerHub Login Credential in Jenkins
<img width="802" height="180" alt="dockerhub" src="https://github.com/user-attachments/assets/5428a4e8-2c52-48c2-99ff-704f3c2edd31" />



### install Trivy for file scanning

```bash
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install -y trivy
```

## making a Pipeline for
```bash
pipeline {
    agent any;
    
    stages{
        stage("pull code"){
            steps{
                git url: "https://github.com/amitsaini4210/two-tier-flask-app.git" , branch: "main"
            }
        }
        stage("build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
            
        }
      stage ("Trivy file scan"){
            steps{
                sh "trivy fs . "
            }
        }
        stage ("test"){
            steps{
                echo "Developer / Tester tests likh ke dega..."
            }
        }
        stage ("Push to dockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCreds",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser")]){
                     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                     sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                     sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
            }
        }
        stage ("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app "
            }
        
        }
    }
    post{
        success{
            script{
                emailext from: 'yourmail@gmail.com',
                to: 'yourmail@gmail.com',
                body: 'Build success for Demo CICD App',
                subject: 'Build success for Demo CICD App'
            }
        }
        failure{
            script{
                emailext from: 'yourmail@gmail.com',
                to: 'yourmail@gmail.com',
                body: 'Build Failed for Demo CICD App',
                subject: 'Build Failed for Demo CICD App'
            }
        }
    }
    
}
```


<img width="801" height="201" alt="jenkins" src="https://github.com/user-attachments/assets/6f84c390-3fa6-4297-9761-942956527dbd" />
<img width="793" height="483" alt="app" src="https://github.com/user-attachments/assets/59e65b2b-b73d-4c50-84f7-63f79bab36f0" />








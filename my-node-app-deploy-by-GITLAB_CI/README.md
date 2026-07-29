# Push Projects From Local to GITLAB
### Initialize Git (if not already done):

```bash
git init
git add .
git commit -m "Initial commit "
```


# Add Remote:
#### Rename existing origin if needed
```bash
git remote rename origin old-origin
```

#### Add new GitLab remote
```bash
git remote add origin git@gitlab.com:username/project-name.git   
```

#### Push:
```bash
git push -u origin main
```

# make .gitlab-ci.yml 

code

### Add variables
 <img width="1272" height="367" alt="add variable" src="https://github.com/user-attachments/assets/efbe6b9d-6fc2-42ef-8f02-33cc45c1a4e1" />


### ADD Runners
Project =>  Setting  =>  CI/CD   => Add Linux machine where app will run 

# GitLab Runner must be installed before you can register a runner. How do I install GitLab Runner? 


### Download the binary for your system
```bash
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
```
### Give it permission to execute
```bash
sudo chmod +x /usr/local/bin/gitlab-runner
```

### Create a GitLab Runner user

```bash
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

```
### Install and run as a service
```bash
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start
```

### register the runner.
```bash
gitlab-runner register  --url https://gitlab.com  --token glrt-VrxPrqNV5aas3z4s7VSrLGM6MQpvOjEKcDoxZWphMHUKdDozCnU6bjEwbzAc.01.1o1hgqrjh
```

### check status of runner
```bash
gitlab-runner status
```
<img width="1296" height="375" alt="runner" src="https://github.com/user-attachments/assets/511d462c-d728-40f3-9566-f7e948a9b37b" />



## App Run on 
```bash
http://localhost:3000
```

<img width="777" height="196" alt="app" src="https://github.com/user-attachments/assets/e45d559e-62f0-4757-868e-d1301df9f893" />








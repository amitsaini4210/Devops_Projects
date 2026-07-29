# Push Projects From Local to GITLAB
### Initialize Git (if not already done):

```bash
git init
git add .
git commit -m "Initial commit "
```


# Add Remote:

### Rename existing origin if needed
```bash
git remote rename origin old-origin
```

### Add new GitLab remote
```bash
git remote add origin git@gitlab.com:username/project-name.git   
```
### Push:

```bash
git push -u origin main
```

# make .gitlab-ci.yml 




### ADD Runners
project =>  Setting  =>  CI/CD   => add Linux machine where app will run 

### GitLab Runner must be installed before you can register a runner. How do I install GitLab Runner? 


# Download the binary for your system
```bash
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
```
# Give it permission to execute
```bash
sudo chmod +x /usr/local/bin/gitlab-runner
```

# Create a GitLab Runner user

```bash
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

```
# Install and run as a service
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


### App Run on 
```bash
http://localhost:3000
```

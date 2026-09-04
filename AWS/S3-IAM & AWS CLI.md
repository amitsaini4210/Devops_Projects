
# Make Your S3 Bucket
### Create a private S3 bucket in AWS.

<img width="1094" height="358" alt="Screenshot 2026-09-04 113626" src="https://github.com/user-attachments/assets/3c4ddc6e-3db9-46e3-a1f4-6625b6c98209" />

---


Make IAM Role and Group 

### 1. Open IAM Console
  - [ ] Go to the AWS Management Console.
  - [ ]   Enter "IAM" in the search bar and go to the IAM console.
- [ ]  Notice the IAM service is global and doesn't require region selection.
### 2. Viewing Current Users
 - [ ] On the left-hand side, click on "Users" to view the current user list.
### 3. Create a New IAM User and Set Password
- [ ]  Click on "Create user."
- [ ]  Enter a username (e.g., admin).
- [ ]  Select "Provide user access to the AWS Management Console."
- [ ]  Choose "I want to Create an IAM user" option.
 - [ ] Choose "Custom password" and enter your password.
 - [ ] Uncheck "Users must create a new password at next sign-in.”
- [ ]  Click "Next".
### 4. Create a User Group and Assign Permissions
 - [ ] Choose "Add user to group."
 - [ ] Click "Create group."
 - [ ] Name the group (e.g., administration).
 - [ ] Attach "AdministratorAccess" policy to the group.
 - [ ] Click "Create user group".
- [ ]  Add the user to the newly created admin group by selecting the group.
 - [ ] Click "Next".
### 5. Review and Create User
 - [ ] Review the settings: username, permissions, groups, etc.
 - [ ] Optionally, add tags (e.g., department: engineering).
 - [ ] Click "Create user."
### 6. Verify User and Group Setup
 - [ ] Optionally, download the CSV file for sign-in credentials.
 - [ ] View the user list to ensure the user is created.
 - [ ] Verify the user belongs to the "administration" group.
 - [ ] Check the "administration" group to confirm "AdministratorAccess" policy is attached.
### 7. Create an Account Alias (Optional)
 - [ ] Go to your AWS IAM Dashboard.
 - [ ] Create an account alias (e.g., aws-adminaccess-v2).
### 8. Sign in with IAM User
 - [ ] Open a new private browser window.
 - [ ] Use the IAM sign-in URL.
 - [ ] Enter account alias or account ID, and IAM username (e.g., admin).
 - [ ] Enter the IAM user password to log in.
 - [ ] Check the top right to ensure you're signed in as the IAM user.


<img width="1605" height="242" alt="IAM user" src="https://github.com/user-attachments/assets/0fa47c19-a174-4ef2-8c04-a22a3692f5df" />

# Configure and Install AWSCLI
```bash
sudo apt update
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

```
### Verify Installation
```bash
aws --version
```
# Configuration
Before using the AWS CLI, you need to configure your AWS credentials.

```bash
$ aws configure
AWS Access Key ID: MYACCESSKEY
AWS Secret Access Key: MYSECRETKEY
Default region name [us-west-2]: us-west-2
Default output format [None]: json
```

# Launch EC2 Using CLI
Create an EC2 instance using AWS CLI.

# Create Key pair
```bash
aws ec2 create-key-pair --key-name MyKeyPair

```
# Create Security Group to attach to ec2 instance
```bash
aws ec2 create-security-group --group-name=my-sg --description="My security group"

```
# Add inbound rule to security-group
```bash
aws ec2 authorize-security-group-ingress --group-id=sg-0732102fbf4ea2fe3 --protocol=tcp --port=443 --cidr=0.0.0.0/0
aws ec2 authorize-security-group-ingress --group-id=sg-0732102fbf4ea2fe3 --protocol=tcp --port=22 --cidr=0.0.0.0/0
aws ec2 authorize-security-group-ingress --group-id=sg-0732102fbf4ea2fe3 --protocol=tcp --port=80 --cidr=0.0.0.0/0

```
# Create instance
```bash
aws ec2 run-instances --image-id=ami-0fc5d935ebf8bc3bc --instance-type=t2.micro --region=us-east-1 --key-name=MyKeyPair --security-groups=my-sg

```

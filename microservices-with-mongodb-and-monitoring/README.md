## 📝 Introduction:

This project aims to provide a real-time chat experience that's both scalable and secure. With a focus on modern technologies, we're building an application that's easy to use and maintain.


## Detailed Workflow Description:


![image](https://github.com/user-attachments/assets/f845a188-8e70-42f7-8577-30af38e83053)


  - **User Interaction:**
    - Users interact with the frontend application running in their browser. This includes actions like logging in, sending messages, and navigating through the chat interface.Frontend (React App):The frontend is responsible for rendering the user interface and handling user inputs.It communicates with the backend via HTTP requests (for RESTful APIs) and WebSocket connections (for real-time interactions).

    - **Backend (Node.js/Express + Socket.io):**
       - The backend handles all the server-side logic.It processes API requests from the frontend to perform actions such as user authentication, message retrieval, and message storage.Socket.io is used to manage real-time bi-directional communication between the frontend and the backend. This allows for instant messaging features, such as showing when users are typing or when new messages are sent.


    - **MongoDB (Database):**
       - MongoDB stores all persistent data for the application, including user profiles, chat messages, and any other relevant data.The backend interacts with MongoDB to retrieve, add, update, or delete data based on the requests it receives from the frontend.




## ✨ Features:


* **Real-time Messaging**: Send and receive messages instantly using Socket.io 
* **User Authentication & Authorization**: Securely manage user access with JWT 
* **Scalable & Secure Architecture**: Built to handle large volumes of traffic and data 
* **Modern UI Design**: A user-friendly interface crafted with React and TailwindCSS 
* **Profile Management**: Users can upload and update their profile pictures 
* **Online Status**: View real-time online/offline status of users 



# Make a ubuntu machine
### Install Docker
```bash
sudo apt-get update
sudo apt-get install docker.io

```
### Add user in Docker Group

```bash
Sudo usermod -aG docker $USER
Newgrp docker 
```


## install kind clusters
```bash
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.32.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```


## install kubectl
```bash
curl -LO 
"https://dl.k8s.io/release/
$(
curl -L -s https://dl.k8s.io/release/stable.txt
)
/bin/linux/amd64/kubectl"

chmod +x kubectl
sudo mv kubectl /usr/local/bin
```

## check install Docker, Kubectl, kind-cluster
```bash
kubectl version
docker --version
kind --version
```

<img width="727" height="205" alt="1" src="https://github.com/user-attachments/assets/872d5d80-39d9-46a5-9d89-595b23c01dc2" />


### write config file for making cluster with the name ⇒   config.yml

### create cluster
```bash
kind create cluster   -- name=my-cluster - - config=config.yml
Kubectl get nodes
```

## 📝 Setup .env File:


1. Navigate to the `backend` directory:
```bash
cd backend
```
2. Create a `.env` file and add the following content (modify the values as needed):
```env
MONGODB_URI=mongodb://mongoadmin:secret@mongodb:27017/dbname?authSource=admin
JWT_SECRET=your_jwt_secret_key
PORT=5001
```
> **Note:** Replace `your_jwt_secret_key` with a strong secret key of your choice.

### Clone the Repository

```bash
git clone https://github.com/iemafzalhassan/full-stack_chatApp.git
```


### Login Docker Hub
```bash
docker login
```

```bash
Docker build -t amitsaini4210/chatapp-backend:latest .
Docker push amitsaini4210/chatapp-backend:latest


Docker build -t amitsaini4210/chatapp-frontend:latest .
Docker push amitsaini4210/chatapp-frontend:latest
```

# Install Metric-Server
if you are using a kind cluster install metrics server
```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
Edit the metrics server deployment
```bash
kubectl -n kube-system edit deployment metrics-server
```
Add the security bypass to deployment under 'container.args' for testing only
```bash
- --kubelet-insecure-tls
- --kubelet-preferred-address-types=InternalIP,Hostname,ExternalIP
```
Restart the deployment
```bash
kubectl -n kube-system rollout restart deployment metrics-server
kubectl top node
```
<img width="946" height="95" alt="top nodes" src="https://github.com/user-attachments/assets/34dbe3ee-60c9-405f-bbfa-608a1f01c9ae" />




# Apply K8S .yml file 
```bash
kubectl apply -f namespace.yml	
kubectl apply -f mongodb.pv.yml	
kubectl apply -f mongodb.pvc.yml	
kubectl apply -f .
```

# Get Service and Port-forward on Port 
```bash
kubectl get svc -n chat-app
kubectl port-forward service/backend -n chat-app 5001:5001 &
kubectl port-forward service/frontend-n chat-app 8080:80 
```
### Check Running App on Local host
<img width="1049" height="508" alt="chat-app" src="https://github.com/user-attachments/assets/8ff04540-6127-4849-b788-02b98ef9b5b3" />


### Mkdir  monitoring
Install helm then ⇒
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4
chmod 700 get_helm.sh
./get_helm.sh
```

### Create namespace for monitoring 
```bash
kubectl create namespace monitoring

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo list

helm repo update
```
```bash
helm install prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitoring --set prometheus.service.nodePort=30000 --set grafana.service.nodePort=31000 --set grafana.service.type=NodePort --set prometheus.service.type=NodePort

```
```bash
kubectl get pods -n monitoring 
kubectl get svc -n monitoring 

kubectl port-forward svc/prometheus-stack-kube-prom-prometheus 9090:9090 -n monitoring --address=0.0.0.0
```

### Go aws active port 9090 and then   ip:9090
### Grafana forward port⇒

```bash
kubectl port-forward svc/prometheus-stack-grafana 3000:80 -n monitoring --address=0.0.0.0 &
```


### Helm auto connect prometheus and grafana 

# Acess Prometheus
### http://localhost:9090/metrics  ⇒ Application jo data prometheus ko bhejta hai show karta hai
<img width="1219" height="651" alt="prom" src="https://github.com/user-attachments/assets/d4300141-49e4-4a99-be00-640553f6ea05" />


# Access Grafana
### Get Grafana Password
```bash
kubectl get secret prometheus-stack-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 --decode 
```
### http://localhost:3000  ⇒ Grafana Running

<img width="1188" height="715" alt="grafana" src="https://github.com/user-attachments/assets/d634bc24-837b-4ba9-8c3f-90ad87e3be95" />

---


This project is licensed under the MIT License. See the LICENSE file for more details.

# Deploy SpringBoot Application with MySQL on K8S
# Steps
1. Launch an instance from an Amazon Linux 2 or Amazon Linux AMI.
2. Connect to the instance.
3. Update the packages and package caches installed in the instance.
- yum update -y
4. Install the latest Docker Engine packages.

## Amazon Linux 2 amazon-linux-extras install 
- docker yum install docker -y
## Start the Docker service.
systemctl start docker 
systemctl enable docker

## Install Conntrack:

yum install conntrack -y

## Install minikube

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo install minikube-linux-amd64 /usr/local/bin/minikube

## Start Minikube

/usr/local/bin/minikube start --force --driver=docker

/usr/local/bin/minikube version

## Install kubectl

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

/usr/local/bin/kubectl version

## Make the DB up

yum install maven -y	

## Create the docker image

docker build -t azizulmaqsud/springboot-crud-k8s:1.0 .

## docker login

 /usr/local/bin/kubectl  apply -f app-deployment.yaml

 /usr/local/bin/kubectl  get svc

 /usr/local/bin/minikube ip

 http://<minikubeIP>:31125/orders


## PUT PORT FORWARD

 /usr/local/bin/kubectl port-forward --address 0.0.0.0 svc/springboot-crud-svc 8080:8080 &

## HOST PORT TO CONTAINER PORT 

kubectl port-forward --address 0.0.0.0 svc/{your service name} {external port to the Internet}:{your service port, the port your app is listening on in it's container}

for example, if your service is named petstore and is listening on 80

kubectl port-forward --address 0.0.0.0 svc/petstore 8888:80




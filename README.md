# helm-blue-gree-for-springboot-mysql

## Pre-Requisites

```bash
1. Install GIT
2. Install Java
3. Install Maven
4. Minikube Setup
5. Helm Install
```

## Install JAVA-8, GIT and Maven

```bash
yum install java-1.8.0-openjdk -y
yum install git -y
yum install maven -y
```
## kubernetes cluster - minikube
```kubectl (install)```

```bash
curl -o kubectl https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/kubectl
chmod +x ./kubectl
mv kubectl /usr/bin
kubectl version --short --client
```

```Install docker```

```bash
yum install docker -y
service docker start
```

```Minikube setup```

```bash
curl -Lo minikube https://github.com/kubernetes/minikube/releases/download/v1.25.2/minikube-linux-amd64
chmod +x minikube
sudo mv minikube /usr/bin/
yum install conntrack -y
minikube start --driver=none
```

## Install helm

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
export PATH=$PATH:/usr/local/bin
./get_helm.sh
```

## Update Secret Values and Run

```bash
kubectl apply -f helm/mysql-secrets.yaml
```

# Deploy Helm Chart 

```bash
helm repo add helm-repo https://charts.bitnami.com/bitnami
helm install mysql-release helm-repo/mysql --dry-run --debug -f helm/mysql/mysql-values.yaml
helm install mysql-release helm-repo/mysql -f helm/mysql/mysql-values.yaml
```

## Build and Deploy Springboot Applcation with helm

1. Build Springboot Applocation

```bash
mvn clean install
```

2. Build and Push docker image

```bash
docker build -t soumya6304/springboothello:v1 .
docker login
docker push soumya6304/springboothello:v1
```

3. Deploy Springboot Application

```bash
helm install springboothello helm/springboot-example
```

## Check application in UI
![image](https://user-images.githubusercontent.com/101722548/210037227-fdb07935-fe48-4a5d-a302-f6f0efcb58eb.png)

# jenkins
**Jenkins server setup with Helm to deploy into Kubernetes cluster**


**#Install and Configure Maven & git in Jenkins server**

Install Maven

yum install wget
wget https://mirror.lyrahosting.com/apache/maven/maven-3/3.8.1/binaries/apache-maven-3.8.1-bin.tar.gz
tar -xvzf apache-maven-3.8.1-bin.tar.gz
export M2_HOME=/opt/apache-maven-3.8.1
export M2=$M2_HOME/bin
PATH=$PATH:$M2
# To set it permanently update your .bash_profile
source ~/.bash_profile
<img width="530" alt="image" src="https://user-images.githubusercontent.com/12380898/151609770-826c85e8-35d7-4bb1-8a49-4edc3253779c.png">


Validate Maven

mvn version
Install git

yum install git

Assign shell to jenkins user

vi /etc/passwd
change shell from /bin/false to /bin/bash

##########################################

Install Docker

yum install docker
systemctl start docker
systemctl enable docker
provide permissions to jenkins user in jenkins server to access docker

  sudo groupadd docker
  sudo usermod -aG docker jenkins
  sudo chmod 777 /var/run/docker.sock
Add Jenkins user into sudoers file to get sudo access

   vi /etc/sudoers
   jenkins ALL=(ALL) NOPASSWD: ALL
   
   
#####################################################

**pre-requisites Pluging installation in Jenkins** 
1. docker pipeline
2. maven integration



################################################################################################
Download and Install helm

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
Test with helm command

helm version
helm list
Copy config file from EKS Management host to Jenkins home directory

mkdir /var/lib/jenkins/.kube

copy config file under .kube directory with jenkins ownership (chmod 600 ) 
helm repo list
######
helm repo add stable https://charts.helm.sh/stable
helm repo search <chartname>
helm search repo stable stable/nginx

helm install repo stable/<chartname> <releasename>
  
helm pull <chartname>
helm pull stable/nginx-ingress
  
helm package <chartname>

helm uninstall RELEASE_NAME



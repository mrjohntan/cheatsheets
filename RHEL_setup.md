# RHEL Setup

# Setup Docker

sudo vi /etc/yum.repos.d/docker.repo

[docker-ce-stable]
name=Docker CE Stable - $basearch
baseurl=https://download.docker.com/linux/rhel/9/$basearch/stable
enabled=1
gpgcheck=1
gpgkey=https://download.docker.com/linux/rhel/gpg

sudo yum install docker-ce --nobest

sudo systemctl start docker
sudo systemctl enable docker

sudo usermod -aG docker $USER && newgrp docker

# Setup VS Code

sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'

dnf check-update
sudo dnf install code

# Setup Kubectl

cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.29/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.29/rpm/repodata/repomd.xml.key
EOF

sudo yum install -y kubectl

# Setup Minikube

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-latest.x86_64.rpm
sudo rpm -Uvh minikube-latest.x86_64.rpm


# Setup istioctl

curl -sL https://istio.io/downloadIstioctl | sh -

export PATH=$HOME/.istioctl/bin:$PATH

source ~/istioctl.bash

# Setup Java

sudo yum install -y https://cdn.azul.com/zulu/bin/zulu-repo-1.0.0-1.noarch.rpm

sudo yum install zulu21-jdk

export PATH=/usr/lib/jvm/java-21-zulu-openjdk/bin:$PATH

# Setup Jetbrains

https://download.jetbrains.com/toolbox/jetbrains-toolbox-2.2.3.20090.tar.gz?_gl=1*115fong*_ga*MTkwNzAyNjAxNS4xNzExMTc3NTkw*_ga_9J976DJZ68*MTcxMTE3NzU4OS4xLjEuMTcxMTE3NzY0OC4wLjAuMA..

sudo tar -zxf jetbrains-toolbox-2.2.3.20090.tar.gz -C /opt

./opt/jetbrains-toolbox-2.2.3.20090/jetbrains-toolbox

# Setup Nodejs NPM

sudo yum install npm -y

# Setup dotnet

sudo yum install dotnet-sdk-8.0 -y

# Setup Helm

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
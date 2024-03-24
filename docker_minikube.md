# Setup Ubuntu Docker Minikube

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list &gt; /dev/null

sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release -y

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io -y

sudo usermod -aG docker $USER

wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo cp minikube-linux-amd64 /usr/local/bin/minikube

sudo chmod +x /usr/local/bin/minikube

curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

chmod +x kubectl

sudo mv kubectl /usr/local/bin/

minikube start --driver=docker --cpus 4 --memory 16g --disk-size 32g

minikube addons enable metallb

minikube addons configure metallb

192.168.49.1

-- Enter Load Balancer Start IP: 192.168.49.200
-- Enter Load Balancer End IP: 192.168.49.225

minikube addons enable metrics-server

git clone https://github.com/kubernetes/kube-state-metrics
kubectl apply -f kube-state-metrics/examples/standard/

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo add grafana https://grafana.github.io/helm-charts

helm install monitoring prometheus-community/kube-prometheus-stack

helm install monitoring prometheus-community/kube-prometheus-stack


helm repo update

helm install grafana grafana/grafana -n monitoring
helm install prometheus prometheus-community/prometheus -n monitoring


minikube stop – Stops the Minikube cluster
minikube delete – Deletes the Minikube cluster and its resources
rm -rf /usr/local/bin/minikube – Removes the Minikube binary
rm -rf ~/.minikube – Deletes Minikube configuration and VM files
rm -rf /usr/local/bin/kubectl – Removes the kubectl binary (if installed)

eval $(minikube docker-env)

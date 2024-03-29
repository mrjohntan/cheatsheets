# Setup Istio for Kubernetes

istioctl install --set profile=default

kubectl label namespace default istio-injection=enabled --overwrite

kubectl get namespace -L istio-injection
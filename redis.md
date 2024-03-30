# Setup Redis Ubuntu

curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list

sudo apt-get update

sudo apt-get install redis


# Setup Redis Kubernetes

helm install redis -n default --set architecture=standalone oci://registry-1.docker.io/bitnamicharts/redis

Pulled: registry-1.docker.io/bitnamicharts/redis:19.0.1
Digest: sha256:46f3a93a617fe836cdb8d11220b38d2231e023222f1b535b3510e58775bf4e57
NAME: redis
LAST DEPLOYED: Sat Mar 30 09:14:44 2024
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: redis
CHART VERSION: 19.0.1
APP VERSION: 7.2.4

** Please be patient while the chart is being deployed **

Redis&reg; can be accessed via port 6379 on the following DNS name from within your cluster:

    redis-master.default.svc.cluster.local



To get your password run:

    export REDIS_PASSWORD=$(kubectl get secret --namespace default redis -o jsonpath="{.data.redis-password}" | base64 -d)

To connect to your Redis&reg; server:

1. Run a Redis&reg; pod that you can use as a client:

   kubectl run --namespace default redis-client --restart='Never'  --env REDIS_PASSWORD=$REDIS_PASSWORD  --image docker.io/bitnami/redis:7.2.4-debian-12-r9 --command -- sleep infinity

   Use the following command to attach to the pod:

   kubectl exec --tty -i redis-client \
   --namespace default -- bash

2. Connect using the Redis&reg; CLI:
   REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h redis-master

To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace default svc/redis-master 6379:6379 &
    REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h 127.0.0.1 -p 6379

WARNING: There are "resources" sections in the chart not set. Using "resourcesPreset" is not recommended for production. For production installations, please set the following values according to your workload needs:
  - master.resources
  - replica.resources
+info https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/

# Kill K port-forward

ps -ef|grep port-forward

jt@lab:~$ ps -ef|grep port-forward
jt         27692    5685  0 09:24 pts/0    00:00:00 grep --color=auto port-forward

kill -9 27692

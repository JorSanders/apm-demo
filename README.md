# APM Server demo on K8s
Just a simple setup to get a apm-server and a kibana dashboard. Using a single node of elasticsearch

## Prequisite
 - A kubernetes cluster (I use minikube `minikube start --driver=docker start --memory 15977 --cpus 8`)
 - Kubectl installed

## Create the namespace
```shell
kubectl create namespace apm-demo
```

## Apply manifests
```shell
kubectl apply -f manifests
```

wait for pods to be running
```shell
watch kubectl get pods -n apm-demo
```

## Port forward to access Kibana and APM Server ports
```shell
kubectl port-forward deployment/apm-server 8200:8200 -n apm-demo
```

```shell
kubectl port-forward deployment/kibana 5601:5601 -n apm-demo
```

## Access kibana dashboard on localhost:8200
```shell
open http://localhost:5601/app/apm
```

## Configure APM clients to send data
https://www.elastic.co/guide/en/apm/agent/nodejs/current/nextjs.html


## Clean up
if you want to remove this setup just
```
kubectl delete namespace apm-demo

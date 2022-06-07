# Kubernetes Study

# Overview
Kubernetes project that will provide an environment with an accessible Web-based MongoDB admin interface and an instance of the Mongo database.

```
┌──────────────────┐
│   Mongo Express  │
│ External Service │
└────────┬─────────┘
         │
         │
    ┌────▼────┐
    │  Mongo  │          ┌────────────────┐       ┌───────┐
    │ Express ├─────────►│MongoDb Internal├──────►│MongoDb│
    │   Pod   │          │    Service     │       │  Pod  │
    └─▲─────▲─┘          └────────────────┘       └─▲───▲─┘
      │     │                                       │   │
      │     │                                       │   │
      │     │                                       │   │
      │     │                             ┌───────┐ │   │
      │     └─────────────────────────────┤Secrets├─┘   │
      │                                   └───────┘     │
      │                                                 │
      │                                  ┌─────────┐    │
      └──────────────────────────────────┤ConfigMap├────┘
                                         └─────────┘
```


## Requirements
- Docker
- Kubectl
- Minikube

## Instructions
Run the below commands
```
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo.yaml
kubectl apply -f mongo-configmap.yaml 
kubectl apply -f mongo-express.yaml

// Check if the resources were created successfully
kubectl get all

// Apply an ip for the external service
minikube service mongo-express-service

// Access the desired service ip from the browser
minikube service --all

```
## Basic commands
### Encode base64 using terminal
```
echo -n 'value' | base64
```
### Create minikube cluster
```
minikube start
kubectl get nodes
minikube status
kubectl version
```
### kubectl commands
```
kubectl get all
kubectl get all | grep mongodb
kubectl get nodes
kubectl get pod
kubectl get pod -o wide
kubectl get services
kubectl create deployment mongo-deployment --image=mongo
kubectl get deployment
kubectl get replicaset
kubectl edit deployment mongo-deployment
```
### Debugging
```
kubectl logs {pod-name}
kubectl exec -it {pod-name} -- bin/bash
```
### Create mongo deployment
```
kubectl create deployment mongo-deployment --image=mongo
kubectl logs mongo-deployment-{pod-name}
kubectl describe pod mongo-deployment-{pod-name}
```
### Delete deployment
```
kubectl delete deployment mongo-depl
```
### Create or edit config file
```
vim mongo-deployment.yaml
kubectl apply -f mongo-deployment.yaml
kubectl get pod
kubectl get deployment
```
### Delete with config
```
kubectl delete -f mongo-deployment.yaml
``` 
### Get metrics
```
kubectl top
``` 
The top command returns the current CPU and memory usage for a cluster’s pods or nodes, or for a particular pod or node if specified.

### Exposing an external service using minikube
```
minikube service mongo-express-service
minikube service --all
```
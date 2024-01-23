# Skooner is the easiest way to manage your Kubernetes cluster

- **Full cluster management**: Namespaces, Nodes, Pods, Replica Sets, Deployments, Storage, RBAC and more
- **Blazing fast and Always Live**: no need to refresh pages to see the latest cluster status
- **Quickly visualize cluster health at a glance**: Real time charts help quickly track down poorly performing resources
- **Easy CRUD and scaling**: plus inline API docs to easily understand what each field does
- **100% responsive** (runs on your phone/tablet)
- **Simple OpenID integration**: no special proxies required
- **Simple installation**: use the provided yaml resources to have skooner up and running in under 1 minute (no, seriously)
- **See Skooner in action**:<br>

<!-- ## Table of Contents

- [Installation](#Installation)
- [Read only user for developers]() -->


## Installation 

```bash
kubectl apply -f skooner.yaml
```

#### This will also create a Deployment/Service/Service Account for Skooner/Cluster Role Binding for with "skooner-sa" account as a super user for Skooner with Cluster full permissions


### To access the skooner in you laptop without NodePort or Loadbalancer for security you can use port forwarding


```bash 
 kubectl port-forward deployment/skooner --address 0.0.0.0 8090:4654 -n kube-system

```

Once we access ther skooner it will ask for authentication which we needed to generate using the bellow command 

```bash 
 kubectl create token skooner-sa -n kube-system
```


### Want to create readonly user to provide with developer for logs please apply readonlyuser.yaml with the bellow command.

```bash
kubectl apply -f readonlyuser.yaml
```

## Read only user for developers 

### Create the service account in the current namespace (we assume default)
```bash
kubectl create serviceaccount skooner-rou -n kube-system
```
### Give that service account root on the cluster
```bash
kubectl create clusterrolebinding skooner-rou --clusterrole=aks-cluster-readonly-role --serviceaccount=kube-system:skooner-rou -n kube-system
```
### To generate token for readonly-user
```bash
kubectl create token skooner-rou -n kube-system
```

### Find the secret that was created to copy the token for the SA
```bash
kubectl get secrets -n kube-system -n kube-system
```
### Show the contents of the secret to extract the token
```bash
kubectl describe secret skooner-rou-token-xxxxx
```


### skooner
Skooner dashboard GUI for Kubernets

```bash
kubectl apply -f skooner.yaml
```

This will create a Deployment/Service/Service Account for Skooner/Cluster Role Binding for skooner-sa account as a super user

## To access the skooner in you laptop for security you can use port forwarding

```bash 
 kubectl port-forward deployment/skooner --address 0.0.0.0 8080:4654 -n kube-system

```

Once we access ther skooner it will ask for authentication which we needed to generate using the bellow command 

```bash 
 kubectl create token skooner-sa 
```
## Want to create readonly user please apply readonlyuser.yaml with the bellow command  and follow above commands 

```bash
kubectl apply -f readonlyuser.yaml
```

# Read only user for developers 

# Create the service account in the current namespace (we assume default)
```bash
kubectl create serviceaccount skooner-rou -n kube-system
```
# Give that service account root on the cluster
```bash
kubectl create clusterrolebinding skooner-rou --clusterrole=aks-cluster-readonly-role --serviceaccount=kube-system:skooner-rou -n kube-system
```
# For Kubernetes v1.21 or lower
# Find the secret that was created to copy the token for the SA
```bash
kubectl get secrets -n kube-system
```
# Show the contents of the secret to extract the token
```bash
kubectl describe secret skooner-rou-token-xxxxx
```
# For Kubernetes v1.22 or higher
```bash
kubectl create token skooner-rou -n kube-system
```




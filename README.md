# azure-kube-101

# Create Kubernetes Cluster Using Azure CLI


**Note:** While AKS is in preview, only some location options are available. These are eastus, westeurope, centralus, canadacentral, canadaeast.

**Register providers**

```
az provider register -n Microsoft.Network
az provider register -n Microsoft.Storage
az provider register -n Microsoft.Compute
az provider register -n Microsoft.ContainerServicec
```
**Login with Azure**

```
az login
```

**Create a resource group**

```
az group create --name rg-kube-101 --location centralus
```

**Create AKS cluster**
This may take 10-20 minutes to finish
```
az aks create --resource-group rg-kube-101 --name kube101 --node-count 1 --generate-ssh-keys
```
List all AKS services under your subscription
```
az aks list -o table
```

If you don't have it installed,
Download and install kubectl, the Kubernetes command-line tool.

```
az aks install-cli
```

**Configure kubectl to connect to your Kubernetes cluster**

```
az aks get-credentials --resource-group rg-kube-101 --name kube101
```

```
kubectl get nodes
```

If you're using **PowerShell** you may create an alias for **kubectl** command as isn't the easiest command to type.
```
new-alias k kubectl
```

Working with [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) and [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/), check the links if you want to learn more about them



## Open Kubernetes dashboard

```
az aks get-credentials --resource-group rg-kube-101 --name kube101
```

```
az aks browse --resource-group rg-kube-101 --name kube101
```

**Delete Cluster**
```
az group delete --name rg-kube-101 --yes --no-wait
```

## Other Commands

List available contexts and  switch between clusters
```
kubectl config get-contexts
kubectl config use-context $NAME 
```

List all pods
```
kubectl get pods --all-namespaces
```

## Troubleshooting Guides
The rule of thumb is when you do `kubectl logs` or `kubectl exec` the API server makes a request _to the_ kubelet. If you experience problems then [refer to this cheat cheat](https://s.itho.me/day/2017/k8s/1020-1100%20All%20The%20Troubles%20You%20Get%20Into%20When%20Setting%20Up%20a%20Production-ready%20Kubernetes%20Cluster.pdf).

## References
* Azure Container Service with Kubernetes Documentation https://docs.microsoft.com/en-us/azure/container-service/kubernetes/
* https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough
* https://developer.atlassian.com/blog/2017/07/kubernetes-infra-on-aws/



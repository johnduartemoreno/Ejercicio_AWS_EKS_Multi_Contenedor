### 1. Eliminar el Pod y el Servicio en Kubernetes
Para eliminar los recursos que creaste (el pod y el servicio), usa los siguientes comandos en kubectl:

###Eliminar el pod multi-contenedor:

```bash
kubectl delete -f multi-container-pod.yaml
```

###Eliminar el servicio Nginx:

```bash
kubectl delete -f nginx-service.yaml
```

2. Eliminar el Clúster EKS
Si deseas eliminar el clúster de EKS que creaste, puedes hacerlo con eksctl:

```bash
eksctl delete cluster --name bootcamp-cluster --region us-east-1
```
Este comando eliminará el clúster de EKS, incluidos los nodos y todos los recursos asociados.

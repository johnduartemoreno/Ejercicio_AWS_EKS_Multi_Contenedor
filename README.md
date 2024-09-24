
# Ejercicio Práctico: Desplegar una Aplicación Multi-Contenedor en Kubernetes (EKS)

## Objetivo
Desplegar una aplicación multi-contenedor en un clúster de Kubernetes en AWS EKS, utilizando pods que ejecuten dos contenedores: un servidor web (Nginx) y un contenedor de Redis para el almacenamiento en caché. Configura ambos contenedores para que se comuniquen entre sí y expongan el servidor web a través de un servicio de Kubernetes.

## Pasos

### 1. Crear el Clúster EKS en AWS

```bash
eksctl create cluster --name bootcamp-cluster --region us-east-1 --nodegroup-name linux-nodes --node-type t3.medium --nodes 3 --nodes-min 1 --nodes-max 4 --managed
```

### 2. Apuntar `kubectl` al Clúster EKS

```bash
aws eks update-kubeconfig --region us-east-1 --name bootcamp-cluster
```

### 3. Verificar la Conexión y el Estado del Clúster

1. Verificar el estado del clúster:

```bash
aws eks describe-cluster --name bootcamp-cluster --region us-east-1 --query "cluster.status"
```

2. Verificar los servicios predeterminados:

```bash
kubectl get svc
```

### 4. Crear y Desplegar el Pod Multi-Contenedor

1. Crear el archivo `multi-container-pod.yaml` y aplicarlo:

```bash
kubectl apply -f multi-container-pod.yaml
```

### 5. Exponer el Pod con un Servicio LoadBalancer

1. Crear el archivo `nginx-service.yaml` y aplicarlo:

```bash
kubectl apply -f nginx-service.yaml
```

### 6. Verificación Final

1. Verificar los Pods:

```bash
kubectl get pods
```

2. Verificar los logs de Nginx y Redis:

```bash
kubectl logs multi-container-pod -c nginx
kubectl logs multi-container-pod -c redis
```

3. Verificar el Servicio y obtener la IP externa:

```bash
kubectl get services
```
Verificar los endpoints y probar el acceso
```bash
kubectl get endpoints nginx-service
```

Probar el acceso al servicio: Usa curl o accede al servicio desde tu navegador usando la dirección del LoadBalancer para verificar que Nginx esté respondiendo

curl http://<tu-loadbalancer-external-ip>

---

### Archivos Incluidos
- `multi-container-pod.yaml`: Definición del pod con dos contenedores (Nginx y Redis).
- `nginx-service.yaml`: Archivo para exponer Nginx a través de un servicio LoadBalancer.

### Tiempo Estimado
1 hora


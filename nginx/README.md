
# Kubernetes Nginx Project

## Project Description
This project demonstrates the deployment of Nginx in a Kubernetes cluster, along with an Ingress configuration for routing traffic. It's designed as a learning exercise to understand how to deploy web servers, create services, and manage ingress in Kubernetes.

## Project Structure
The project consists of Kubernetes manifest files that define the necessary resources for deploying Nginx and setting up an Ingress controller.

### Key Components:
1. Nginx Deployment
2. Nginx Service
3. Ingress Resource for Kubernetes Dashboard

## Nginx Deployment

A Deployment resource is defined to run Nginx instances:

- Name: `nginx-deployment`
- Replicas: 2
- Image: `nginx:1.16`
- Container Port: 8080

Key features of this deployment:
- Uses Nginx version 1.16
- Runs two replicas for high availability
- Exposes port 8080 within the cluster

The deployment YAML looks like this:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.16
        ports:
        - containerPort: 8080
```

## Nginx Service

A Service resource is defined to expose the Nginx deployment:

- Name: `nginx-service`
- Type: ClusterIP (default)
- Port: 80
- Target Port: 8080

The service YAML looks like this:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

This service makes the Nginx deployment accessible within the cluster on port 80, forwarding traffic to the containers' port 8080.

## Ingress Resource

An Ingress resource is defined with the following key features:

- Name: `dashboard-ingress`
- Namespace: `kubernetes-dashboard`
- Ingress Class: `nginx`
- Host: `dashboard.com`
- Path: `/` (Exact match)
- Backend Service:
  - Name: `kubernetes-dashboard`
  - Port: 80

This Ingress resource is configured to route traffic from `dashboard.com` to the Kubernetes Dashboard service.

## Prerequisites
- Kubernetes cluster
- Nginx Ingress Controller installed in the cluster
- `kubectl` command-line tool
- Basic understanding of Kubernetes concepts

## Configuration
The project relies on the following:

1. A pre-existing Nginx Ingress Controller in the cluster
2. The Kubernetes Dashboard service running in the `kubernetes-dashboard` namespace (for the Ingress example)

Ensure these components are set up before applying the resources.

## Usage
To deploy the resources, apply the YAML files to your Kubernetes cluster:

```bash
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
kubectl apply -f dashboard-ingress.yaml
```

After applying:
1. The Nginx instances will be running in the default namespace.
2. The Nginx service will be available within the cluster.
3. Configure your DNS or local hosts file to point `dashboard.com` to the IP address of your Ingress Controller for the dashboard example.

## Accessing the Nginx Instances
To access the Nginx instances:

1. Within the cluster, other pods can access the service at `nginx-service:80`.
2. To access from outside the cluster, you may need to:
   - Use `kubectl port-forward` for testing purposes.
   - Create a NodePort or LoadBalancer service instead of ClusterIP.
   - Configure an Ingress resource for the Nginx service.

## Next Steps
- Set up TLS/SSL for secure access
- Configure additional paths or hosts in the Ingress as needed
- Implement authentication for the Ingress if required
- Consider updating the Nginx version if 1.16 is not the latest stable version
- Create an Ingress resource specifically for the Nginx service

## Monitoring and Scaling
- Monitor the Nginx deployment using Kubernetes dashboard or monitoring tools like Prometheus
- Scale the deployment up or down based on traffic needs:
  ```
  kubectl scale deployment nginx-deployment --replicas=3
  ```

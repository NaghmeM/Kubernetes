# Kubernetes MongoDB and Mongo Express Project

## Project Description
This project demonstrates the deployment of MongoDB and Mongo Express in a Kubernetes cluster. It's designed as a learning exercise to understand how to set up and configure these applications in a Kubernetes environment.

## Project Structure
The project consists of Kubernetes manifest files that define the necessary resources for running MongoDB and Mongo Express.

### Key Components:
1. MongoDB Deployment
2. MongoDB Service
3. Mongo Express Deployment
4. Mongo Express Service
5. MongoDB Secret
6. MongoDB ConfigMap

## MongoDB Deployment

The `mongodb-deployment` is defined with the following key features:

- Uses the `mongo` image
- Deploys 1 replica
- Exposes port 27017
- Configures environment variables for root username and password:
  - Values are fetched from the Kubernetes Secret named `mongodb-secret`

## MongoDB Service

A ClusterIP service (default type) is created to expose MongoDB within the cluster:

- Selector matches the `mongodb` deployment
- Port 27017 is exposed

## Mongo Express Deployment

The `mongo-express` deployment is defined with the following key features:

- Uses the `mongo-express` image
- Exposes port 8081
- Configures environment variables for MongoDB connection:
  - Admin username and password are fetched from the Kubernetes Secret named `mongodb-secret`
  - MongoDB server URL is fetched from the ConfigMap named `mongodb-configmap`

## Mongo Express Service

A LoadBalancer service is created to expose Mongo Express:

- Selector matches the `mongo-express` deployment
- Port 8081 is exposed
- NodePort is set to 31000

## MongoDB Secret

A Kubernetes Secret is used to store sensitive information:

- Secret Name: `mongodb-secret`
- Type: Opaque
- Data:
  - `mongo-root-username`: bmFqbWU= (base64 encoded)
  - `mongo-root-password`: amFzbWluNjIxMQ== (base64 encoded)

Note: The values in the Secret are base64 encoded. Make sure to replace these with your own encoded values in a real-world scenario.

## MongoDB ConfigMap

A ConfigMap is used to store non-sensitive configuration data:

- ConfigMap Name: `mongodb-configmap`
- Data:
  - `database_url`: mongodb-service

This ConfigMap is used to provide the MongoDB service name to the Mongo Express deployment.

## Prerequisites
- Kubernetes cluster
- `kubectl` command-line tool
- Basic understanding of Kubernetes concepts

## Configuration
All necessary configurations are included in the provided manifest files.

## Usage
To deploy the resources, apply the YAML files to your Kubernetes cluster in the following order:

```bash
kubectl apply -f mongodb-configmap.yaml
kubectl apply -f mongodb-secret.yaml
kubectl apply -f mongodb-deployment.yaml
kubectl apply -f mongo-express.yaml
```

Access Mongo Express through the NodePort 31000 or the LoadBalancer IP.

## Security Note
The Secret file contains sensitive information. In a production environment:
- Never commit secrets to version control
- Use a secure method to manage and inject secrets into your cluster
- Consider using tools like HashiCorp Vault or AWS Secrets Manager for enhanced security

## Learning Objectives
This project helps in understanding:
1. How to deploy stateful applications like MongoDB in Kubernetes
2. Using ConfigMaps for configuration management
3. Managing secrets in Kubernetes
4. Setting up services for internal (ClusterIP) and external (LoadBalancer) access
5. Connecting multiple services in a Kubernetes cluster

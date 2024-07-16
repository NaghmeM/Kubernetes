# Kubernetes Learning Journey

Welcome to my Kubernetes learning repository! This project documents my self-guided journey into DevOps and Kubernetes. As a self-learner, I believe in applying concepts hands-on to solidify my understanding.

## Project Structure

This repository contains two main projects, each in its own directory:

1. **MongoDB and Mongo Express Project**
   - Located in: `/Mongo-DB`
   - Demonstrates deploying a MongoDB database with Mongo Express frontend in Kubernetes.

2. **Nginx Project**
   - Located in: `/nginx`
   - Showcases deploying Nginx web server with associated services and ingress configurations.

## Learning Objectives

Through these projects, I aim to understand:

- Basic Kubernetes concepts (Pods, Deployments, Services)
- ConfigMaps and Secrets management
- Ingress controllers and routing
- Stateful applications in Kubernetes
- Service exposure and networking

## Key Learnings

- Kubernetes manifest file structure and syntax
- Deploying applications using kubectl
- Configuring environment variables in containers
- Setting up internal and external access to services

## Challenges and Notes

- In the MongoDB/Mongo Express project, I'm still figuring out how to properly set `ME_CONFIG_MONGODB_ENABLE_ADMIN` to true. The current setup uses default Docker configuration values for Mongo Express.

## Next Steps

- Implement proper security measures (e.g., non-default passwords, HTTPS)
- Explore Helm charts for easier deployment
- Dive into Kubernetes monitoring and logging
- Learn about CI/CD integration with Kubernetes

## Resources

- Official Kubernetes Documentation
- Online courses and tutorials (list specific ones you found helpful)
- Community forums and Stack Overflow

## Disclaimer

This repository is a learning project. Configurations may not be production-ready and are primarily for educational purposes.

## Contribution

While this is a personal learning project, I'm open to suggestions and corrections. Feel free to open an issue if you spot any mistakes or have improvement ideas!

Happy learning!
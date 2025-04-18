#  Best Buy Cloud-Native Application

##  Updated Application Architecture

The Best Buy application is built using a microservices-based, cloud-native architecture deployed on a Kubernetes cluster.

###  Architecture Diagram  
![diagram](https://github.com/user-attachments/assets/65827401-56ff-4888-a843-da006c27791d)


## Application and Architecture Explanation

This cloud-native e-commerce application includes multiple microservices that work together:

- **frontend-bestbuy**: A web-based user interface for customers to browse and purchase products.
- **productservice-bestbuy**: Handles product listings and inventory.
- **orderservice-bestbuy**: Manages customer orders.
- **storeadmin-bestbuy**: Admin portal to manage catalog and store settings.
- **makelineservice-bestbuy**: AI-powered service that generates product descriptions and images using GPT-4 and DALL·E.
- **aiservice-bestbuy**: Additional AI utilities.
- **mongodb**: Stores product and order data.
- **Azure Service Bus**: Facilitates asynchronous communication between services like order processing and makelineservice.

The application is containerized and deployed using Kubernetes for scalability and ease of management.

##  Deployment Instructions

1. **Clone Repositories**  
   Clone each microservice repo. for deployment.

2. **Build Docker Images**  
   For each service:
   ```example:
   docker build -t bestbuy-aiservice ./aiservice_bestbuy
   docker tag bestbuy-aiservice:latest nidhi0152/bestbuy-aiservice:latest
   docker push nidhi0152/bestbuy-aiservice:latest
   ```
3. **Setup Azure Service Bus**
   Update the relevant service configuration with the Azure Service Bus connection string.
   ```example:
   - name: ORDER_QUEUE_URI
              value: "amqp://bestbuy.servicebus.windows.net" # servicebus connection string
            - name: ORDER_QUEUE_USERNAME
              value: "listner"
            - name: ORDER_QUEUE_PASSWORD
              value: "fQWy3YXUPlNz8WYcG8//5SolwJRRaNZp6+ASbMCPnw4="
   ```
4. **Configure Kubernetes Manifests**  
   Apply Kubernetes YAML configuration files including deployments, configmaps, and secrets:
   ```example:
   kubectl apply -f aps-all-in-one.yaml

   ```
5. **Use Kubectl to get pods and service and Access frontend and store admin with exposed URL**
```
kubectl get pods
kubectl get service
```
## Table of Microservice Repositories

| Service            | Repository Link                                      |
|--------------------|------------------------------------------------------|
| Store-Front        | https://github.com/Nidhi0152/frontend_bestbuy.git |
| Product-Service    | https://github.com/Nidhi0152/productservice_bestbuy.git |
| Order-Service      | https://github.com/Nidhi0152/orderservice_bestbuy.git |
| Store-Admin        | https://github.com/Nidhi0152/storeadmin_bestbuy.git |
| MakeLine-Service   | https://github.com/Nidhi0152/makelineservice_bestbuy.git |
| AI-Service         | https://github.com/Nidhi0152/aiservice_bestbuy.git |

## Table of Docker images

| Service            | DockerHub Link                                      |
|--------------------|------------------------------------------------------|
| Store-Front        | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-frontend |
| Product-Service    | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-productservice/tags |
| Order-Service      | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-orderservice/tags |
| Store-Admin        | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-storeadmin/tags  |
| MakeLine-Service   | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-makelineservice/tags |
| AI-Service         | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-aiservice/tags |
    
## Deployment file
 You can find file under Deployment folder:

## Demo Video
Link to Youtube : 

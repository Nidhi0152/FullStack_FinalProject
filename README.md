#  Best Buy Cloud-Native Application

##  Updated Application Architecture

The Best Buy application is built using a microservices-based, cloud-native architecture deployed on a Kubernetes cluster.

###  Architecture Diagram  
![diagram](https://github.com/user-attachments/assets/a092e006-4e93-4af5-ab5e-1547ffa2deec)


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
3. **Set AZure AKS Cluster**
    Connect with Azure CLI and use kubectrl
     ```
     az login
     az account set --subscription ee6d1840-d090-4e11-94bc-fb6c42daa912
     az aks get-credentials --resource-group cst8915 --name finalexam_nidhi --overwrite-existing
     ```
 4.**Check Kubectrl is working**
  ```
     kubectl get nodes
```
   
5. **Configure Kubernetes Manifests**  
   Apply Kubernetes YAML configuration files including deployments, configmaps, and secrets:
   ```example:
   kubectl apply -f aps-all-in-one.yaml

   ```
6. **Use Kubectl to get pods and service and Access frontend and store admin with exposed URL**
```
kubectl get pods
kubectl get service
```

7.**Access the applicaton**

   Use 'EXTERNAL-IP' of frontend-bestbuy and storeadmin-bestbuy to access services.
   
## Table of Microservice Repositories

| Service            | Repository Link                                      |
|--------------------|------------------------------------------------------|
| frontend-bestbuy       | https://github.com/Nidhi0152/frontend_bestbuy.git |
| productservice-bestbuy    | https://github.com/Nidhi0152/productservice_bestbuy.git |
| orderservice-bestbuy      | https://github.com/Nidhi0152/orderservice_bestbuy.git |
| storeadmin-bestbuy        | https://github.com/Nidhi0152/storeadmin_bestbuy.git |
| makelineservice-bestbuy   | https://github.com/Nidhi0152/makelineservice_bestbuy.git |
| aiservice-bestbuy         | https://github.com/Nidhi0152/aiservice_bestbuy.git |
| mongodb-bestbuy           | https://github.com/Nidhi0152/mongodb_bestbuy.git |

## Table of Docker images

| Service            | DockerHub Link                                      |
|--------------------|------------------------------------------------------|
| frontend-bestbuy        | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-frontend/tags |
| productservice-bestbuy    | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-productservice/tags |
| orderservice-bestbuy       | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-orderservice/tags |
| storeadmin-bestbuy        | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-storeadmin/tags  |
| makelineservice-bestbuy   | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-makelineservice/tags |
| aiservice-bestbuy         | https://hub.docker.com/repository/docker/nidhi0152/bestbuy-aiservice/tags |
    
## Deployment file
 You can find files under Deployment File folder:
 | Ymal Files            |
|--------------------|
| admin-tasks.yaml       |
| aps-all-in-one.yaml   | 
| config-maps.yaml      | 
| secrets.yaml     |

I have made one deployment file to deploy all services : aps-all-in-one.yml

## Issue Encounterd
1.  **Deplying AI Service**
   - While deploying open AI error encoured : Insuffiencient Quota
   - How ever when I used it previously for that same project I was able to deploy but at that time those services were not working and I thought to give a next try and deleted. Unfortunaly when I tried to create open ai again insufficient quota error  was coming.
   -  I asked for a help to friend and some how I was able to retrive my openai project made previously; and my gpt4 service was deployed and for dall-e-3 it was giving error as insufficient quota. To run these ai service I have taken below steps :

###  `secrets.yml`: Added Encrypted API Key

```yaml
data:
  OPENAI_API_KEY: "Qzd3dFdEazd4anJSTVdwdUJyNGkxeVc0a0dnbXhhdHJjTXpZMkYxVWZkUUt2cGdrbkhWV0pRUUo5OUJEQUNIWUh2NlhKM3czQUFBQUFDT0dJZmdr"
```
  
### aps-all-in-one.yml: Gave endpoints of AI services and entered the service names

  ```yaml
- name: AZURE_OPENAI_DEPLOYMENT_NAME # required if using Azure OpenAI
              value: "gpt-4"
            - name: AZURE_OPENAI_ENDPOINT # required if using Azure OpenAI
              value: "https://desa0-m9ktnwfl-eastus2.openai.azure.com/"
            - name: AZURE_OPENAI_DALLE_ENDPOINT
              value: "https://desa0-m9ktnwfl-eastus2.openai.azure.com/"
            - name: AZURE_OPENAI_DALLE_DEPLOYMENT_NAME
              value: "dall-e-3"
   ```
2. **Azure Service bus**
 - It was taking a bit long to reflect the chnages after checking out from cart and I have mentioned that in video as well. Moreover in video you can see some order spkies around 1:04am as I already tried it before recording video.

## Demo Video
Link to Youtube : https://www.youtube.com/watch?v=pe4-DR737W8

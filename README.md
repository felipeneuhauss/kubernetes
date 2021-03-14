## Node.js with MongoDB Example

<img src="https://i.imgur.com/V6k9QVB.png" alt="Swagger Page of that application" title="Swagger Page of that application"/>

### Requirements

- Node.js v10+
- MongoDB running on local instance

#### Environment Variables

- PORT: 3000
- MONGO_URL: localhost:27017

### Running

- Install dependencies - `npm i`
- Build typescript - `npm run build`
- Run project - `npm start`
- Go to swagger page - `localhost:3000/`

### Development with Watch Compiler

- Run once - `npm run dev`
- Run and watch files - `npm run dev:watch`

### Azure

```shell
az login
az account set --subscription "Subscription Name"
az group create --name k8s-course --location eastus
az group create --name k8s-course --location eastus
az acr create --resource-group k8s-course --name fnak8simages --sku Basic
```

fnak8simages.azurecr.io

```shell
az acr login --name k8s-course
az acr --resource-group k8s-course --output table
docker tag felipeneuhauss/api-heroes fnak8simages.azurecr.io/api-heroes
docker push fnak8simages.azurecr.io/api-heroes
```

### Azure Container Services
#### Mongo
MONGO_URL=52.149.255.15
```shell
az container create --resource-group k8s-course \
--name mongodb --image mongo:3.5 \
--port 27017 \
--ip-address public

az container logs --resource-group k8s-course --name mongodb 
az container show --resource-group k8s-course --name mongodb --query ipAddress.ip
```
#### App

```shell
az container create --resource-group k8s-course \
 --name api-heroes --image fnak8simages.azurecr.io/api-heroes \
 --port 3000 \
 --environment-variables MONGO_URL=52.149.255.15 \
 --registry-username fnak8simages \
 --registry-password $(az acr credentials show -n fnak8simages --query passwords[0].value) \
 --ip-address public 
 
az acr update -n fnak8simages --admin-enabled  


 
```
### Azure Kubernetes Service 

```shell
az aks create -g k8s-course \
  --name k8s-cluster \
  --dns-name-prefix fna-k8s-cluster
  --generate-ssh-keys \
  --node-count 2    
```

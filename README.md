# Infrastructure Engineer (DevOps) Challenge
![JOIN acceleration](https://github.com/join-com/devops-challenge/raw/master/illustration.png)

## Prerequisite
use minikube cluster or Docker for Mac. for this Challenge
install helm

## Explanation 

* Each Deployment has its own helm chart.
* used node Port for calc for exposing it to outside of cluster.
* Calc env file use the service name managed by helm to communicate with accelerator-a and accelerator-dv application.
* created unique service account for accelerator-dv and accelerator-a deployment management.
* created role bindings for associating service account with deployment in helm templates.
* Created cron jobs in accelerator-a and in dv to restart the deployment gracefully after every 4 minutes as in node service the timeout set for 5 min and making the service unstable.
* used two replica set for all the application.

## Setup
- `start the` minikube `cluster`
```bash
minikube start
```

- `export` minikube `environment variable to use local docker images`
```bash
eval $(minikube docker-env)
```

- `build` Docker `images`
```bash
cd acceleration-a && docker build -t acceleration-a -f Dockerfile .
```
```bash
cd acceleration-calc && docker build -t acceleration-calc -f Dockerfile .
```
```bash
cd acceleration-dv && docker build -t acceleration-dv -f Dockerfile .
```

- `Deploy` Helm `charts`
```bash
cd acceleration-a && helm install acceleration-a-helm acceleration-a-helm/
```
```bash
cd -
```
```bash
cd acceleration-dv && helm install acceleration-dv-helm acceleration-dv-helm/
```
```bash
cd -
```
```bash
cd acceleration-calc && helm install acceleration-calc-helm acceleration-calc-helm/
```
```bash
cd -
```

- `Check` service name and URL of calc `service`
```bash
minikube service list
```

## The context
This challenge addresses a web application with a microservice architecture to calculate the [acceleration](http://www.softschools.com/formulas/physics/acceleration_formula/1/) of an object.
## The application
- The application contains 3 microservices
- Each microservice takes care of only one arithmetic operation
- The microservices take inputs from the URL query form and return the result in JSON format
- The microservices are not stable and can stop serving requests
## Services:
- `acceleration-dv` calculates `𝚫v=vf-vi`
```bash
curl http://127.0.0.1:3001/dv?vf=200&vi=5
{"dv":195}
```
- `acceleration-a` calculates `a=𝚫v/t`
```bash
curl http://127.0.0.1:3002/a?dv=200&t=5
{"a":40}
```
- `acceleration-calc` coordinates request to `acceleration-dv` and `acceleration-a` services
```bash
curl http://127.0.0.1:3000/calc?vf=200&vi=5&t=123
{"a":1.5853658536585367}
```

# Task
- Using [Helm](https://helm.sh), write the necessary Kubernetes deployment and service files that can be used to create the full application, running 2 instances of each microservice.
- Only  `/calc` of `acceleration-calc` microservices can be available outside of the kubernetes cluster.
- Run the application on a kubernetes cluster like Minikube or Docker for Mac.
- Make sure the application is stable.
- Please do not change a code in services.

# Environment Setup
- Microservices are written on Typescript and Node.js version 10.14.2
- You would need to setup `yarn`
- Run `yarn install` to setup all required components
- Run `yarn build` to build production ready code
- Run `yarn dev` to run a service in dev environment
- Run `yarn start` to run a service in production

# Instructions
- The challenge is on!
- **Send us an email with a link to repository when you finish the assesment.**
- Please complete your working solution within 7 days of receiving this challenge.


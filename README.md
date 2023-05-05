# Hotel Search Application
## Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Usage](#usage)

## About <a name = "about"></a>

A simple docker application on top of a simple hotel search application, uses two microservices to perform basic search. 
Uses Kubernetes on top of these microservices to create a cluster. This also allows port forwarding and adds test program to search kubernetes service.

## Getting Started <a name = "getting_started"></a>

### Prerequisites

To run this project, you need to have:
1. docker or docker-desktop
2. kubernetes
3. kubectl
4. Node (Optional, only if you want to run test program)

### Installing

1. Clone this repository: `git clone https://github.com/ps662/sit323_737-2023-t1-prac7c.git`
2. Navigate to the project directory: `cd sit323_737-2023-t1-prac7c`

## Usage <a name = "usage"></a>

To start the server, run the following command:

```
kubectl apply -f k8s/nlp_service.yaml
kubectl apply -f k8s/nlp_deployment.yaml
kubectl apply -f k8s/search_deployment.yaml
kubectl apply -f k8s/search_service.yaml
```

This will start the server and listen on port 3000. You can access the application in your web browser by visiting [http://localhost:3000](http://localhost:3000).

To enable port forwarding:

```
kubectl port-forward service/search-service 3000:3000
kubectl port-forward service/nlp-service 3001:3001
```

After this, you can also test the application by (you need node installed for this):

```
node .\simple_test_query.js
```

If you also want to monitor using the dashboard then use:

```
# Change version according to your kubectl
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
kubectl apply -f k8s/admin_dashboard.yaml
kubectl proxy
```

To generate an access token use:

```
kubectl -n kubernetes-dashboard create token admin-user
```

Navigate to http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/ and use the generated token to access the dashboard.






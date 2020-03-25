# little-help-book
because we just need a little help

## Run the App From Docker

### Install the image and container

- Install Docker
- Build the image with `docker build -t little-help-book:0.1 .`

### Run the app
- Run the image with `docker run -p 5000:800 little-help-book::0.1`
- Open a browser and go to `localhost:5000`

### Close down the app
 Stop the app using ctl+c.

## Run the App From Kubernetes

### Install Kubernetes
- Look online to find how to install at least a single node k8s cluster.
- There are many ways to run k8s, including KinD, microk8s, and others.

### Install the namespace, apply the deployment and service
- Run the command `kubectl create -f kube/namespace.yml`
- Run `kubectl apply -f kube/deploy.yml`
- Run `kubectl apply -f kube/service.yml`

### Run the app
- Wait for the pod to be deployed. You can see if the pod is running with `kubectl get pods -n little-help-book`
- See which IP address the app is running on with `kubectl get service -n little-help-book`. Take note of the `CLUSTER_IP`.
- Open a browser and point to the `CLUSTER_IP` address. It will automatically be using port 80, so no port need be specified.
- Go to the URL path /weatherforecast to see information from the API, e.g. `http://10.0.0.1/weatherforecast`

### Shut down app
- `kubectl delete namespace little-help-book`
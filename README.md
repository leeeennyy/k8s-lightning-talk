# k8s-lightning-talk

## Prerequisites
Install the following:
- [Docker](https://www.docker.com/products/docker-desktop)
- [minikube](https://minikube.sigs.k8s.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) (minikube should install this I think, but if not, install it)

## Docker
### Building the image
Navigate to the API solution and run:
```
docker build -t alenaintergen/k8s-lightning-talk-demo:v1 -f k8s-lightning-talk-demo\Dockerfile .
```
### Pushing the image
```
docker push alenaintergen/k8s-lightning-talk-demo:v1
```
You'll need to replace `alenaintergen` with the name of your docker registry if you want to make your own. You can create an account at https://hub.docker.com/.

## Kubernetes
To deploy locally, ensure that minikube is started and that kubectl is connected to it.
```
minikube start
kubectl config use-context minikube
```

### Deploying k8s resources
Navigate to the top level of this repo
```
kubectl apply -f service.yaml
kubectl apply -f deployment.yaml
```

Check resources are up
```
kubectl get po
kubectl get deployment
kubectl get svc
```

Once resources are up, we can connect to our API. The command below will open up a tab in your browser, and we can navigate to `<url>/weatherforecast`. We should see our API.
```
minikube service k8s-lightning-talk-demo-svc
```

### Cool commands you can do
```
kubectl scale deployment k8s-lightning-talk-demo --replicas=5
kubectl logs po <podname>
```

### Clean up
```
kubectl delete -f service.yaml
kubectl delete -f deployment.yaml
minikube stop
```

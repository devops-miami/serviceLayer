# Helm Chart -> Atlantis
The stuff dreams are made of.. 
A quick and easy way to deploy `Atlantis` on a `Kubernetes Cluster`. 

[Atlantis Official Helm Chart](https://www.runatlantis.io/docs/deployment.html#deployment-2)

### Deploy locally with Minikube
Testing out our changes locally using `minikube`.

*This assumes you already installed minikube*

```sh
# Start minikube
minikube start --cpus 2 --memory 4096 --driver=docker 
# Add the Official Helm Repo
helm repo add runatlantis https://runatlantis.github.io/helm-charts
```

You now have the repo for the chart install but before you continue you need to download and modify the values file in the chart to allow access to your github repos. Follow the instructions from `Atlantis` to sort that stuff out.
* [Generating an Access Token](https://www.runatlantis.io/docs/access-credentials.html#generating-an-access-token)
* [Generating a Web Hook Secret](https://www.runatlantis.io/docs/webhook-secrets.html#generating-a-webhook-secret)


```sh
helm inspect values runatlantis/atlantis > values.yaml
# Run the install command
helm install atlantis runatlantis/atlantis -f values.yaml
kubectl port-forward svc/atlantis 8080:80  
```
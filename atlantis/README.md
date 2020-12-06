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
# Adjust the github credentials and also adjust the image
# We want to point to our local registry
# Run the install command
helm install atlantis runatlantis/atlantis -f values.yaml
# Check the pod is online
kubectl get pods
# Forward the port to the localhost 8080
kubectl port-forward svc/atlantis 8080:80
```

Ok, if all that works we are ready to up the game a knotch.
Now let's use the custom image we built in the ISO layer with this default `Helm Chart` by modifying the `values` file.

*If you are using minikube you will need to have this image available in the minikube registry not the local docker one!*

[isoLayer configure minikube]()

## Run the Custom ISO
We created a custom image in the `isoLayer` with support for `SOPS` and `Terragrunt`. Let's use that image instead of the default one they provide.

```yaml
# Modify the image setting to reflect the minikube registry or your cloud providers
image:
  repository: atlantis
  tag: v1
  pullPolicy: IfNotPresent
```

We are telling `helm` we want to use the image from the minikube registry. If you are deploying to the cloud this would be a gcr or ecr registry.

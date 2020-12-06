# Demo Repos
This is a demo for how my stack works. Three different repos represent three different layers required to go to production at scale. The stack splits resources into the Infrastructure layer, dependencies into the ISO Layers, and scaling / deployment / ingress / certs into the Service layer (everything that happens on K8 level).

[Senpai Stack](https://devops.miami/my-stack/)

## Service Layer
This layer is responsible for the `Helm Charts` and the `values` file we use to install them on `Kubernetes Clusters`.
In this case we are adding instructions to spin up the `Atlantis` image we built in the `isoLayer` repo.

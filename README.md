## Running the Node app

Install the app using:

`npm install`

Run the app using:

`npm run start`

Connect by going to: 

[http://localhost:3000/](http://localhost:3000/)


## Creating a Docker image to deploy

#### Build the image

`docker build -t clintomed/hello-kubernetes:0.1.0 .`

#### Run an image

`docker run -p 3000:3000 -d hello-kubernetes`

#### Push the image

`docker push clintomed/hello-kubernetes:0.1.0`


## Deploying to Kubernetes using vanilla Kubernetes

For these instructions I used [kind](https://kind.sigs.k8s.io/). Make sure you have pushed the Docker image.

1. `kind create cluster`
1. Go into `kubernetes-yaml/deployments/hello-kubernetes.deployment.yaml` and change the spec.template.spec to use the image you pushed to Docker Hub.
1. Run `k apply -f kubernetes-yaml/deployments/hello-kubernetes.deployment.yaml`
1. Run `k apply -f kubernetes-yaml/services/service-definition.yaml`
1. Run `kubectl port-forward service/myapp-service 3003:3000` to expose port 3000 on your node to port 3003 on your host.
1. Go to [http://localhost:3003/](http://localhost:3003/)

## Deploying to Kubernetes using Helm

#### Setting up helm release

1. Create a new folder called helm
1. Initialize helm using `helm create node-kubernetes`
1. In the `deployment.yaml` file in the `templates` folder, change the `containerPort` to `3000`.
1. In the `Chart.yaml` change the the `appVersion` to the version of the docker container you want to deploy, for example `0.1.0`.
1. In the `values.yaml` file, change the `image.repository` to `clintomed/hello-kubernetes`. Change `service.type` to `NodePort` and `service.port` to `3000`. Change `ingress.enabled` to `true`.

[How to make a Helm chart in 10 minutes](https://opensource.com/article/20/5/helm-charts)

#### Deploying the new helm release



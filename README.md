## Docker commands used

```
//Create container image build
docker build.
OR
docker build -t roshin/name .

//Any time a request coming from port http://localhost:8080 need to
//redirect to 8080 on the docker container
docker run -p 8080:8080 <container-id>

//To run commands inside containers
docker run -it <cid> sh
OR
docker exec -it <cid> sh

//To show all container files
docker ps

//To log the container
docker log <cid>

## Docker Cloud
create an account on Docker Hub at https://hub.docker.com/. This is where you'll store your container images.
Tag Your Local Image:
Before you can push an image to Docker Hub, you need to tag it with the repository information. The format for the tag is typically <username>/<repository>:<tag>. For example:
docker tag <local-image>:<tag> <username>/<repository>:<tag>
## Create an Account on Docker Hub (Docker Cloud):
## Login to Docker Hub:
Use the following command to log in to Docker Hub using your Docker Hub account credentials:
docker login
docker logout

## Push the Image to Docker Hub:
docker push <username>/<repository>:<tag>
##Access the Image on Docker Hub:
docker pull <username>/<repository>:<tag>

```

## Kubernetes commands used

```
//Go to docker desktop setting preference and enable Kubernetes
kubectl version

//Create a post pod(container)
//Take build using docker build -t roshin/name:0.0.01 .
//paste roshin/name:0.0.01 name on yaml file like image:roshin/name:0.0.01 , then run:
kubectl apply -f post.yaml

//see all pods running
//get pod name
kubectl get pods

If your pods are showing ErrImagePull, ErrImageNeverPull, or ImagePullBackOff errors after running kubectl apply, the simplest solution is to provide an imagePullPolicy to the pod.
First, run:
kubectl delete -f infra/k8s/

Then, update your pod manifest:

spec:
containers: - name: posts
image: cygnet/posts:0.0.1
imagePullPolicy: Never
Then, run
kubectl apply -f infra/k8s/

This will ensure that Kubernetes will use the image built locally from your image cache instead of attempting to pull from a registry.

//log
kubectl logs <podname>

//run shell
kubectl exec -it <podname> sh

//delete pod
kubectl delete pod <podname>

//pull out some info on running pod
kubectl describe pod <podname>


//create a deployment to handle pods
//Delete .yaml file inside /k8s
//create name-depl.yaml
kubectl apply -f posts-depl.yaml

//get deployments
kubectl get deployments
//If we try to delete a pod deployment will automatically create for us.
kubectl delete pod <podname>

//pull out some info on running deployment
kubectl describe deployment <podname>

//Delete deployment
kubectl delete deployment posts-depl

//It is very difficult to manage the version for each code change.
//So don't specify a version. K8s automatically fetches the latest version of the docker build.
//push it to docker hub
//makesure that username is correct(roshin)
kubectl push roshin/posts

//Now need to tell deployment to use latest version
kubectl rollout restart deployment posts-depl(deployment name: posts-depl .You can find those when run: kubectl get deployment)

//To find latest change log
kubectl get pods
//Copy the pod name,run:
kubectl logs <podname>

## Concluding steps if any file changes made
docker build -t roshin/name .
docker push roshin/name

kubectl apply -f .\name-depl.yaml
kubectl get deployment
kubectl rollout restart deployment <deployment-name>
kubectl get pods
kubectl logs <pod-name>

```

### Kubernetes services nodeport and clusterip

```
kubectl apply -f .\name-srv.yaml
//Get service name and nodeport port
kubectl get services
kubectl describe service <service-name>

//Create a nodeport service to access node port from externsl like localhost:30744/posts
//Create clusterip for connecting different pods
//Make sure that generated cluster ip name need to replace with localhost like htttp://post-clusterip-srv:30714/posts in nodejs file
//First check nodeport is working fine from post-man http://localhost:30744/posts
If we return data then check log from services run:
kubectl get pods
kubectl logs <pod-name>

//To apply all the config yaml file with one single command inside a k8s folder
kubectl apply -f .

```

## loadbalancer & ingress

```
//GO to these site
https://kubernetes.github.io/ingress-nginx/deploy/#quick-start
//Run these cmd:
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.1/deploy/static/provider/cloud/deploy.yaml

kubectl apply -f ingress-srv.yaml


```

## Skaffold

```
// Go to https://skaffold.dev/docs/install/
choco install -y skaffold
//Watch all yamal file inside k8s folder
//Create depoly object when skaffold up and delete all the config object associated kubernetes  whenever we stop sakffold
//Automaticalyy detect any file changes and create build and deploy
//create skaffolf.yaml file from root directory and run:
skaffold dev

```

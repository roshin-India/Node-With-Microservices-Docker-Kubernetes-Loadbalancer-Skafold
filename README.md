## Docker commands used

```
//Create container image build
docker build .
OR
docker build -t roshin/name .

//Any time a request coming from port http://localhost:8080 need to
//redirect to 8080 on docker container
docker run -p 8080:8080 <container-id>

//To run command inside containers
docker run -it <cid> sh
OR
docker exec -it <cid> sh

//To show all container files
docker ps

//To log container
docker log <cid>

## Docker Cloud
```

create an account on Docker Hub at https://hub.docker.com/. This is where you'll store your container images.
Tag Your Local Image:
Before you can push an image to Docker Hub, you need to tag it with the repository information. The format for the tag is typically <username>/<repository>:<tag>. For example:
docker tag <local-image>:<tag> <username>/<repository>:<tag>

```
## Create an Account on Docker Hub (Docker Cloud):

```

## Log In to Docker Hub:

Use the following command to log in to Docker Hub using your Docker Hub account credentials:
docker login

```

```

## Push the Image to Docker Hub:

docker push <username>/<repository>:<tag>
##Access the Image on Docker Hub:
docker pull <username>/<repository>:<tag>

```


```

## Kubernates commands used

```
//Go to docker desktop setting preference and enable kubernetes
kubectl version

//Create a post pod(container)
//Take build using docker build -t roshin/name:0.0.01 .
//paste roshin/name:0.0.01 name on yaml file like image:roshin/name:0.0.01 , then run:
kubectl apply -f post.yaml

//see all pods running
//get pod name
kubectl get pods
```

If your pods are showing ErrImagePull, ErrImageNeverPull, or ImagePullBackOff errors after running kubectl apply, the simplest solution is to provide an imagePullPolicy to the pod.

First, run
kubectl delete -f infra/k8s/

Then, update your pod manifest:

spec:
containers: - name: posts
image: cygnet/posts:0.0.1
imagePullPolicy: Never
Then, run
kubectl apply -f infra/k8s/

This will ensure that Kubernetes will use the image built locally from your image cache instead of attempting to pull from a registry.

```
//log
kubectl logs <podname>

//run shell
kubectl exec -it <podname> sh

//delete pod
kubectl delete pod <podname>

//pull out some info of running pod
kubectl describe pod <podname>


//create deployment to handle pods
//Delete .yaml file inside /k8s
//create name-depl.yaml
kubectl apply -f posts-depl.yaml

//get deployments
kubectl get deployments
//If we try to delete a pod deployment will automatically create for us.
kubectl delete pod <podname>

//pull out some info of running deployment
kubectl describe deployment <podname>

//Delete deployment
kubectl delete deployment posts-depl

//It is very difficult to manage cersion for each codr changes.
//So dont specify version. K8s automatically fetch latest versio of docker build.
//push it to docker hub
//makesure that username is correct(roshin)
kubectl push roshin/posts

//Now need to tell deployment to use latest version
kubectl rollout restart deployment posts-depl(deployment name: posts-depl .You can find those whrn run: kubectl get deployment)

//To found latest change log
kubectl get pods
//Copy the podname,run:
kubectl logs <podname>

## concluding Steps if any changes made
```

docker build -t roshin/name .
docker push roshin/name

kubectl apply -f .\name-depl.yaml  
kubectl get deployment
kubectl rollout restart deployment <deployment-name>
kubectl get pods
kubectl logs <pod-name>

```

```

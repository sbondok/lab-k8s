# lab-k8s
This Lab-Project includes some yaml configuration files (Deployments, Services, Volumes etc...) for training purposes only, so feel free to clone it, under your own responsibility.

## Some commands help you to work with pods and deployment.
### What is the difference between:
- kubectl create and kubectl apply?

* create: creates (pod, services, namespace etc..) from scratch a new file (does not exist before)
* apply: creates from scratch and modifies existing object.

### To run commands inside pods:
- kubectl exec -it <pod name> -- /bin/bash

### To get more information about pods: (ip - namespace - node etc..)
- kubectl get pod -o wide

### To get more details about pods:
- kubectl describe pod <pod name> 


# Deployment:

## To create a yaml deployment template file from command prompt:
- kubectl create deployment my-deb --image=busybox --port=5701 --replicas=3 -o yaml --dry-run=client > my-deb.yaml
** "busybox may not work!!!- consider using nginx instead"

## To show all deployments:
- kubectl get deployments.app (k get deployment)

## To delete specific deployment use the command:
- kubectl delete deployment <deployment>

## To watch the running command live use:
- watch n 1 "kubectl get pods"

## To force kubernetes to keep at least 2 replicas when changes made inside deployment file under spec section: 
strategy:
  type: RollingUpdate
		rollingUpdate:
		  maxUnavailable:1
		  maxSurge:1
This will change 2 replicas at a time.

## What if we want to replace all of the replicas at once?

strategy:
  type: Recreate


## By default the current namespace is <<default>>, but if we need to change it to another namespace we first create that namespace and set it as current one!

- kubectl create namespace <namespace name>
- kubectl config set-context --current --namespace=<namespace name>

Now if we create any pod or deployment it will be placed into bond namespace.

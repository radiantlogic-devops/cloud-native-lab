## minikube start
Minikube is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes.

All you need is Docker (or similarly compatible) container or a Virtual Machine environment, and Kubernetes is a single command away: ```minikube start```

### What you’ll need for this lab
* 4 CPUs or more
* 16GB of free memory
* 50GB of free disk space
* Internet connection

** If using Docker Desktop, increase the memory allocation to 16GB
** If you already started minikube, stop it, delete it and configure with the following settings

### Settings
* Increase the default cpu/memory allocation (requires restart)
```
minikube config set memory 8192
minikube config set cpus 4
```
* On Windows (if needed)
```
minikube config set driver hyperv
```
* Validate the settings
```
minikube config view
```
### Start
* Start minikube
```
minikube start
```
* Run the command below to launch the kubernetes dashboard
```
minikube dashboard
```
### Stop
* When the lab is finished, you can stop minikube

```
minikube stop
```
### Delete Minikube

* To delete the minikube cluster

```
minikube delete
```

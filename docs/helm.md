## **Before you start**

* Make sure [Helm](https://helm.sh/docs/intro/install/) is installed and available.
* Make sure you have a running kubernetes cluster (minikube, EKS, AKS, GKE, k3s, k8s)
* Make sure kubectl is configured to access the right cluster. You can verify that by running the following commands
```console
kubectl cluster-info
```
```console
kubectl get nodes
```

## **Add Helm Repository**

* Run the below command to list the existing repo (if any)

```console
helm repo list
```
* From the, output of command above if you see "radiantone", run the below command else jump to "Deploying FID/Zookeeper" section.

```console
helm repo update
```
### **Deploying FID/Zookeeper**

#### **Add radiantone repository**

* Run the below command to add the radiantone repo

```console
helm repo add radiantone https://radiantlogic-devops.github.io/helm
```

Verify

* To verify if the radiantone repo is added, run the command below

```console
helm repo list
```
In the output you should see "radiantone" added along with other repositories if you have any.

####**Creating Namespace**

* Run the below command to create a new namespace to deploy FID/Zookeeper

```console
kubectl create namespace helm-lab
```

Verify:

* To verify if the namespace has been created, run the command below

```console
kubectl get namespace
```

* You should see "helm-lab" in the list of outputs

#### **Deploying Zookeeper**

**Install zookeeper with default values**

```console
helm install --namespace=<name space> <release name> radiantone/zookeeper
```

Example:

```console
helm install --namespace=helm-lab zk radiantone/zookeeper
```
* The above command deploys zookeeper (default with replicaCount=3)
* You will see following response printed to the console
```console

```

Verify

* To verify if zookeeper has been deoployed successfully, run the command below

```console
kubectl get pods -n helm-lab
```
* You will see three zookeeper pods "zk-zookeeper-0/1/2" (the release name is joined to default zookeeper name, so the pods are named zk-zookeeper-x)


**List Zookeeper releases**

* To list the zookeeper releases, run the command below

```console
helm list --namespace=<name space>
```

Example:

```console
helm list --namespace=helm-lab
```

**Upgrade a Zookeeper Release (optional)**

* To upgrade an existing or deployed zookeeper releasem, run the below command

```console
helm upgrade --namespace=<name space> <release name> radiantone/zookeeper
```

Example:

```console
helm upgrade --namespace=helm-lab zk radiantone/zookeeper
```

#### **Deploying FID**

**Install FID with default values**

```console
helm install --namespace=<name space> <release name> radiantone/fid
```

Example:

```console
helm install --namespace=helm-lab fid radiantone/zookeeper
```
* The above command deploys fid (default with replicaCount=3)
* You will see following response printed to the console
```console

```

**Install FID with overridden values**

```console
helm install --namespace=<name space> <release name> radiantone/fid \
--set zk.connectionString="zk.dev:2181" \
--set zk.ruok="http://zk.dev:8080/commands/ruok" \
--set fid.license="<FID cluster license>" \
--set fid.rootPassword="<password>"
```

Example(replace the "FID cluster license" with your license):

```console
helm install --namespace=helm-lab fid radiantone/fid \
--set zk.connectionString="zk-zookeeper.helm-lab:2181" \
--set zk.ruok="http://zk-zookeeper.helm-lab:8080/commands/ruok" \
--set fid.license="<FID cluster license>" \
--set fid.rootPassword="test1234"
```

**IMPORTANT NOTE** : Curly brackets in the liense must be escaped --set fid.license="\\{rlib\\}xxx"


Verify

* To verify if fid has been deoployed successfully, run the command below

```console
kubectl get pods -n helm-lab
```
* You will see  fid pod "fid-o"


**List FID releases**

* To list the fid releases, run the command below

```console
helm list --namespace=<name space>
```

Example:

```console
helm list --namespace=helm-lab
```

**Upgrade a FID Release (optional)**

* To upgrade an existing or deployed zookeeper releasem, run the below command

```console
helm upgrade --namespace=<name space> <release name> radiantone/fid --set image.tag= 7.4.x/7.3.x
```
**NOTE:** Check for the latest image releases [here](https://hub.docker.com/r/radiantone/fid/tags)

Example:

```console
helm upgrade --namespace=helm-lab fid radiantone/fid --set image.tag = 7.4.0
```

## **Cleanup**


* To remove the Zookeerp/ FID helm deployments run the commands below

**Removing FID deployment**

```console
helm delete --namespace=<name space> <release name>
```

Example

```console
helm delete --namespace=helm-lab fid

Verify

* To verify if the fid depoloyment has been deleted/removed run the command below

```console
kubectl get all -n helm-lab
```

You not see any fid pods, move to the next step

**Removing Zookeeper Deployment**

* To remove Zookeeper deployment run the command below

```console
helm delete --namespace=<name space> <release name>
```

Example

```console
helm delete --namespace=helm-lab zk
```

Verify

* To verify if the fid depoloyment has been deleted/removed run the command below

```console
kubectl get all -n helm-lab
```

You will not see any zk-zookeeper pods.

**Delete Namespace**

* To delete the namespace that was created, run the command below

```console
kubectl delete namespace helm-lab
```

Verify

* To verify if namespace has been deleted, run the command below

```console
kubectl get namespace
```

You will not find the "helm-lab" in the list of namespaces.





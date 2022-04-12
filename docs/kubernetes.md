## Before you start
* FID or Zookeeper running locally on your machine are stopped.
* Make sure that kubectl is configured to access the right cluster

        kubectl cluster-info
        kubectl get nodes

* Clone the kubernetes manifest samples repo
```
git clone https://github.com/radiantlogic-devops/kubernetes.git
```
## Standalone FID
#### namespace
```
kubcetl create ns lab-00
```
#### edit manifest
Update the manifesl file `kubernetes/00-cluster-local-zk/fid.yaml` and paste the license key. Look for `PASTE_LICENSE_HERE` and replace it.

#### run
```
kubectl apply -f kubernetes/00-cluster-local-zk/fid.yaml -n lab-00
```
#### status
```
kubectl get all -n lab-00
```
When the pod shows 1/1 ready status, run the following command to forward the port

```
kubectl port-forward svc/fid 7070:7070 -n lab-00
```
Access the control panel at http://localhost:7070

The default username/password is

    cn=Directory Manager
    secret1234

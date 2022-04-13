## Docker
## Kubernetes

### If pods are not getting deployed

```console
kubectl get events -n <name space>
```

### Check if zookeeper is up and running

```console
kubectl exec -it zookeeper-0 -- bash -c "export JAVA_HOME=/opt/radiantone/rli-zookeeper-external/jdk/jre/;/opt/radiantone/rli-zookeeper-external/zookeeper/bin/zkServer.sh status"
```

### Exec into an fid/zk container

```console
kubectl exec -it zookeeper-0 -- /bin/bash
```
```console
kubectl exec -it fid-0 -- /bin/bash
```

### Run cluster.sh command

```console
kubectl exec -it fid-0 -- cluster.sh list
```

### Get kubernetes context

```console
kubectl config get-contexts
```

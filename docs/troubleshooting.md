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

##DOCKER TROUBLESHOOTING

### Logs

```
docker logs [options] <container name>
```
Options Available

* --details includes additional attributes to the log output, such as environment variables.
* --follow or -f shows new log output as the container runs.
* --since shows the log entries after the desired timestamp.
* --tail or -n shows some number (n) of lines from the end (tail) of the log.
* --timestamp or -t shows the log output for the desired point in time.
* --until shows all log entries until the desired timestamp.

### Docker Process Status
The docker process status command shows running containers 
```
docker ps
```
To view all the running containers
```
docker ps -a
```

### Docker Remove
When you want to completely remove a container, you use the docker rm command
```
docker rm <container_name>
```

### Docker Inspect
* The Docker inspect command returns an assortment of detailed Docker container information. 
* The information can include the container state, network port mappings, environment variable values and path to history log files

```
docker inspect [options] <container 1 name or ID> <container 2 name or ID…>
```

### Docker Info

* Docker info command output may provide details that include the number of running, paused and stopped containers; number of available images; what storage driver is in use; storage use and availability metrics; specifics for plugins, OS and the kernel; CPU and memory details; the current Docker server version; and execution and logging drivers in use.
```
docker info [options]
```

### Docker Stats

* The stats command automatically streams usage data for all running containers. Admins can declutter this information by using options and specifying desired container names
```
docker stats [options] <container 1 name> <container 2 name…>
```

### Docker Events

* The Docker events command enables admins to see up to 1,000 server-based events in real time
```
docker events [options]
```

### Docker exec

* The Docker exec command enables admins to execute new commands within the default directory of a running container. For exec to function, the command must be executable, and admins must run the target container
```
docker exec [options] <container command> <command arguments>
```


## DOCKER-COMPOSE TROUBELSHOOTING

To get the proper usage of docker-compose command run the command below

```
docker-compose -h
```

### Docker-Compose Process Status

To check the state of all the containers

```
docker-compose ps
```
**NOTE** : Run the docker-compose from the location of docker-compose.yaml file


### Docker-Compose Logs

To inpsect the logs and find any errors

```
docker-compose logs --follow
```

### Docker-Compose Events

Receive real time events from containers

```
docker-compose events
```


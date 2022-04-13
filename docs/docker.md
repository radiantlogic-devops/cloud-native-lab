
## **Before you start**
* FID or Zookeeper running locally on your machine are stopped.
* Copy these commands in a notepad and replace the license key.

## **Standalone FID**
This command runs FID in a docker container as a standalone node (local zookeeper).
#### run
```
docker run --rm --hostname=myfid --name=myfid -e LICENSE="<FID Cluster License>" \
-p 7070:7070 -p 2389:2389 radiantone/fid:7.4.0
```
For Mac M1 use this image ```radiantone/fid:7.4.0-arm64```
#### logs
```
docker logs -f myfid
```
#### status
```
docker ps
```
When the container shows healthy status, access the control panel at http://localhost:7070

The default username/password is

    cn=Directory Manager
    secret1234

## **Cleanup**
```
docker stop container myfid
docker rm container myfid
```
## **FID Cluster + External Zookeeper**

#### create a network
```
docker network create --driver bridge zk-net
```
### External Zookeeper
#### start zookeeper containers
```
docker run --hostname=zk-0 --name=zk-0 --network=zk-net --rm \
-e ZOOKEEPER_FLEET_SIZE=3 radiantone/zookeeper:3.5.8
```
```
docker run --hostname=zk-1 --name=zk-1 --network=zk-net --rm \
-e ZOOKEEPER_FLEET_SIZE=3 radiantone/zookeeper:3.5.8
```
```
docker run --hostname=zk-2 --name=zk-2 --network=zk-net --rm \
-e ZOOKEEPER_FLEET_SIZE=3 radiantone/zookeeper:3.5.8
```
For Mac M1 use this image ```radiantone/zookeeper:3.5.8-arm64```
#### status
```
docker ps
```
#### logs
```
docker logs -f zk-0
```
```
docker logs -f zk-1
```
```
docker logs -f zk-2
```
### FID cluster
#### node 1
```
docker run -d --hostname=fid-0 --name fid-0 --network=zk-net --rm \
-e CLUSTER=new -e ZK=external -e ZK_CONN_STR="zk-0:2181,zk-1:2181,zk-2:2181" \
-e ZK_CLUSTER=docker-cluster -e ZK_PASSWORD=secret1234 \
-e LICENSE="<FID Cluster License>" \
-p 17070:7070 12389:2389 radiantone/fid:7.4.0
```
#### node 2
Start the second node only after the first node is completely up and running
```
docker run -d --hostname=fid-1 --name fid-1 --network=zk-net --rm \
-e CLUSTER=new -e ZK=external -e ZK_CONN_STR="zk-0:2181,zk-1:2181,zk-2:2181" \
-e ZK_CLUSTER=docker-cluster -e ZK_PASSWORD=secret1234 \
-e LICENSE="<FID Cluster License>" \
-p 27070:7070 22389:2389 radiantone/fid:7.4.0
```
#### node 3
Check the memory and CPU usage before running the third node
```
docker run -d --hostname=fid-2 --name fid-2 --network=zk-net --rm \
-e CLUSTER=new -e ZK=external -e ZK_CONN_STR="zk-0:2181,zk-1:2181,zk-2:2181" \
-e ZK_CLUSTER=docker-cluster -e ZK_PASSWORD=secret1234 \
-e LICENSE="<FID Cluster License>" \
-p 37070:7070 32389:2389 radiantone/fid:7.4.0
```

For Mac M1 use this image ```radiantone/fid:7.4.0-arm64```

When the container shows healthy status, access the control panel at http://localhost:7070

The default username/password is

    cn=Directory Manager
    secret1234

## **Cleanup**
```
docker stop container fid-0 fid-1 fid-2
docker stop container zk-0 zk-1 zk-2
```
```
docker container prune
```

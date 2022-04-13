
## **Before you start**
* FID or Zookeeper running locally on your machine are stopped.
* All containers from previous section are stopped and removed

```
docker ps -a
docker container prune
```

Clone the docker-compose samples repo
```
git clone https://github.com/radiantlogic-devops/docker-compose.git
```

## **Standalone FID**
* Change to 00-standalone folder
* Edit .env file and set the values 

```
# Example .env file
FID_VERSION=7.4.0
CLUSTER_NAME=docker-cluster-2
LICENSE=PASTE_YOUR_LICENSE_HERE
```
```
cd 00-standalone
```

#### run
This will run the containers in background
```
docker-compose up -d
```
#### status
From the same folder run this command. This will show the status.
```
docker-compose ps
```
When the container shows healthy status, access the control panel at http://localhost:7070

The default username/password is

    cn=Directory Manager
    secret1234

```
docker-compose down -v
```
## **Cluster FID + External Zookeeper**
### External Zookeeper ensemble
* Change to 03-external-zk folder

```
cd 03-external-zk
```
#### run
This will run the containers in background
```
docker-compose up -d
```
#### status
From the same folder run this command. This will show the status.
```
docker-compose ps
```
When the container shows healthy status, proceed to next step

### **FID Cluster**

* Change to 02-cluster-ext-zk folder

```
cd 02-cluster-ext-zk
```
* Edit .env file and set the values 

```
# Example .env file
FID_VERSION=7.4.0
CLUSTER_NAME=docker-cluster-3
LICENSE=PASTE_YOUR_LICENSE_HERE
```
#### run
This will run the containers in background
```
docker-compose up -d
```
#### status
From the same folder run this command. This will show the status.
```
docker-compose ps
```
When the container shows healthy status, access the control panel at http://localhost:7070

The default username/password is

    cn=Directory Manager
    secret1234

## **Cleanup**

```
cd 02-cluster-ext-zk
docker-compose down -v
```

```
cd 03-external-zk
docker-compose down -v
```

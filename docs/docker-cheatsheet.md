## Docker
Stop and remove all containers

    docker stop $(docker ps -aq); docker rm $(docker ps -aq)

Docker stats	:	

	$ docker stop $(docker ps -aq); docker rm $(docker ps -aq)
	$ docker run -itd -p 8030:80 --name nginx7 -v c:/html:/usr/share/nginx/html:ro nginx:v2
	$ docker stats
		CONTAINER ID        NAME         CPU %      MEM USAGE / LIMIT       MEM %               NET I/O             BLOCK I/O           PIDS
		779eb8148aa7        nginx7       0.00%      1.914MiB / 8.75GiB      0.02%               906B / 0B           0B / 4.1kB          2



Create and start a container

	$ docker create -t -i fedora bash
		6d8af538ec541dd581ebc2a24153a28329acb5268abe5ef868c1f1a261221752

	$ docker start -a -i 6d8af538ec5
		bash-4.2#

		
Copy	:

	Copy a file from host to container:
		 docker cp Dockerfile 779eb8148aa7:/tmp/Dockerfile
		 docker exec -it 779eb8148aa7 //bin/bash
		 docker cp Dockerfile 779eb8148aa7:/tmp/Dockerfile123
		 docker exec -it 779eb8148aa7 //bin/bash
	 
	Copy a file from Docker container to host:
		docker cp 779eb8148aa7:/tmp/Dockerfile123 Dockerfile_Delete
 
 
	Copy a Folder from host to container:
		docker cp /home/captain/my_dir ubu_container:/home
		docker cp ubu_container:/home/my_dir  /home/captain
 
 
Logs	:

	$ docker logs 779eb8148aa7 --follow
	

## Docker-Compose

Usage:

```
docker-compose <command>
```

Docker Compose Up:

Builds, (re)creates, starts, and attaches to containers for a service

```
Usage: docker-compose up [options] [--scale SERVICE=NUM...] [SERVICE...]

Options:
    -d, --detach               Detached mode: Run containers in the background,
                               print new container names. Incompatible with
                               --abort-on-container-exit.
    --no-color                 Produce monochrome output.
    --quiet-pull               Pull without printing progress information
    --no-deps                  Don't start linked services.
    --force-recreate           Recreate containers even if their configuration
                               and image haven't changed.
    --always-recreate-deps     Recreate dependent containers.
                               Incompatible with --no-recreate.
    --no-recreate              If containers already exist, don't recreate
                               them. Incompatible with --force-recreate and 
                               --renew-anon-volumes.
    --no-build                 Don't build an image, even if it's missing.
    --no-start                 Don't start the services after creating them.
    --build                    Build images before starting containers.
    --abort-on-container-exit  Stops all containers if any container was
                               stopped. Incompatible with --detach.
    --attach-dependencies      Attach to dependent containers.
    -t, --timeout TIMEOUT      Use this timeout in seconds for container
                               shutdown when attached or when containers are
                               already running. (default: 10)
    -V, --renew-anon-volumes   Recreate anonymous volumes instead of retrieving
                               data from the previous containers.
    --remove-orphans           Remove containers for services not defined
                               in the Compose file.
    --exit-code-from SERVICE   Return the exit code of the selected service
                               container. Implies --abort-on-container-exit.
    --scale SERVICE=NUM        Scale SERVICE to NUM instances. Overrides the
                               `scale` setting in the Compose file if present.
```

Docker Compose Down:

```
docker-compose down [options]
Options:
    --rmi type              Remove images. Type must be one of:
                              'all': Remove all images used by any service.
                              'local': Remove only images that don't have a
                              custom tag set by the `image` field.
    -v, --volumes           Remove named volumes declared in the `volumes`
                            section of the Compose file and anonymous volumes
                            attached to containers.
    --remove-orphans        Remove containers for services not defined in the
                            Compose file
    -t, --timeout TIMEOUT   Specify a shutdown timeout in seconds.
                            (default: 10)
```

Docker Compose Start:

Starts existing containers for a service

```
docker-compose docker-compose start [SERVICE...]
```

Docker Compose Stop:

Stops running containers without removing them. They can be started again with docker-compose start.

```
Usage: docker-compose stop [options] [SERVICE...]

Options:
  -t, --timeout TIMEOUT      Specify a shutdown timeout in seconds.
                             (default: 10)
```

Docker Compose Pull:

Pulls an image associated with a service defined in a docker-compose.yml or docker-stack.yml file, but does not start containers based on those images.

```
docker-compose pull [options] [SERVICE...]

Options:
    --ignore-pull-failures  Pull what it can and ignores images with pull failures.
    --parallel              Deprecated, pull multiple images in parallel (enabled by default).
    --no-parallel           Disable parallel pulling.
    -q, --quiet             Pull without printing progress information
    --include-deps          Also pull services declared as dependencies
```

Docker Compose Events:

Stream container events for every container in the project.

```
docker-compose events [SERVICE...]
```

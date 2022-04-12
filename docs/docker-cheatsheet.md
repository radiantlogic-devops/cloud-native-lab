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
	

## Kubernetes

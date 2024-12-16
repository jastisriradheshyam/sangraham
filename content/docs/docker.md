+++
title = 'Docker'
date = 2024-12-16T05:40:22+05:30
draft = false
+++

# docker common commands

- List all docker process/containers: `docker ps -a`
- List images: `docker images`
- List docker volumes: `docker volume ls`
- List docker networks: `docker network ls`
- Prune volumes: `docker volume prune`
- Prune networks: `docker network prune`
- Remove all containers: `docker rm -f $(docker ps -aq)`
- Remove all containers along with volumes: `docker rm -vf $(docker ps -aq)`
- Remove all images: `docker rmi $(docker images | awk 'NR>1 {print $3}')`
- Logs of the container: `docker logs continer_id`
- Logs of the container with follow: `docker logs -f container_id`
- Logs since N minutes (here 10 min.) with follow: `docker logs -f --since 10m container`
- Run bash in container: `docker exec -it container_id bash`

-----
## run a container
### new way
- `docker container run --publish 80:80 ngnix`
- `docker container run --publish 80:80 --detach ngnix`
- `docker container run --publish 80:80 --detach --name webhost ngnix`
### old way
- `docker run --publish 80:80 ngnix`
- `docker run --publish 80:80 --detach ngnix`
- `docker run --publish 80:80 --detach --name webhost ngnix`

## list containers
### new way
- `docker container ls`
### old way
- `docker ps`

## stop container
### new way`
- `docker container stop CONTAINER_ID`
## old way
- `docker stop CONTAINER_ID`

## container logs
### new way
- `docker container logs CONTAINER_ID`
### old way
- `docker logs CONTAINER_ID`

## container ps / top
### new way
- `docker contaniner top CONTAINER_ID`
## old way
- `docker top CONTAINER_ID`


## container start with bash
- `docker start -ai ubuntu`
  - `a` : attach
  - `i` : interactive

----

## Network
- `docker network ls`
- `docker network inspect`
- `docker network create --driver`
- `docker network connect`
- `docker network disconnect`


---

## Misc.
- docker layers image: `docker history IMAGE:TAG`

- Size reduction tool: https://github.com/wagoodman/dive#dive
- Distroless images: https://github.com/GoogleContainerTools/distroless
- Build without cache: `docker build --no-cache --pull ...`

# docker-compose

**Note**: with new Docker compose is built in so use it as sub command `docker compose` instead of `docker-compose`

- docker containers orchestrate as described in compose file: `docker-compose -f docker-compose-file.yaml up`
- docker containers remove as described in compose file: `docker-compose -f docker-compose-file.yaml down`
- docker containers stop as described in compose file: `docker-compose -f docker-compose-file.yaml stop`
- docker containers start as described in compose file: `docker-compose -f docker-compose-file.yaml start`
- docker containers orchestrate in detached mode as described in compose file: `docker-compose -f docker-compose-file.yaml up -d`
- docker containers logs as described in compose file: `docker-compose -f docker-compose-file.yaml logs`
- docker containers logs with follow as described in compose file: `docker-compose -f docker-compose-file.yaml logs -f`
- docker containers remove as described in compose file: `docker-compose -f docker-compose-file.yaml down`
- docker containers remove along with volumes as described in compose file: `docker-compose -f docker-compose-file.yaml down -v`


# Dockerfile

- `ARG`
    - The ARG instruction defines a variable that users can pass at build-time to the builder with the docker build command using the `--build-arg <varname>=<value>` flag.

```
ARG user1
ARG buildno
```
    - With default : `ARG buildno=1`
    - usage of argument

```
ARG SETTINGS
RUN ./run/setup $SETTINGS
```

```
ARG ALPINE_VER
FROM alpine:${ALPINE_VER} as peer-base
```

- `FROM`
    - The FROM instruction initializes a new build stage and sets the Base Image for subsequent instructions. As such, a valid Dockerfile must start with a FROM instruction.
    - Optionally a name can be given to a new build stage by adding AS name to the FROM instruction. The name can be used in subsequent FROM and `COPY --from=<name|index>` instructions to refer to the image built in this stage.

- `RUN`
    - The RUN instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile.
    - example
```
RUN <command>
or
RUN ["executable", "param1", "param2"]
```
- `WORKDIR`
    - The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile.
    - example
```
ENV DIRPATH /path
WORKDIR $DIRPATH/$DIRNAME
```

- `ADD`
    - The ADD instruction copies new files, directories or remote file URLs from `<src>` and adds them to the filesystem of the image at the path `<dest>`

```
ADD [--chown=<user>:<group>] <src>... <dest>
ADD [--chown=<user>:<group>] ["<src>",... "<dest>"]
```
    - Example: `ADD file:0c4555f363c2672e350001f1293e689875a3760afe7b3f9146886afe67121cba in /`

- `COPY`
    - COPY instruction is similar to ADD but with limited capabilities, see this link for further info
    - [docker - What is the difference between the 'COPY' and 'ADD' commands in a Dockerfile? - Stack Overflow](https://stackoverflow.com/questions/24958140/what-is-the-difference-between-the-copy-and-add-commands-in-a-dockerfile)
```
COPY --from=peer /go/src/github.com/hyperledger/fabric/build/bin /usr/local/bin
```

- `CMD`
    - There can only be one CMD instruction in a Dockerfile. If you list more than one CMD then only the last CMD will take effect.
    - The main purpose of a CMD is to provide defaults for an executing container.
```
CMD ["peer","node","start"]
```

- `EXPOSE`
    - The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime.
    - example : `EXPOSE 80/udp`

## Comprehensive Example

```Dockerfile
# Copyright IBM Corp. All Rights Reserved.
#
# SPDX-License-Identifier: Apache-2.0

ARG GO_VER
ARG ALPINE_VER

FROM alpine:${ALPINE_VER} as peer-base
RUN apk add --no-cache tzdata

FROM golang:${GO_VER}-alpine${ALPINE_VER} as golang
RUN apk add --no-cache \
	bash \
	gcc \
	git \
	make \
	musl-dev
ADD . $GOPATH/src/github.com/hyperledger/fabric
WORKDIR $GOPATH/src/github.com/hyperledger/fabric

FROM golang as peer
ARG GO_TAGS
RUN make peer GO_TAGS=${GO_TAGS}

FROM peer-base
ENV FABRIC_CFG_PATH /etc/hyperledger/fabric
VOLUME /etc/hyperledger/fabric
VOLUME /var/hyperledger
COPY --from=peer /go/src/github.com/hyperledger/fabric/build/bin /usr/local/bin
COPY --from=peer /go/src/github.com/hyperledger/fabric/sampleconfig/msp ${FABRIC_CFG_PATH}/msp
COPY --from=peer /go/src/github.com/hyperledger/fabric/sampleconfig/core.yaml ${FABRIC_CFG_PATH}
EXPOSE 7051
CMD ["peer","node","start"]
```

# private registry

- `docker container run -d -p 5000:5000 --name registry -v $(pwd)/registry-data/:/var/lib/registry regsitry`
- `docker push 127.0.0.1:5000/hello-world`

# secrets

- stored in memory and accessble only to container
- e.g:
  - `/run/secrets/SECRET_NAME`

---
creating secret

- `docker secret create db_secret db_secret.txt`
- `echo "password" | docker secret create db_secret -`

---
service with secrets

- `docker service create --name psql --secret psql_user --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_USER_FILE=/run/secrets/psql_user postgres`

---

## docker stack compose file:
```
version: "3.1"

services:
    psql:
        image: postgres
        secrets:
            - psql_user
            - psql_password
        environment:
            POSTGRES_PASSWORD_FILE: /run/secrets/psql_password
            POSTGRES_USER_FILE: /run/secrets/psql_user
secrets:
    psql_user:
        file: ./psql_user.txt
    psql_password:
        file: ./psql_password.txt
```

- `docker stack deploy -c docker-compose.yml db_stack_name`

# stacks

- `docker stack deploy -c stack_example.yml STACK_NAME`
- `docker stack rm STACK_NAME`
- `docker stack ps STACK_NAME`
- `docker stack ls`

# docker swarm

- `docker swarm init`
- `docker node ls`
- `docker service create alpine ping 8.8.8.8`
- `docker service ps SERVICE_NAME`
- `docker service update <ID> --replicas 3`
- `docker service rm SERVICE_NAME`



---

### node 1
- `docker swarm init`
### node 2 and 3
- `docker swarm join --token SWMTKN-1-25v0dnvieneukkkgl8wd39ohlrbbs6z7k20r1se77y5q2vbs2e-3yhoecp5c8m8z2m0z3uhus4ia 10.128.0.2:2377`
### making node 2 and 3 managers from node 1
- `docker node update --role manager node 2`
- `docker node update --role manager node 3`
### creating a service that is replicated in three nodes
- `docker service create --replicas 3 alpine ping 8.8.8.8`

---
# Overlay multi-host networking

- `--driver overlay`
- for container to container traffic inside a single Swarm
- Optional IPSec (AES) encryption on network creation
- each service can be connected to mutiple networks
  - (e.g front end, back end)

---
# Routing mesh
- Routes ingress (incoming) packets for a service to proper task
- spans all nodes in swarm
- uses IPVS from Linux Kernel
- load balances swarm services across their tasks
-Two ways this works:
- Container to container in a overlay network ( uses VIP )
- external traffic incoming to published ports (all nodes listen)
- This is stateless load balancing
- this load balancing is at OSI layer 3 (TCP), not layer 4 (DNS)

# Build X

- `buildx` plugin uses Buildkit to build in concurrent manner (in multi stage builds)
  - If a stage is not used by other stages it will be skipped, and
  - **CAUTION**: also if any build argument is used in a stage and they are explicitly overridden by passing through docker build command, then the stage will be built even if it is not used by any other stage.
- Installation script in easy_compute repo -> `install/docker/buildx-install.sh`

# Docker Deploy

```yaml
version: "3"
services:
        redis:
                image: redis:alpine
                ports:
                        - "6379"
                networks:
                        - frontend
                deploy:
                        replicas: 2
                        update_config:
                                parallelism: 2
                                delay: 10s
                        restart_policy:
                                condition: on-failure
        db:
                image: postgres:9.4
                volumes:
                        - db-data:/var/lib/postgresql/data
                networks:
                        - backend
                deploy:
                        placement:
                                constraints: [node.role == manager]
        vote:
                image: dockersamples/examplevotingapp_vote:before
                ports:
                        - 5000:80
                networks:
                        - frontend
                depends_on:
                        - redis
                deploy:
                        replicas: 2
                        update_config:
                                parallelism: 2
                        restart_policy:
                                condition: on-failure
        result:
                image: dockersamples/examplevotingapp_result:before
                ports:
                        - 5001:80
                networks:
                        - backend
                depends_on:
                        - db
                deploy:
                        replicas: 1
                        update_config:
                                parallelism: 2
                                delay: 10s
                        restart_policy:
                                condition: on-failure
        worker:
                image: dockersamples/examplevotingapp_worker
                networks:
                        - frontend
                        - backend
                deploy:
                        mode: replicated
                        replicas: 1
                        labels: [APP=VOTING]
                        restart_policy:
                                condition: on-failure
                                delay: 10s
                                max_attempts: 3
                                window: 120s
                        placement:
                                constraints: [node.role == manager]
networks:
        frontend:
        backend:
volumes:
        db-data:
```

# References:

1. [docker buildx ](https://docs.docker.com/engine/reference/commandline/buildx/)
2. [GitHub - docker/buildx: Docker CLI plugin for extended build capabilities with BuildKit](https://github.com/docker/buildx)
3. [GitHub - moby/buildkit: concurrent, cache-efficient, and Dockerfile-agnostic builder toolkit](https://github.com/moby/buildkit)

# Nginx Load balancer NodeJS

Nginx Load balancer for a dockerized NodeJS application Using 2 containers.

## Prerequisites

- Install [Docker](https://docs.docker.com/install/linux/docker-ce/centos/)

## Overview

- RUN: `docker build -t nodeapp:01`
  Once the image is built you can see it using the `docker images` command

- RUN: `docker container run -p 5001:5000 --name helloworld -d nodeapp:01`
- RUN: `docker container run -p 5002:5000 --name customized -e "name=guys" -d nodeapp:01`

Check the browser for your http://ip:port and verify that the containers are successfully deployed.
we can see one container is running on host port 5001 and other on host port 5002.

- We set up a proxy in nginx.conf using upstream and added our two server addresses which needed to be load balanced and we set the load balancing algorithm to be least_connection instead of the default round robin.
  To learn more about load balancing with nginx you can refer [this](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/)

- RUN: `docker build -t nginxbalancer:01 .`
- RUN: `docker container run --name nginxbalancer -p 5000:80 -d nginxbalancer:01`

If things worked correctly, You should visit your IP:5000 on your browser and hit refresh multiple to see both outputs on the same address meaning that nginx is redirecting our http request to both containers and balancing the load overall.

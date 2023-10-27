# DJ26 WEB APP

## docker build
- https://hub.docker.com/_/httpd
```bash
$ docker build -t my-apache2 .
$ sudo docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
my-apache2   latest    e133bdde4db8   2 minutes ago   173MB
```

## docker run
``` bash
$ sudo docker run -dit --name my-webapp -p 8080:80 my-apache2
$ sudo docker ps
CONTAINER ID   IMAGE        COMMAND              CREATED         STATUS         PORTS                                   NAMES
c52058cd5124   my-apache2   "httpd-foreground"   6 seconds ago   Up 5 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   my-webapp
```

### into docker
```bash
$ sudo docker exec -it my-webapp bash

root@c52058cd5124:/usr/local/apache2# ls -l
total 40
drwxr-xr-x 2 root root 4096 Oct 11 20:23 bin
drwxr-xr-x 2 root root 4096 Oct 11 20:23 build
drwxr-xr-x 2 root root 4096 Oct 11 20:23 cgi-bin
drwxr-xr-x 4 root root 4096 Oct 11 20:23 conf
drwxr-xr-x 3 root root 4096 Oct 11 20:23 error
drwxr-xr-x 1 root root 4096 Oct 18 21:12 htdocs
drwxr-xr-x 3 root root 4096 Oct 11 20:23 icons
drwxr-xr-x 2 root root 4096 Oct 11 20:23 include
drwxr-xr-x 1 root root 4096 Oct 18 21:13 logs
drwxr-xr-x 2 root root 4096 Oct 11 20:23 modules

root@c52058cd5124:/usr/local/apache2# cd htdocs/
root@c52058cd5124:/usr/local/apache2/htdocs# ls -l
total 96
-rw-r--r-- 1 root root    49 Oct 18 21:12 Dockerfile
-rw-r--r-- 1 root root 17128 Oct 19  2023 LICENSE.txt
-rw-r--r-- 1 root root    84 Oct 19  2023 LICENSE.txt:Zone.Identifier
-rw-r--r-- 1 root root   170 Oct 18 21:11 README.md
-rw-r--r-- 1 root root  1344 Oct 19  2023 README.txt
-rw-r--r-- 1 root root    84 Oct 19  2023 README.txt:Zone.Identifier
drwxr-xr-x 6 root root  4096 Oct 18 20:20 assets
-rw-r--r-- 1 root root 18398 Oct 19  2023 elements.html
-rw-r--r-- 1 root root    84 Oct 19  2023 elements.html:Zone.Identifier
-rw-r--r-- 1 root root  5045 Oct 19  2023 generic.html
-rw-r--r-- 1 root root    84 Oct 19  2023 generic.html:Zone.Identifier
drwxr-xr-x 2 root root  4096 Oct 18 20:20 images
-rw-r--r-- 1 root root  7195 Oct 18 21:04 index.html
-rw-r--r-- 1 root root    84 Oct 19  2023 index.html:Zone.Identifier
root@c52058cd5124:/usr/local/apache2/htdocs#
```

### how2pr
- https://oss.cashmallow.com/team/how2pr/


### Deploy Production
- merge PR to main

### Deploy Pre-Production
- [ ] https://dj-twenty-six.web.app
```bash
$ firebase deploy

=== Deploying to 'dj-twenty-six'...

i  deploying hosting
i  hosting[dj-twenty-six]: beginning deploy...
i  hosting[dj-twenty-six]: found 364 files in /
✔  hosting[dj-twenty-six]: file upload complete
i  hosting[dj-twenty-six]: finalizing version...
✔  hosting[dj-twenty-six]: version finalized
i  hosting[dj-twenty-six]: releasing new version...
✔  hosting[dj-twenty-six]: release complete

✔  Deploy complete!

Project Console: https://console.firebase.google.com/project/dj-twenty-six/overview
Hosting URL: https://dj-twenty-six.web.app
```

### BMT
- hosts
```
# bmt
127.0.0.1	homepage.flyio.local
```

- server start
- https://docs.docker.com/engine/reference/commandline/compose_up/#options
```bash
# $ docker compose up -d --build --force-recreate
$ docker compose up -d
[+] Running 3/3
 ✔ Network dj-twenty-sixgithubio_default       Created                              0.1s
 ✔ Container dj-twenty-sixgithubio-homepage-1  Started                              0.0s
 ✔ Container dj-twenty-sixgithubio-nginx-lb-1  Started                              0.0s
```

![image](https://github.com/dj-twenty-six/dj-twenty-six.github.io/assets/87309910/7c805f2b-9950-4e27-aa8f-db1f859ffad7)

- 
```bash
$ docker compose -f ./manual-proxy-compose.yml up -d --build
[+] Building 0.7s (7/7) FINISHED                                                                                                                                                                                                                              docker:default
 => [load_balancer internal] load build definition from Dockerfile                                                                                                                                                                                                      0.0s
 => => transferring dockerfile: 114B                                                                                                                                                                                                                                    0.0s
 => [load_balancer internal] load .dockerignore                                                                                                                                                                                                                         0.0s
 => => transferring context: 2B                                                                                                                                                                                                                                         0.0s
 => [load_balancer internal] load metadata for docker.io/library/nginx:1.25.3                                                                                                                                                                                           0.7s
 => [load_balancer internal] load build context                                                                                                                                                                                                                         0.0s
 => => transferring context: 34B                                                                                                                                                                                                                                        0.0s
 => [load_balancer 1/2] FROM docker.io/library/nginx:1.25.3@sha256:add4792d930c25dd2abf2ef9ea79de578097a1c175a16ab25814332fe33622de                                                                                                                                     0.0s
 => CACHED [load_balancer 2/2] COPY [default.conf, /etc/nginx/conf.d/]                                                                                                                                                                                                  0.0s
 => [load_balancer] exporting to image                                                                                                                                                                                                                                  0.0s
 => => exporting layers                                                                                                                                                                                                                                                 0.0s
 => => writing image sha256:ddbbce8e85c2bc0daf2011afefb40f0450bc3ed1500a414de604293d44fab13c                                                                                                                                                                            0.0s
 => => naming to docker.io/library/bmt_lb-load_balancer                                                                                                                                                                                                                 0.0s
[+] Running 2/0
 ✔ Container bmt_lb-homepage_1-1  Running                                                                                                                                                                                                                               0.0s
 ✔ Container mproxy               Running                                                                                                                                                                                                                               0.0s

$ docker compose ps
NAME      IMAGE     COMMAND   SERVICE   CREATED   STATUS    PORTS

$ docker compose -f ./manual-proxy-compose.yml ps
NAME                  IMAGE                                     COMMAND                                          SERVICE         CREATED          STATUS          PORTS
bmt_lb-homepage_1-1   pysatellite/dj-twenty-six.github.io:bmt   "httpd-foreground"                               homepage_1      7 minutes ago    Up 3 minutes    80/tcp
mproxy                bmt_lb-load_balancer                      "/docker-entrypoint.sh nginx -g 'daemon off;'"   load_balancer   45 seconds ago   Up 44 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp

$ sudo docker stats --no-stream
CONTAINER ID   NAME                  CPU %     MEM USAGE / LIMIT     MEM %     NET I/O       BLOCK I/O   PIDS
9f4529c2caf2   mproxy                0.00%     7.172MiB / 7.625GiB   0.09%     796B / 0B     0B / 0B     9
644e9dac4e50   bmt_lb-homepage_1-1   0.01%     22.09MiB / 30MiB      73.62%    1.09kB / 0B   0B / 0B     82
```

### Ref
- [nginx-및-nginx-plus를-사용한-caching](https://nginxstore.com/blog/nginx/nginx-%EB%B0%8F-nginx-plus%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%9C-caching/)


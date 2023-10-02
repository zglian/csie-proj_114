Run container

<br>

### Solution

Check current container status

input:
```
podman ps
```

output:
```
$ podman ps
CONTAINER ID  IMAGE                                    COMMAND     CREATED         STATUS         PORTS       NAMES
1d16e5700bb2  docker.io/library/alpine:latest          sh          2 days ago      Up 2 days                  competent_tesla
0eb85463b093  localhost/podman-pause:4.6.2-1694548869              2 days ago      Up 2 days                  aed1dcce39a5-infra
9ea035d01911  docker.io/library/alpine:latest          top         2 days ago      Up 2 days                  nostalgic_jones
a894c236c769  docker.io/library/alpine:latest          sh          2 days ago      Up 2 days                  charming_wu
33550b56b0f6  docker.io/library/alpine:latest          sh          54 seconds ago  Up 54 seconds              eloquent_kalam
```

run alpine
```
podman run -it alpine sh
```

or

```
podman run -it docker.io/libray/alpine:latest sh
```

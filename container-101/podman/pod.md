
```
podman pod ls
# or
podman pod ps
```


```
$ podman pod ps
POD ID        NAME            STATUS      CREATED     INFRA ID      # OF CONTAINERS
aed1dcce39a5  awesome_austin  Degraded    2 days ago  0eb85463b093  4
```


```
# podman ps --pod
CONTAINER ID  IMAGE                                    COMMAND     CREATED     STATUS      PORTS       NAMES               POD ID        PODNAME
1d16e5700bb2  docker.io/library/alpine:latest          sh          2 days ago  Up 2 days               competent_tesla                   
0eb85463b093  localhost/podman-pause:4.6.2-1694548869              2 days ago  Up 2 days               aed1dcce39a5-infra  aed1dcce39a5  awesome_austin
9ea035d01911  docker.io/library/alpine:latest          top         2 days ago  Up 2 days               nostalgic_jones     aed1dcce39a5  awesome_austin
a894c236c769  docker.io/library/alpine:latest          sh          2 days ago  Up 2 days               charming_wu         aed1dcce39a5  awesome_austin
```

```
podman pod create
```

```
podman pod create mypod
```


```
# podman pod ps
POD ID        NAME            STATUS      CREATED        INFRA ID      # OF CONTAINERS
4aa674492648  mypod           Created     4 seconds ago  c488abbe41d1  1
aed1dcce39a5  awesome_austin  Degraded    2 days ago     0eb85463b093  4
```

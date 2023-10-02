Run container

<br>

### Solution

Check current container status

input:
```
podman search fedora
```


````
cat /etc/containers/registries.conf
```

https://github.com/containers/image/blob/main/docs/containers-registries.conf.5.md

```
...
unqualified-search-registries = ["registry.fedoraproject.org", "docker.io", "quay.io"]
...

```


output:
```
$ podman search --limit 3 fedora 
NAME                                           DESCRIPTION
registry.fedoraproject.org/f29/fedora-toolbox  
registry.fedoraproject.org/f30/fedora-toolbox  
registry.fedoraproject.org/f31/fedora-toolbox  
docker.io/library/fedora                       Official Docker builds of Fedora
docker.io/kasmweb/fedora-37-desktop            Fedora 37 desktop for Kasm Workspaces 
docker.io/kasmweb/fedora-38-desktop            
quay.io/fedora/fedora                          
quay.io/skiffos/skiff-core-fedora              
quay.io/containerdisks/fedora                  # Fedora Containerdisk Images  <img src="htt...
```

However, https://hub.docker.com/ provide much useful information.

https://unix.stackexchange.com/questions/706472/how-do-i-get-the-cgroup-path-for-a-podman-container


normal container
```
/sys/fs/cgroup/machine.slice/libpod-<pid>.scope/
/sys/fs/cgroup/machine.slice/libpod-conmon-<pid>.scope/
libpod-1d16e5700bb207936a96b02cfe929fa161e5685aa15186f4c8be5dc44821b860.scope/
````

pod

```
machine-libpod_pod_aed1dcce39a52379aaa25179323c2597863a7a9bc9a974950c58d6b5ea4f04e7.slice

machine-libpod_pod_<pid>.slice/libpod-<pid>.scope/ 
machine-libpod_pod_<pid>.slice/libpod-conmon-<pid>.scope/ 
```


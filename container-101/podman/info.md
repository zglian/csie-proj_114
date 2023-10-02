
```
#  podman info
host:
  arch: amd64
  buildahVersion: 1.31.2
  cgroupControllers:
  - cpuset
  - cpu
  - io
  - memory
  - hugetlb
  - pids
  - rdma
  - misc
  cgroupManager: systemd
  cgroupVersion: v2
  conmon:
    package: conmon-2.1.7-3.fc39.x86_64
    path: /usr/bin/conmon
    version: 'conmon version 2.1.7, commit: '
  cpuUtilization:
    idlePercent: 89.13
    systemPercent: 2.14
    userPercent: 8.73
  cpus: 4
  databaseBackend: boltdb
  distribution:
    distribution: fedora
    variant: silverblue
    version: "39"
  eventLogger: journald
  freeLocks: 2005
  hostname: sb470
  idMappings:
    gidmap: null
    uidmap: null
  kernel: 6.5.5-300.fc39.x86_64
  linkmode: dynamic
  logDriver: k8s-file
  memFree: 1697759232
  memTotal: 20849172480
  networkBackend: netavark
  networkBackendInfo:
    backend: netavark
    dns:
      package: aardvark-dns-1.7.0-2.fc39.x86_64
      path: /usr/libexec/podman/aardvark-dns
      version: aardvark-dns 1.7.0
    package: netavark-1.7.0-2.fc39.x86_64
    path: /usr/libexec/podman/netavark
    version: netavark 1.7.0
  ociRuntime:
    name: crun
    package: crun-1.9-1.fc39.x86_64
    path: /usr/bin/crun
    version: |-
      crun version 1.9
      commit: a538ac4ea1ff319bcfe2bf81cb5c6f687e2dc9d3
      rundir: /run/crun
      spec: 1.0.0
      +SYSTEMD +SELINUX +APPARMOR +CAP +SECCOMP +EBPF +CRIU +LIBKRUN +WASM:wasmedge +YAJL
  os: linux
  pasta:
    executable: /usr/bin/pasta
    package: passt-0^20230908.g05627dc-1.fc39.x86_64
    version: |
      pasta 0^20230908.g05627dc-1.fc39.x86_64
      Copyright Red Hat
      GNU General Public License, version 2 or later
        <https://www.gnu.org/licenses/old-licenses/gpl-2.0.html>
      This is free software: you are free to change and redistribute it.
      There is NO WARRANTY, to the extent permitted by law.
  remoteSocket:
    exists: true
    path: /run/podman/podman.sock
  security:
    apparmorEnabled: false
    capabilities: CAP_CHOWN,CAP_DAC_OVERRIDE,CAP_FOWNER,CAP_FSETID,CAP_KILL,CAP_NET_BIND_SERVICE,CAP_SETFCAP,CAP_SETGID,CAP_SETPCAP,CAP_SETUID,CAP_SYS_CHROOT
    rootless: false
    seccompEnabled: true
    seccompProfilePath: /usr/share/containers/seccomp.json
    selinuxEnabled: false
  serviceIsRemote: false
  slirp4netns:
    executable: /usr/bin/slirp4netns
    package: slirp4netns-1.2.1-1.fc39.x86_64
    version: |-
      slirp4netns version 1.2.1
      commit: 09e31e92fa3d2a1d3ca261adaeb012c8d75a8194
      libslirp: 4.7.0
      SLIRP_CONFIG_VERSION_MAX: 4
      libseccomp: 2.5.3
  swapFree: 7044681728
  swapTotal: 8589930496
  uptime: 144h 37m 29.00s (Approximately 6.00 days)
plugins:
  authorization: null
  log:
  - k8s-file
  - none
  - passthrough
  - journald
  network:
  - bridge
  - macvlan
  - ipvlan
  volume:
  - local
registries:
  search:
  - registry.fedoraproject.org
  - docker.io
  - quay.io
store:
  configFile: /etc/containers/storage.conf
  containerStore:
    number: 33
    paused: 0
    running: 4
    stopped: 29
  graphDriverName: overlay
  graphOptions:
    overlay.mountopt: nodev,metacopy=off
  graphRoot: /var/lib/containers/storage
  graphRootAllocated: 998500204544
  graphRootUsed: 589627756544
  graphStatus:
    Backing Filesystem: btrfs
    Native Overlay Diff: "true"
    Supports d_type: "true"
    Using metacopy: "false"
  imageCopyTmpDir: /var/tmp
  imageStore:
    number: 318
  runRoot: /run/containers/storage
  transientStore: false
  volumePath: /var/lib/containers/storage/volumes
version:
  APIVersion: 4.6.2
  Built: 1694548869
  BuiltTime: Wed Sep 13 04:01:09 2023
  GitCommit: ""
  GoVersion: go1.21.0
  Os: linux
  OsArch: linux/amd64
  Version: 4.6.2
```




killercoda

```
 podman info                      
host:
  arch: amd64
  buildahVersion: 1.23.1
  cgroupControllers:
  - cpuset
  - cpu
  - cpuacct
  - blkio
  - memory
  - devices
  - freezer
  - net_cls
  - perf_event
  - net_prio
  - hugetlb
  - pids
  - rdma
  cgroupManager: systemd
  cgroupVersion: v1
  conmon:
    package: 'conmon: /usr/libexec/podman/conmon'
    path: /usr/libexec/podman/conmon
    version: 'conmon version 2.1.2, commit: '
  cpus: 1
  distribution:
    codename: focal
    distribution: ubuntu
    version: "20.04"
  eventLogger: journald
  hostname: ubuntu
  idMappings:
    gidmap: null
    uidmap: null
  kernel: 5.4.0-131-generic
  linkmode: dynamic
  logDriver: journald
  memFree: 74588160
  memTotal: 2079682560
  ociRuntime:
    name: crun
    package: 'crun: /usr/bin/crun'
    path: /usr/bin/crun
    version: |-
      crun version UNKNOWN
      commit: ea1fe3938eefa14eb707f1d22adff4db670645d6
      spec: 1.0.0
      +SYSTEMD +SELINUX +APPARMOR +CAP +SECCOMP +EBPF +CRIU +YAJL
  os: linux
  remoteSocket:
    path: /run/podman/podman.sock
  security:
    apparmorEnabled: true
    capabilities: CAP_CHOWN,CAP_DAC_OVERRIDE,CAP_FOWNER,CAP_FSETID,CAP_KILL,CAP_NET_BIND_SERVICE,CAP_SETFCAP,CAP_SETGID,CAP_SETPCAP,CAP_SETUID,CAP_SYS_CHROOT
    rootless: false
    seccompEnabled: true
    seccompProfilePath: /usr/share/containers/seccomp.json
    selinuxEnabled: false
  serviceIsRemote: false
  slirp4netns:
    executable: /usr/bin/slirp4netns
    package: 'slirp4netns: /usr/bin/slirp4netns'
    version: |-
      slirp4netns version 1.1.8
      commit: unknown
      libslirp: 4.3.1-git
      SLIRP_CONFIG_VERSION_MAX: 3
      libseccomp: 2.4.3
  swapFree: 1073201152
  swapTotal: 1073737728
  uptime: 14m 20.53s
plugins:
  log:
  - k8s-file
  - none
  - journald
  network:
  - bridge
  - macvlan
  volume:
  - local
registries:
  search:
  - docker.io
  - quay.io
store:
  configFile: /etc/containers/storage.conf
  containerStore:
    number: 1
    paused: 0
    running: 1
    stopped: 0
  graphDriverName: overlay
  graphOptions:
    overlay.mountopt: nodev,metacopy=on
  graphRoot: /var/lib/containers/storage
  graphStatus:
    Backing Filesystem: extfs
    Native Overlay Diff: "false"
    Supports d_type: "true"
    Using metacopy: "true"
  imageStore:
    number: 1
  runRoot: /run/containers/storage
  volumePath: /var/lib/containers/storage/volumes
version:
  APIVersion: 3.4.2
  Built: 0
  BuiltTime: Thu Jan  1 00:00:00 1970
  GitCommit: ""
  GoVersion: go1.15.2
  OsArch: linux/amd64
  Version: 3.4.2
```

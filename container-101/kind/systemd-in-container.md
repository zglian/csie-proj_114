
```shell
systemd─┬─ModemManager───3*[{ModemManager}]
       ...
        ├─conmon───systemd─┬─containerd───19*[{containerd}]
        │                  ├─containerd-shim─┬─kube-scheduler───9*[{kube-scheduler}]
        │                  │                 ├─pause
        │                  │                 └─12*[{containerd-shim}]
        │                  ├─containerd-shim─┬─kube-controller───6*[{kube-controller}]
        │                  │                 ├─pause
        │                  │                 └─12*[{containerd-shim}]

```

```shell
root@kind-control-plane:/# systemctl status
● kind-control-plane
    State: running
     Jobs: 0 queued
   Failed: 0 units
    Since: Wed 2023-10-04 15:27:22 UTC; 2 days ago
   CGroup: /
           ├─init.scope 
           │ ├─    1 /sbin/init
           │ ├─ 1455 bash
           │ ├─39981 bash
           │ ├─39990 systemctl status
           │ └─39991 (pager)
           ├─system.slice 
           │ ├─containerd.service …
           │ │ ├─ 103 /usr/local/bin/containerd
           │ │ ├─ 263 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id db55d14e0019b9392ca0245dd324ba3087ad22577b0f3e4ec10afb220ba3318b -address /run/containerd/containerd.sock
           │ │ ├─ 264 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id 4ac056f4267846210f5b99abd894cd36fe6021fbe54d3a74439378cdb568e482 -address /run/containerd/containerd.sock
           │ │ ├─ 270 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id d4b48d2f44838de72f2e0d5fc535ea141e617d82d357427824cc66eb64c2c24a -address /run/containerd/containerd.sock
           │ │ ├─ 298 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id bbd60b1475485b2e090bbd001233af2f6fde76b65389e70f2adb94787a04d2e6 -address /run/containerd/containerd.sock
           │ │ ├─ 722 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id f0d5ee118bfa181b97ed99f8c32f31f7f29822efb448ea1aedcfd3c047c4ab77 -address /run/containerd/containerd.sock
           │ │ ├─ 750 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id e70cff93befb38cbdbe6b02f6d012fb63939b5b0a5227284bcfb38c1ae0b7b7c -address /run/containerd/containerd.sock
           │ │ ├─1129 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id d26c040592bfb4e099938d8c677f5df654749f8727223b000f7d30d5ec5bc78c -address /run/containerd/containerd.sock
           │ │ ├─1157 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id 49b0f0a68bf3d5768c08b9c2baa33bc4a6a91351ecee92843ca3f0389da5979e -address /run/containerd/containerd.sock
           │ │ └─1191 /usr/local/bin/containerd-shim-runc-v2 -namespace k8s.io -id bccd392d1ccc97f74fbcbdaa5e3f056add28c1e78ea3f4cc54b5757abfef7039 -address /run/containerd/containerd.sock
           │ └─systemd-journald.service 
           │   └─91 /lib/systemd/systemd-journald
           └─kubelet.slice 
             ├─kubelet.service 
             │ └─646 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --config=/var/lib/kubelet/config.yaml --container-runtime-endpoint=unix:///run/containerd/containerd.sock --node-ip=10.89.0.2 --node-labels= --pod-infra-container-image=registry.k8s.io/pause:3.9 --provider-id=kind://podman/kind/kind-control-plane --runtime-cgroups=/system.slice/containerd.service
             └─kubelet-kubepods.slice 
               ├─kubelet-kubepods-pod25481da8_5ec3_4008_9d54_a47f9a615e58.slice 
               │ ├─cri-containerd-82c05f0822fece7008091b6aa5f716e6636b2160e54760ff93799a678a7a55bc.scope …
               │ │ └─980 /bin/kindnetd
               │ └─cri-containerd-f0d5ee118bfa181b97ed99f8c32f31f7f29822efb448ea1aedcfd3c047c4ab77.scope …
               │   └─756 /pause
               ├─kubelet-kubepods-besteffort.slice 
               │ ├─kubelet-kubepods-besteffort-pode0e7502c_3e95_4e46_bb0d_a42725b3fbd0.slice 
               │ │ ├─cri-containerd-1ee3921995dd56e674f60e90e107d900d40505fa9679870c98a358d236b76c7e.scope …
               │ │ │ └─1402 local-path-provisioner --debug start --helper-image docker.io/kindest/local-path-helper:v20230510-486859a6 --config /etc/config/config.json
               │ │ └─cri-containerd-bccd392d1ccc97f74fbcbdaa5e3f056add28c1e78ea3f4cc54b5757abfef7039.scope …
               │ │   └─1235 /pause
               │ └─kubelet-kubepods-besteffort-pod2ea4d65b_3d51_440d_8009_5beed93c7b82.slice 
               │   ├─cri-containerd-543ea349bc07b978c9e997752adb9d0fb3a97b86670a4b48314c18eb66eb677e.scope …
               │   │ └─818 /usr/local/bin/kube-proxy --config=/var/lib/kube-proxy/config.conf --hostname-override=kind-control-plane
               │   └─cri-containerd-e70cff93befb38cbdbe6b02f6d012fb63939b5b0a5227284bcfb38c1ae0b7b7c.scope …
               │     └─778 /pause
               └─kubelet-kubepods-burstable.slice 
                 ├─kubelet-kubepods-burstable-podb192bc79b664e59b2a5862c8486030a1.slice 
                 │ ├─cri-containerd-4ac056f4267846210f5b99abd894cd36fe6021fbe54d3a74439378cdb568e482.scope …
                 │ │ └─364 /pause
                 │ └─cri-containerd-dca110a2f0f7efc4d5414a120506dbfe9b00590e8f4be778db808f2b26d14d6c.scope …
                 │   └─480 kube-controller-manager --allocate-node-cidrs=true --authentication-kubeconfig=/etc/kubernetes/controller-manager.conf --authorization-kubeconfig=/etc/kubernetes/controller-manager.conf --bind-address=127.0.0.1 --client-ca-file=/etc/kubernetes/pki/ca.crt --cluster-cidr=10.244.0.0/16 --cluster-name=kind --cluster-signing-cert-file=/etc/kubernetes/pki/ca.crt --cluster-signing-key-file=/etc/kubernetes/pki/ca.key --controllers=*,bootstrapsigner,tokencleaner --enable-hostpath-provisioner=true --kubeconfig=/etc/kubernetes/controller-manager.conf --leader-elect=true --requestheader-client-ca-file=/etc/kubernetes/pki/front-proxy-ca.crt --root-ca-file=/etc/kubernetes/pki/ca.crt --service-account-private-key-file=/etc/kubernetes/pki/sa.key --service-cluster-ip-range=10.96.0.0/16 --use-service-account-credentials=true
                 ├─kubelet-kubepods-burstable-poda680e7c33873fe2ce5d0601c71e8c7b0.slice 
                 │ ├─cri-containerd-bbd60b1475485b2e090bbd001233af2f6fde76b65389e70f2adb94787a04d2e6.scope …
```
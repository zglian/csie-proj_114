
```
root@kind-control-plane:/# crictl ps
CONTAINER           IMAGE               CREATED             STATE               NAME                      ATTEMPT             POD ID              POD
1ee3921995dd5       ce18e076e9d4b       2 days ago          Running             local-path-provisioner    0                   bccd392d1ccc9       local-path-provisioner-6bc4bddd6b-v28nx
fd35e7a0f6ef0       ead0a4a53df89       2 days ago          Running             coredns                   0                   49b0f0a68bf3d       coredns-5d78c9869d-tg66l
64269ab284602       ead0a4a53df89       2 days ago          Running             coredns                   0                   d26c040592bfb       coredns-5d78c9869d-zzk2j
82c05f0822fec       b0b1fa0f58c6e       2 days ago          Running             kindnet-cni               0                   f0d5ee118bfa1       kindnet-zspqh
543ea349bc07b       9d5429f6d7697       2 days ago          Running             kube-proxy                0                   e70cff93befb3       kube-proxy-wtdck
cab2d333c143a       86b6af7dd652c       2 days ago          Running             etcd                      0                   d4b48d2f44838       etcd-kind-control-plane
0cdaa9ef8c494       c604ff157f0cf       2 days ago          Running             kube-apiserver            0                   bbd60b1475485       kube-apiserver-kind-control-plane
dca110a2f0f7e       9f8f3a9f3e8a9       2 days ago          Running             kube-controller-manager   0                   4ac056f426784       kube-controller-manager-kind-control-plane
e65d20d424129       205a4d549b94d       2 days ago          Running             kube-scheduler            0                   db55d14e0019b       kube-scheduler-kind-control-plane
```

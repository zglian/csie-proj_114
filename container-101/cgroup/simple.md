
## Cgroupv1

有多個控制器，可以針對不同的資源進行管理（memory,CPU...）

```Shell
**~$ mount -t cgroup**
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,name=systemd)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,rdma)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
```
在memory中新增名字為democgv1的cgroup
```Shell
**~$ mkdir /sys/fs/cgroup/memory/democgv1** 
```
自動產生好控制資源 (Memory) 時所需要的組態檔案
```Shell
**~$ ls -l /sys/fs/cgroup/memory/democgv1**
total 0
-rw-r--r-- 1 root root 0 Sep 29 13:39 cgroup.clone_children
--w--w--w- 1 root root 0 Sep 29 13:39 cgroup.event_control
-rw-r--r-- 1 root root 0 Sep 29 13:39 cgroup.procs
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.failcnt
--w------- 1 root root 0 Sep 29 13:39 memory.force_empty
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.failcnt
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.limit_in_bytes
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.max_usage_in_bytes
-r--r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.slabinfo
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.tcp.failcnt
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.tcp.limit_in_bytes
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.tcp.max_usage_in_bytes
-r--r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.tcp.usage_in_bytes
-r--r--r-- 1 root root 0 Sep 29 13:39 memory.kmem.usage_in_bytes
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.limit_in_bytes
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.max_usage_in_bytes
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.memsw.failcnt
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.memsw.limit_in_bytes
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.memsw.max_usage_in_bytes
-r--r--r-- 1 root root 0 Sep 29 13:39 memory.memsw.usage_in_bytes
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.move_charge_at_immigrate
-r--r--r-- 1 root root 0 Sep 29 13:39 memory.numa_stat
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.oom_control
---------- 1 root root 0 Sep 29 13:39 memory.pressure_level
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.soft_limit_in_bytes
-r--r--r-- 1 root root 0 Sep 29 13:39 memory.stat
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.swappiness
-r--r--r-- 1 root root 0 Sep 29 13:39 memory.usage_in_bytes
-rw-r--r-- 1 root root 0 Sep 29 13:39 memory.use_hierarchy
-rw-r--r-- 1 root root 0 Sep 29 13:39 notify_on_release
-rw-r--r-- 1 root root 0 Sep 29 13:39 tasks
```

## Cgroupv1切換到 Cgroupv2

```Shell
**~$ echo 'GRUB_CMDLINE_LINUX_DEFAULT="${GRUB_CMDLINE_LINUX_DEFAULT} systemd.unified_cgroup_hierarchy=1"' | sudo tee /etc/default/grub.d/70-cgroup-unified.cfg
~$ sudo update-grub
~$ sudo reboot -h now**
# 重新開機登入機器後，透過下面指令檢查該檔案是否存在來判斷 cgroup v2 啟用與否
**~$ ls /sys/fs/cgroup/cgroup.controllers**
```

## Cgroupv2

```Shell
**~$ mount | grep cgroup**
cgroup2 on /sys/fs/cgroup type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate)
**~$ ls -l /sys/fs/cgroup**
total 0
-r--r--r--  1 root root 0 Sep 29 14:13 cgroup.controllers
-rw-r--r--  1 root root 0 Sep 29 14:20 cgroup.max.depth
-rw-r--r--  1 root root 0 Sep 29 14:20 cgroup.max.descendants
-rw-r--r--  1 root root 0 Sep 29 14:13 cgroup.procs
-r--r--r--  1 root root 0 Sep 29 14:20 cgroup.stat
-rw-r--r--  1 root root 0 Sep 29 14:13 cgroup.subtree_control
-rw-r--r--  1 root root 0 Sep 29 14:20 cgroup.threads
-rw-r--r--  1 root root 0 Sep 29 14:20 cpu.pressure
-r--r--r--  1 root root 0 Sep 29 14:20 cpu.stat
-r--r--r--  1 root root 0 Sep 29 14:20 cpuset.cpus.effective
-r--r--r--  1 root root 0 Sep 29 14:20 cpuset.mems.effective
drwxr-xr-x  2 root root 0 Sep 29 14:13 init.scope
-rw-r--r--  1 root root 0 Sep 29 14:20 io.cost.model
-rw-r--r--  1 root root 0 Sep 29 14:20 io.cost.qos
-rw-r--r--  1 root root 0 Sep 29 14:20 io.pressure
-r--r--r--  1 root root 0 Sep 29 14:20 io.stat
-r--r--r--  1 root root 0 Sep 29 14:20 memory.numa_stat
-rw-r--r--  1 root root 0 Sep 29 14:20 memory.pressure
-r--r--r--  1 root root 0 Sep 29 14:20 memory.stat
drwxr-xr-x 39 root root 0 Sep 29 14:13 system.slice
drwxr-xr-x  3 root root 0 Sep 29 14:13 user.slice
```
新增一個cgroup
```Shell
**~$ mkdir /sys/fs/cgroup/democgv2
~$ ls -l /sys/fs/cgroup/democgv2**
total 0
-r--r--r-- 1 root root 0 Sep 29 14:25 cgroup.controllers
-r--r--r-- 1 root root 0 Sep 29 14:25 cgroup.events
-rw-r--r-- 1 root root 0 Sep 29 14:25 cgroup.freeze
-rw-r--r-- 1 root root 0 Sep 29 14:25 cgroup.max.depth
-rw-r--r-- 1 root root 0 Sep 29 14:25 cgroup.max.descendants
-rw-r--r-- 1 root root 0 Sep 29 14:25 cgroup.procs
-r--r--r-- 1 root root 0 Sep 29 14:25 cgroup.stat
-rw-r--r-- 1 root root 0 Sep 29 14:25 cgroup.subtree_control
-rw-r--r-- 1 root root 0 Sep 29 14:25 cgroup.threads
-rw-r--r-- 1 root root 0 Sep 29 14:25 cgroup.type
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpu.max
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpu.pressure
-r--r--r-- 1 root root 0 Sep 29 14:25 cpu.stat
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpu.uclamp.max
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpu.uclamp.min
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpu.weight
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpu.weight.nice
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpuset.cpus
-r--r--r-- 1 root root 0 Sep 29 14:25 cpuset.cpus.effective
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpuset.cpus.partition
-rw-r--r-- 1 root root 0 Sep 29 14:25 cpuset.mems
-r--r--r-- 1 root root 0 Sep 29 14:25 cpuset.mems.effective
-rw-r--r-- 1 root root 0 Sep 29 14:25 io.max
-rw-r--r-- 1 root root 0 Sep 29 14:25 io.pressure
-r--r--r-- 1 root root 0 Sep 29 14:25 io.stat
-rw-r--r-- 1 root root 0 Sep 29 14:25 io.weight
-r--r--r-- 1 root root 0 Sep 29 14:25 memory.current
-r--r--r-- 1 root root 0 Sep 29 14:25 memory.events
-r--r--r-- 1 root root 0 Sep 29 14:25 memory.events.local
-rw-r--r-- 1 root root 0 Sep 29 14:25 memory.high
-rw-r--r-- 1 root root 0 Sep 29 14:25 memory.low
-rw-r--r-- 1 root root 0 Sep 29 14:25 memory.max
-rw-r--r-- 1 root root 0 Sep 29 14:25 memory.min
-r--r--r-- 1 root root 0 Sep 29 14:25 memory.numa_stat
-rw-r--r-- 1 root root 0 Sep 29 14:25 memory.oom.group
-rw-r--r-- 1 root root 0 Sep 29 14:25 memory.pressure
-r--r--r-- 1 root root 0 Sep 29 14:25 memory.stat
-r--r--r-- 1 root root 0 Sep 29 14:25 memory.swap.current
-r--r--r-- 1 root root 0 Sep 29 14:25 memory.swap.events
-rw-r--r-- 1 root root 0 Sep 29 14:25 memory.swap.high
-rw-r--r-- 1 root root 0 Sep 29 14:25 memory.swap.max
-r--r--r-- 1 root root 0 Sep 29 14:25 pids.current
-r--r--r-- 1 root root 0 Sep 29 14:25 pids.events
-rw-r--r-- 1 root root 0 Sep 29 14:25 pids.max
```
利用修改cgroup.controllers來設定cgroup 可以使用哪一些 Subsystem
```Shell
**~$ cat /sys/fs/cgroup/cgroup.controllers**
cpuset cpu io memory hugetlb pids rdma
``` 
reference: <https://medium.com/starbugs/第一千零一篇的-cgroups-介紹-a1c5005be88c>
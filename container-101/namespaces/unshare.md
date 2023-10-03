
input by normal user
```
unshare --user --map-root-user --pid --mount --fork 
```

```
ls -l /proc/1/ns
```

```
total 0
lrwxrwxrwx 1 root root 0 Oct  3 17:50 cgroup -> 'cgroup:[4026532388]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 ipc -> 'ipc:[4026532305]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 mnt -> 'mnt:[4026532479]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 net -> 'net:[4026532308]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 pid -> 'pid:[4026532480]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 pid_for_children -> 'pid:[4026532480]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 time -> 'time:[4026531834]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 time_for_children -> 'time:[4026531834]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 user -> 'user:[4026532478]'
lrwxrwxrwx 1 root root 0 Oct  3 17:50 uts -> 'uts:[4026532304]'
```

```
$ ls -l /proc/2930/ns/
total 0
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:50 cgroup -> 'cgroup:[4026532388]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:50 ipc -> 'ipc:[4026532305]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:50 mnt -> 'mnt:[4026532479]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:50 net -> 'net:[4026532308]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:50 pid -> 'pid:[4026532306]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:51 pid_for_children -> 'pid:[4026532480]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:50 time -> 'time:[4026531834]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:51 time_for_children -> 'time:[4026531834]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:50 user -> 'user:[4026532478]'
lrwxrwxrwx 1 shawn111 shawn111 0 Oct  3 17:50 uts -> 'uts:[4026532304]'
```
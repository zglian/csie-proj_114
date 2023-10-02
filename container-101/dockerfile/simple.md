```
FROM alpine
RUN apk add --no-cache wget
```

```
ubuntu $ podman build . 
STEP 1/2: FROM alpine
STEP 2/2: RUN apk add --no-cache wget
fetch https://dl-cdn.alpinelinux.org/alpine/v3.18/main/x86_64/APKINDEX.tar.gz
fetch https://dl-cdn.alpinelinux.org/alpine/v3.18/community/x86_64/APKINDEX.tar.gz
(1/4) Installing libunistring (1.1-r1)
(2/4) Installing libidn2 (2.3.4-r1)
(3/4) Installing pcre2 (10.42-r1)
(4/4) Installing wget (1.21.4-r0)
Executing busybox-1.36.1-r2.trigger
OK: 10 MiB in 19 packages
COMMIT
--> c39c2e72a4f
c39c2e72a4f3d521d6b03899d2e5c6c665a1facf6f98c7d680658b76b4c4b7f4
```
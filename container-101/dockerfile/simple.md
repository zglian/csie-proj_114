## 一個簡單的 Dockerfile 範例

這個 Dockerfile 用於建立一個基於 Alpine Linux 的容器映像。以下是它的主要步驟：

1. 使用基礎映像 (base image) alpine，這是一個輕量級的 Linux 發行版。
2. 使用 RUN 指令在容器 (container) 中運行命令 `apk add --no-cache wget`。這個命令的作用是在容器中安裝 wget 工具，--no-cache 選項表示不保留安裝的快取文件，以減小容器映像的大小。

```Dockerfile
FROM alpine
RUN apk add --no-cache wget
```

## Podman build

`podman build .` 是一個用於使用 Podman 工具建立容器映像的命令。這個命令的作用是基於當前目錄中的 Dockerfile 建立一個容器映像。

具體步驟如下：

1. 基於當前目錄中的 Dockerfile 定義，Podman 將建立一個新的容器映像。

2. Podman 將執行 Dockerfile 中定義的每個步驟，例如安裝軟體、複製文件、設置環境變數等。

3. 完成後，你將得到一個新的 image，可以使用 `podman run` 命令運行它，創建容器並運行應用程序。

範例：

```Shell
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

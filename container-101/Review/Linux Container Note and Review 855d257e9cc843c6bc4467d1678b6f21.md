# Linux Container Note and Review

- Docker
    
    ```powershell
    #查詢官方映像檔案
    $ docker search keyword
    #eg. docker serach ubuntu
    
    #查看已有的映像檔
    $ docker images
    
    #取得映像檔
    $ docker pull image_name
    
    #刪除映像檔
    $ deocker rmi image_name
    ```
    
    [Docker (一) : 介紹與安裝](https://lufor129.medium.com/docker-介紹與安裝-5b9183409ce3)
    
    [Docker (二) : 基本操作Image&Container](https://lufor129.medium.com/docker-二-基本操作image-container-1bddaee3fa2)
    
    [Docker (三) : 基本操作Volume & Net](https://lufor129.medium.com/docker-三-基本操作volume-net-5f323965486)
    
- From docker to podman
    
    ![Untitled](Linux%20Container%20Note%20and%20Review%20855d257e9cc843c6bc4467d1678b6f21/Untitled.png)
    
    1. Kubelet 透過CRI 介面（gRPC）呼叫dockershim，請求建立一個容器。CRI 即容器執行時間介面（Container Runtime Interface），在這一步驟中，Kubelet 可以視為一個簡單的CRI Client，而dockershim 就是接收請求的Server。目前dockershim 的程式碼其實是內嵌在Kubelet 中的，所以接收呼叫的湊巧就是Kubelet 進程；
    2. dockershim 收到請求後，轉換成Docker Daemon 能聽懂的請求，發到Docker Daemon 上請求建立一個容器。
    3. 因此Docker Daemon 仍然不能幫我們創建容器，而是要請求containerd 創建一個容器
    4. containerd 收到請求後，並不會自己直接去操作容器，而是創建一個叫做containerd-shim 的進程，讓containerd-shim 去操作容器。這是因為容器程序需要一個父進程來做諸如收集狀態，維持stdin 等fd 開啟等工作。而假如這個父進程就是containerd，那每次containerd 掛掉或升級，整個宿主機上所有的容器都得退出了。而引入了containerd-shim 就規避了這個問題（containerd 和shim 並不是父子進程關係）
    5. 我們知道創建容器需要做一些設定namespaces 和cgroups，掛載root filesystem 等等操作，而這些事該怎麼做已經有了公開的規範了，那就是OCI（Open Container Initiative，開放容器標準）。它的一個參考實作叫做runC。於是，containerd-shim 在這一步驟需要呼叫runC 這個命令列工具，來啟動容器
    6. runC 啟動完容器後本身會直接退出，containerd-shim 則會成為容器進程的父進程，負責收集容器進程的狀態，上報給containerd，並在容器中pid 為1 的進程退出後接管容器中的子進程進行清理，確保不會出現殭屍行程。
    
    **runc 希望提供一個“ OCI 套件”，它只是一個根檔案系統和一個config.json 檔案。**
    
    ![Untitled](Linux%20Container%20Note%20and%20Review%20855d257e9cc843c6bc4467d1678b6f21/Untitled%201.png)
    
    本質上是想要去掉docker，把中間的組合在一起
    
- Podman
    1. docker 得要使用 root 的身份去管理，所以所有的容器都是 root 的權限！對於某些人來說，實在不太喜歡。 podman 可以在一般帳號身份來管理容器！而且也能夠管理由 docker 所建立的映像檔與容器
    2. 基本指令與docker大致上相同
    
    ```bash
    #啟動container
    $ podman run
    #執行container內的指令
    $ podman exec
    #ps 或者是加上 -a 的參數，都可以看到運作中或者是全部的 podman container
    $ podman ps
    ```
    
    [專題 - 使用 podman 進行 container 管理](https://dic.vbird.tw/network_project/zunit12.php)
    
    1. `save` will fetch an image
        
        `export` will fetch the whole container
        
- Container registry
    
    [Docker run reference](https://docs.docker.com/engine/reference/run/)
    
    ```powershell
    $ docker search docker.io/library/alpine:latest
    
    NAME                                DESCRIPTION                                      STARS     OFFICIAL   AUTOMATED
    d3fk/s3cmd                          A simple s3cmd S3 client installed on the Al…   15
    ryanburketllc/foggycam-alpine       foggycam w/ alpine:latest including python3,…   0
    intrepidde/rpi-phpmyadmin           Image based on arm32v6/alpine:latest with ph…   0
    3x3cut0r/alpine                     official alpine:latest base-image with gosu,…   1
    freke/docker_alpine_doxygen         Docker image built on alpine:latest includin…   0                    [OK]
    playniuniu/ikev2-vpn                IKEv2 vpn based on alpine:latest and strongs…   1                    [OK]
    acrelle/rpi-eggdrop                 Raspberry pi build of eggdrop based on arm32…   0
    opillion/node                       based on: alpine:latest                          0
    sisnet/alpine-curl                  Builds a docker image from alpine:latest add…   0                    [OK]
    idef1x/docker-owncloud-client       headless nextcloud-client on Alpine:latest       4                    [OK]
    artemklevtsov/r-alpine               R docker images based on the alpine:latest      3                    [OK]
    ywatase/ansible                     ansible on alpine:latest                         0                    [OK]
    fixiu/jdk-alpine                    alpine:latest  oracle jdk 8u211                  1
    mkoppanen/etcdtool                  Image based on alpine:latest to run etcdtool     0
    bmauter/alpine-samba-client         alpine:latest + samba-client                     0
    robonuka/sslh                       Alpine:latest + SSLH v1.2.0                      0
    soff/alpine                         alpine:latest with mirror aliyun.com             0
    mheindl/alpine-aws                  Just a simple Image based on alpine:latest c…   1                    [OK]
    gymnae/alpine-base                  A pico base image suited for my needs based …   0                    [OK]
    gymnae/webserverbase                Web server image with alpine:latest origin -…   0                    [OK]
    paulgoio/toolkit                    alpine:latest image with curl, bash, openssh…   0
    robonuka/socks                      Alpine:latest + Dante 1.4.2 Socks5 server        0
    biosniper/jackett                   Docker build of Jackett using alpine:latest      0                    [OK]
    neverlock/alpine-wrk                wrk build on alpine:latest                       0                    [OK]
    lazaruslongone/alpine-openrc-base   A simple container that uses alpine:latest a…   0                    [OK]
    ```
    
    ```powershell
    $ docker pull alpine:latest
    
    latest: Pulling from library/alpine
    Digest: sha256:eece025e432126ce23f223450a0326fbebde39cdf496a85d8c016293fc851978
    Status: Image is up to date for alpine:latest
    docker.io/library/alpine:latest
    ```
    
    ```powershell
    $ docker imgaes
    #注意:pull 下來是一個image，不能用docker ps -a(這是察看container)
    
    REPOSITORY                 TAG       IMAGE ID       CREATED        SIZE
    httpd                      2.4       75a48b16cd56   3 days ago     168MB
    alpine                     latest    8ca4688f4f35   3 weeks ago    7.34MB
    docker/welcome-to-docker   latest    912b66cfd46e   4 months ago   13.4MB
    postgres                   latest    ceccf204404e   6 months ago   379MB
    ```
    
    ```powershell
    $ docker image inspect alpine
    
    [
        {
            "Id": "sha256:8ca4688f4f356596b5ae539337c9941abc78eda10021d35cbc52659c74d9b443",
            "RepoTags": [
                "alpine:latest"
            ],
            "RepoDigests": [
                "alpine@sha256:eece025e432126ce23f223450a0326fbebde39cdf496a85d8c016293fc851978"
            ],
            "Parent": "",
            "Comment": "",
            "Created": "2023-09-28T21:19:27.801479409Z",
            "Container": "6fd75b3ad2cde1fb91e80db8f58701b0d6710f1b88c383492c28612918d81549",
            "ContainerConfig": {
                "Hostname": "6fd75b3ad2cd",
                "Domainname": "",
                "User": "",
                "AttachStdin": false,
                "AttachStdout": false,
                "AttachStderr": false,
                "Tty": false,
                "OpenStdin": false,
                "StdinOnce": false,
                "Env": [
                    "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
                ],
                "Cmd": [
                    "/bin/sh",
                    "-c",
                    "#(nop) ",
                    "CMD [\"/bin/sh\"]"
                ],
                "Image": "sha256:6913aeba049e6e1fb16d610436f78c039eec4a06bce4bfaffa43ae89fcf67942",
                "Volumes": null,
                "WorkingDir": "",
                "Entrypoint": null,
                "OnBuild": null,
                "Labels": {}
            },
            "DockerVersion": "20.10.23",
            "Author": "",
            "Config": {
                "Hostname": "",
                "Domainname": "",
                "User": "",
                "AttachStdin": false,
                "AttachStdout": false,
                "AttachStderr": false,
                "Tty": false,
                "OpenStdin": false,
                "StdinOnce": false,
                "Env": [
                    "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
                ],
                "Cmd": [
                    "/bin/sh"
                ],
                "Image": "sha256:6913aeba049e6e1fb16d610436f78c039eec4a06bce4bfaffa43ae89fcf67942",
                "Volumes": null,
                "WorkingDir": "",
                "Entrypoint": null,
                "OnBuild": null,
                "Labels": null
            },
            "Architecture": "amd64",
            "Os": "linux",
            "Size": 7335363,
            "VirtualSize": 7335363,
            "GraphDriver": {
                "Data": {
                    "MergedDir": "/var/lib/docker/overlay2/3e418f95c53d1308abe5b8d02b057641bf8a0db363d1417fe9494b3b1f848dae/merged",
                    "UpperDir": "/var/lib/docker/overlay2/3e418f95c53d1308abe5b8d02b057641bf8a0db363d1417fe9494b3b1f848dae/diff",
                    "WorkDir": "/var/lib/docker/overlay2/3e418f95c53d1308abe5b8d02b057641bf8a0db363d1417fe9494b3b1f848dae/work"
                },
                "Name": "overlay2"
            },
            "RootFS": {
                "Type": "layers",
                "Layers": [
                    "sha256:cc2447e1835a40530975ab80bb1f872fbab0f2a0faecf2ab16fbbb89b3589438"
                ]
            },
            "Metadata": {
                "LastTagTime": "0001-01-01T00:00:00Z"
            }
        }
    ]
    ```
    
- Dockerfile
    
    ```docker
    FROM centos:7    
    MAINTAINER Neil
    
    RUN yum install -y wget
    
    RUN cd /
    
    ADD jdk-12.0.2_linux-x64_bin.tar.gz /
    
    RUN wget http://apache.stu.edu.tw/tomcat/tomcat-7/v7.0.94/bin/apache-tomcat-7.0.94.tar.gz
    RUN tar zxvf apache-tomcat-7.0.94.tar.gz
    
    ENV JAVA_HOME=/jdk-12.0.2
    ENV PATH=$PATH:/jdk-12.0.2/bin
    
    CMD ["/apache-tomcat-7.0.94/bin/catalina.sh", "run"]
    
    #FROM： 使用到的 Docker Image 名稱，今天使用 CentOS
    #MAINTAINER： 用來說明，撰寫和維護這個 Dockerfile 的人是誰，也可以給 E-mail的資訊
    #RUN： RUN 指令後面放 Linux 指令，用來執行安裝和設定這個 Image 需要的東西
    #ADD： 把 Local 的檔案(要與Dockerfile同目錄) 複製到 Image 裡，如果是 tar.gz 檔複製進去 Image 時會順便自動解壓縮。Dockerfile 另外還有一個複製檔案的指令 COPY 未來還會再介紹
    #ENV： 用來設定環境變數
    #CMD： 在指行 docker run 的指令時會直接呼叫開啟 Tomcat Service
    #ARG : 在build時候是可以從外部以--build-arg帶入的變數，讓build的動作可結合外部的指令給定一些建構時候所需的參數
    #EXPOSE: The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if the protocol is not specified.
    ```
    
    [Docker 範例 - HackMD](https://hackmd.io/@karta134033/BJJS6RmfH)
    
    [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
    
- Docker-compose
    1. 實務上一個服務，一定由眾多 service 共同運作若只使用 `docker run`，則勢必寫 Bash 來管理 4 個 service，還必須考慮：
        - 4 個 service 必須在同一個虛擬 network 下
        - 4 個 service 的啟動順序… 等問題
        
        Docker 為此提出 Docker Compose 概念，在 `docker-compose.yml` 檔描述各 service 間的參數與關係
        
    
    eg.
    
    ```yaml
    version: "3"
    
    services:
      netcore:
        image: microsoft/dotnet
        container_name: MyNETCore
        volumes:
          - ${NETCORE_HOST_DIR}:/code/
        tty: true
        networks: 
          - netcore-dev
        depends_on:
          - postgres
    
      postgres:
        image: postgres
        container_name: MyPostgres
        volumes:
          - ${POSTGRES_HOST_DIR}/data:/var/lib/postgresql/data
        expose:
          - "5432"
        ports:
          - "${POSTGRES_PORT}:5432"
        environment:
          - POSTGRES_DB=${POSTGRES_DB}
          - POSTGRES_USER=${POSTGRES_USER}
          - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
        networks:
          - netcore-dev
    
    networks:
      netcore-dev:
    ```
    
    [深入淺出 Dockerfile 與 Docker Compose](https://old-oomusou.goodjack.tw/docker/dockerfile-dockercompose/)
    
    1. dockerfile VS. docker-compose
        - `Dockerfile` 是用來描述 image，也就是如何產生客製化的 image，通常用來安裝 package，將檔案複製進 image 用
        - `docker-compose.yml` 是用來描述 container，也就是管理一個以上的 container，彼此串連，把同一組架構寫在一起，通常用來設定 container 參數，設定 container 的網路，設定 container 啟動順序或 service 的環境變數 … 等
    
    `services` 提供哪些的服務
    
    `volumes` 絕對路徑
    
    `ports` 在哪個port提供服務
    
- Before docker
    1. `chroot` (change root)
        
        ![Untitled](Linux%20Container%20Note%20and%20Review%20855d257e9cc843c6bc4467d1678b6f21/Untitled%202.png)
        
    2. `schroot`(secure chroot)
        
        is an enhancement and management tool for the **`chroot`**
        
    3. `fakeroot`
        
        simulates the effect of running a command with superuser (root) privileges without actually requiring root access
        
- container == isolated linux process
    1. `namespace` 
        
        Namespace 其中一個應用是「隔離」同一個作業系統上的不同行程。把一個行程放在某一個種類的 namespace 中，它就會只看得到該 namespace 下看得到的資源。儘管處在該 namespace 中的行程可能以為自己可以存取整個根目錄、以為自己是它 root，但在 namespace 以外的行程看來只是一個普通權限的行程。而這也是容器 (container) 的基礎。
        
        [系統程式設計 - Namespaces - HackMD](https://hackmd.io/@0xff07/r1wCFz0ut)
        
    2. `cgroup`(Control Groups)
        
        cgroups 主要提供有底下四個功能：
        
        - **Resource Limiting**: Group 可以設定 Memory 的使用上限，其中也包含 File System 的 Cache
        - **Prioritization**: 不同的 Group 可以擁有不同的 CPU 跟 Disk I/O 使用優先順序
        - **Accounting**: 計算 Group 內的資源使用狀況，例如可以拿來當作計費的依據
        - **Control**:凍結或是重啟一整個 Group 的 Process
        
        [第一千零一篇的 cgroups 介紹](https://medium.com/starbugs/第一千零一篇的-cgroups-介紹-a1c5005be88c)
        
    3. `pod`
        
        Pod 是在 k8s 最基本的組成單位(也是最小的可佈署單位)，實際在 k8s 上運行的很多 resource object 都是以 pod 型式存在，它封裝了許多不同的資源，也因此每個 pod 都有以下特性：
        
        - 包含一到多個 container
        - 同一個 pod 都 container 都共享相同的檔案系統 & volume … 等資源
        - container 共享相同的 network namespace(container 之間可以透過 `localhost` + `port number` 互相通訊)，且有獨一無二的 IP address
        - container 之間也可以透過進程間通信，例如：SystemV or POSIX shared memory
        - container 共享 pod 中的 volume resource
        - pod 中的 container 總是被同時調度 & 有共同的運行環境
        
        [Pods](https://kubernetes.io/docs/concepts/workloads/pods/)
        
        [[Kubernetes] Pod 的設計 & 相關運作機制](https://godleon.github.io/blog/Kubernetes/k8s-Pod-Overview/)
        
- Container specs
    1. OCI定義了容器運行時標準，runC是Docker按照開放容器格式標準（OCF， Open Container Format）制定的一種具體實現
    2. OCI runtime spec
        
        OCI 對容器 runtime 的標準主要是指定容器的運行狀態，和 runtime 需要提供的命令
        
        ![Untitled](Linux%20Container%20Note%20and%20Review%20855d257e9cc843c6bc4467d1678b6f21/Untitled%203.png)
        
        - creating：使用 命令創建容器，這個過程稱為創建中`create`
        - created：容器創建出來，但是還沒有運行，表示鏡像和配置沒有錯誤，容器能夠運行在當前平臺
        - running：容器的運行狀態，裡面的進程處於 up 狀態，正在執行使用者設定的任務
        - stopped：容器運行完成，或者運行出錯，或者 命令之後，容器處於暫停狀態。 這個狀態，容器還有很多資訊保存在平臺中，並沒有完全被刪除`stop`
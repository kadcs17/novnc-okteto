# novnc-okteto

https://cloud.okteto.com/deploy?repository=https://github.com/valetzx/novnc-okteto

在okteto上部署ubuntu并使用novnc连接，如果有okteto账号的话点一下上面的链接就能自动部署

`docker-compose.yml`中可以修改的参数有：

```yml
services:
    ubuntu: #服务名字
        public: true #是否公开，没试过否
        container_name: valetzx #容器名字
        image: imlala/ubuntu-xfce-vnc-novnc:latest
        shm_size: "3gb"
        ports: 
            - 6080:6080
        environment: 
            - VNC_PASSWD=passwd #你的密码
            - GEOMETRY=1080x720 #vnc分辨率
            - TZ=Asia/Shanghai #时区
            - DEPTH=24 #像素深度？最好别改
        volumes: #挂载目录/home会保留
            - /root/Desktop 
            - /home
        resources:
          cpu: 1000m #1核是Free上限
          memory: 3072Mi #3G是Free上限
          storage:
            size: 4Gi #5G是Free上限
            class: standard
```

部署完成后，会在 Endpoints: 中出现ws链接，点进去使用`- VNC_PASSWD=passwd #你的密码`登录即可

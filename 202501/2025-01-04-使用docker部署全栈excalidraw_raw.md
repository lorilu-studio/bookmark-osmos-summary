Title: 使用Docker部署全栈Excalidraw

URL Source: https://www.jamesflare.com/zh-cn/excalidraw-full-stack-docker/

Published Time: 2023-01-13T15:54:36+08:00

Markdown Content:
FlareBlog
 归档
 关于
Docker Compose
4
修正因 Queue 导致的 Flarum 的邮件无法发送问题
使用Docker Compose部署LobeChat服务端数据库版本
将Docker部署的Umami从一台服务器迁移到另一台服务器
使用Docker部署全栈Excalidraw
4/4
使用Docker部署全栈Excalidraw
 James 收录于  教程  资源分享 和  Docker Compose
2023-01-13 2024-03-11 约 1000 字 预计阅读 2 分钟 
警告
本文最后更新于 2024-03-11，文中内容可能已过时。
Intro

这可能是中文互联网上唯一一篇讲如何全栈部署 Excalidraw 的，绝大多数只是部署了一个残血的前端。

本人试图在本地私有化部署 Excalidraw，操作是很简单，根据官方的 README，一会就完成了是吧。

Issue

但是有没有发现，分享链接和在线协作有问题，用不了？甚至 Libraries 还有点问题？

这是因为，几乎全网的搭建教程都只是搭建了 excalidraw-app 这个前端，它的存储需要 excalidraw-json，协作需要 excalidraw-room。

这些代码官方都开源了，不过前端的进度实在是太快了，于是乎这些就都用不了了。

比如官方开放的 excalidraw-json 是 S3 的存储，现在不出意外是 firebase，官方也没出个剥离的版本，那我们怎么办呢？

Solution

答，降级，构建全栈。

excalidraw-app 我们用官方的，不过版本差不多是 9 个月前的，讲道理，功能也没少多少，bug 也没什么问题，这一代前端可以很好兼容。

excalidraw-json 是用不得了，国外也有一些方案用 minio 来跑 S3 对接它，但是我测试了，问题有些大，这个后端应该是用不得了，所幸的是，我找到了一个第三方，用自己代码实现的全功能后端，支持 v2 的 api，excalidraw-storage-backend。

excalidraw-room 我们用官方的，最新一版，差不多是 9 个月前的，和前端一致，可以正常使用。

redis，这个是 excalidraw-storage-backend 所需要的，用于临时存储分享画板的数据，所以它不能保证数据可靠性。

那我们开始吧，本方案使用 docker-compose。

excalidraw-app
excalidraw-room
excalidraw-storage-backend
redis
Docker Compose

Docker Compose 配置

 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34

	
version: "3.8"

services:
  excalidraw:
    image: kiliandeca/excalidraw
    healthcheck:
      disable: true
    ports:
      - "80:80" # 默认端口80，可以修改
    environment:
      BACKEND_V2_GET_URL: http://localhost:8080/api/v2/scenes/
      BACKEND_V2_POST_URL: http://localhost:8080/api/v2/scenes/
      LIBRARY_URL: https://libraries.excalidraw.com
      LIBRARY_BACKEND: https://us-central1-excalidraw-room-persistence.cloudfunctions.net/libraries
      SOCKET_SERVER_URL: http://localhost:5000/
      STORAGE_BACKEND: "http"
      HTTP_STORAGE_BACKEND_URL: "http://localhost:8080/api/v2"

  excalidraw-storage-backend:
    image: kiliandeca/excalidraw-storage-backend
    ports:
      - "8080:8080"
    environment:
      STORAGE_URI: redis://redis:6379

  excalidraw-room:
    image: excalidraw/excalidraw-room
    ports:
      - "5000:80"

  redis:
    image: redis
    ports:
      - "6379:6379"

本身不支持 https，如有需要可以通过反向代理实现，不过记得同时修改 environment 中的变量

此配置文件经本地测试通过，可完美运行。

如果你 6379 端口有冲突，那可以选择构建一个 network

1

	
docker network create excalidraw-net

然后像这样对其进行一些修改，就完成了

 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39

	
version: "3.8"

services:
  excalidraw:
    image: kiliandeca/excalidraw
    healthcheck:
      disable: true
    ports:
      - "80:80"
    environment:
      BACKEND_V2_GET_URL: http://localhost:8080/api/v2/scenes/
      BACKEND_V2_POST_URL: http://localhost:8080/api/v2/scenes/
      LIBRARY_URL: https://libraries.excalidraw.com
      LIBRARY_BACKEND: https://us-central1-excalidraw-room-persistence.cloudfunctions.net/libraries
      SOCKET_SERVER_URL: http://localhost:5000/
      STORAGE_BACKEND: "http"
      HTTP_STORAGE_BACKEND_URL: "http://localhost:8080/api/v2"

  excalidraw-storage-backend:
    image: kiliandeca/excalidraw-storage-backend
    ports:
      - "8080:8080"
    environment:
      STORAGE_URI: redis://redis:6379

  excalidraw-room:
    image: excalidraw/excalidraw-room
    ports:
      - "5000:80"

  redis:
    image: redis
    expose:
      - "6379"

networks:
  default:
    external:
      name: excalidraw-net
Run

找一个，或者新建一个目录，创建 docker-compose 文件。

1

	
nano docker-compose.yml

填入 docker-compose 配置，记得按你的实际情况修改。

随后我们要配置一下反向代理，记得配置 WebSocket 支持，我这里就跳过了。

思路是这样的，参考下面配置即可：

Stack
收录于  合集・Docker Compose 4
将Docker部署的Umami从一台服务器迁移到另一台服务器
更新于 2024-03-11 
阅读原始文档
  
Excalidraw开源软件Docker
返回 | 主页
For 杨文雅 - 祝你学业顺利
由 Hugo 强力驱动 | 主题 - FixIt
 2024 JamesCC BY-NC 4.0

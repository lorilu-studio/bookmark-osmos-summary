Title: 【Outline】纯Docker部署指南

URL Source: https://biteax.com/b9dce220.html

Published Time: 2022-05-07T09:58:53.000Z

Markdown Content:
此网站使用Cookie来改善您的体验。 了解更多
知道了！
主页
归档
分类
标签
工具
3 年前
发表
1 年前
更新
OUTLINE
18 分钟读完 (大约2726个字)
1412次访问
【Outline】纯Docker部署指南

找了好久，总算中意了一个，好看又好用，开源不要钱，赶紧部署一个试试。

因为用的是 UnRaid 系统，这里直接使用纯 Docker 的方式进行部署。

Outline依赖 PostgreSQL (v9.5+)、Redis (v4+)、Minio, S3, or S3 兼容对象存储服务

还要另外配置一个登录授权的服务器，这里我采用的是自建的服务器

这个部署起来还真是麻烦，不过用起来是很舒服了，有种 Typora 的在线版的感觉

安装 Docker

部署 postgres 12

1
2
3
4
5
6
7
8

	
docker run -d \
    --name postgres_12 \
    --restart=always \
    -e POSTGRES_PASSWORD=mysecretpassword \
    -e PGDATA=/var/lib/postgresql/data/pgdata \
    -v postgres_12:/var/lib/postgresql/data \
    -p 5432:5432 \
    postgres:12.10


创建用户和数据库

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

	
# 进入数据库命令行
docker exec -it --user postgres postgres_12 psql -U postgres

# 创建用户
CREATE USER outline WITH PASSWORD '123456';

# 创建数据库
CREATE DATABASE outline OWNER outline;
CREATE DATABASE outline_test OWNER outline;

# 退出
\q


部署 Redis

1
2
3
4
5

	
docker run -d \
    --name redis_6 \
    --restart=always \
    -p 6379:6379 \
    redis:6.2.7


部署 minio，用来代替 AWS S3

参考

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

	
# 创建容器
docker run -d \
    --name minio \
    --restart=always \
    -p 9000:9000 \
    -p 9001:9001 \
    -e MINIO_ROOT_USER="6m2lx2ffmbr9ikod" \
    -e MINIO_ROOT_PASSWORD="2k78fpraq7rs5xlrti5p6cvb767a691h3jqi47ihbu75cx23twkzpok86sf1aw1e" \
    -e MINIO_REGION_NAME="cn-homelab-1" \
    -e MINIO_BROWSER="on" \
    -e MINIO_SERVER_URL="http://192.168.100.155:9000/" \
    -e MINIO_BROWSER_REDIRECT_URL="http://192.168.100.155:9001/" \
    --volume minio:/data \
    minio/minio:RELEASE.2021-09-03T03-56-13Z server /data --console-address ":9001"


MINIO_ROOT_USER 使用小写字母加数字长度为16位的随机数

MINIO_ROOT_PASSWORD 使用小写字母加数字长度为64位的随机数

MINIO_SERVER_URL 是API地址，反向代理请务必开启 proxy_pass，否则会无法连接，导致附件及图片无法上传

比如说使用了 Nginx Proxy Manager，就要在代理的高级选项中加入以下字段（IP需要使用自己的）

1
2
3
4
5
6
7

	
location / {
    proxy_pass              http://192.168.100.155:9000;
    proxy_set_header        Host            $http_host;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        X-Scheme        $scheme;
    proxy_set_header        X-Script-Name   /;
}


MINIO_BROWSER_REDIRECT_URL 是管理地址，即反代后的地址比如 https://file-admin.lab.com/，不反代就老老实实用原始访问的地址

这边还需要访问这个页面，创建一个新的 Buckets，名称为 outline，不创建的话到时候上传不了图片，也导出不了文件

搭建 OIDC 服务器（sso-server），用于代替 slack 或 google 登录

项目地址

1
2
3
4
5
6
7
8

	
docker run -d \
    --name=sso-server \
    -e CLIENT_NAME="My SSO Service" \
    -e CLIENT_ID="b8c40013-cc03-4bc5-b3a5-6a31046fa415" \
    -e CLIENT_SECRET="26272010-37d9-4bea-a58e-6b0a382d7626" \
    -e USER_PASS="password" \
    -p 3000:80 \
    soulteary/sso-server:1.1.5


CLIENT_NAME 是随机的

CLIENT_ID 是随机的，格式如上面所示

CLIENT_SECRET 是随机的，格式如上面所示

USER_PASS 是默认的密码

启动后就可以有一个挺好看的登录页可访问：http://localhost:3000/login

默认的用户名是 username，密码是 USER_PASS 字段所设置的

先拉取一下 outline

1

	
docker pull outlinewiki/outline:0.63.0


编辑一个 .env 的本地文件

参考 .env.sample

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
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100
101
102
103
104
105
106
107
108
109
110
111
112
113
114
115
116
117
118
119
120
121
122
123
124
125
126
127
128
129
130
131
132
133
134
135
136
137
138
139
140
141
142
143
144
145
146
147
148
149
150
151
152
153
154
155
156
157
158
159
160
161
162
163
164
165
166
167
168
169
170
171
172

	
# –––––––––––––––– REQUIRED ––––––––––––––––

# 生成一个十六进制编码的 32 字节随机密钥。你应该使用`openssl rand -hex 32`
# 在你的终端中生成一个随机值。
SECRET_KEY=6697a4fc3c47d879f42d73e4ed00cda076c79e845257acfab8661b2241532ea7

# 生成唯一的随机密钥。格式并不重要，您仍然可以使用 `openssl rand -hex 32` 
# 在你的终端中生成。
UTILS_SECRET=9fb6973a0e562ca592999436c2f5ed4326a81e2fdff8c996b27cb58b5abff79a

# 对于生产点这些在您的数据库中，在开发中默认应该开箱即用。
# 这里的 postgres_12 是上面创建的数据库容器的默认 Hostname，需要建立单独的网络或使用 --link
# outline:123456 是上面创建的数据库账户
DATABASE_URL=postgres://outline:123456@postgres_12:5432/outline
DATABASE_URL_TEST=postgres://outline:123456@postgres_12:5432/outline_test
DATABASE_CONNECTION_POOL_MIN=
DATABASE_CONNECTION_POOL_MAX=
# 取消注释以禁用 SSL 连接到 Postgres
PGSSLMODE=disable

# 对于 redis，你可以像这样指定一个 ioredis 兼容的 url
# 这里的 redis_6 是上面创建的数据库容器的默认 Hostname，需要建立单独的网络或使用 --link
REDIS_URL=redis://redis_6:6379
# 或者，如果您想提供额外的连接选项，
# 使用 base64 编码的 JSON 连接选项对象。参考 ioredis 文档获取可用选项的列表。
# 示例：使用 Redis Sentinel 实现高可用性
# {"sentinels":[{"host":"sentinel-0","port":26379},{"host":"sentinel-1","port":26379}],"name":"mymaster"}
# REDIS_URL=ioredis://eyJzZW50aW5lbHMiOlt7Imhvc3QiOiJzZW50aW5lbC0wIiwicG9ydCI6MjYzNzl9LHsiaG9zdCI6InNlbnRpbmVsLTEiLCJwb3J0IjoyNjM3OX1dLCJuYW1lIjoibXltYXN0ZXIifQ==

# URL 应指向完全限定的、可公开访问的 URL。
# 如果使用代理 URL 和 PORT 中的端口可能不同。
# 简单的说就是第一个是反代后访问的地址
# PORT 是服务器默认打开的端口，是需要本地开放的端口
URL=http://192.168.100.155:13090
PORT=3000

# 参见 [文档](docs/SERVICES.md) 运行单独的协作服务器，正常操作不需要设置。
COLLABORATION_URL=

# 支持上传头像和文档附件的图片必须提供与 s3 兼容的存储。建议使用 AWS S3 进行冗余
# 但是，如果您想将所有文件存储保持在本地，则可以使用替代方法，例如
# minio (https://github.com/minio/minio) can be used.

# 有关设置 S3 的更详细指南可在此处获得：
# => https://wiki.generaloutline.com/share/125de1cc-9ff6-424b-8415-0d58c809a40f
# AWS_ACCESS_KEY_ID 对应上面的 MINIO_ROOT_USER
# AWS_SECRET_ACCESS_KEY 对应上面的 MINIO_ROOT_PASSWORD
# AWS_REGION 对应上面的 MINIO_REGION_NAME
# AWS_S3_UPLOAD_BUCKET_URL 是 MINIO 的API地址，注意是API地址，不是管理地址 
AWS_ACCESS_KEY_ID=6m2lx2ffmbr9ikod
AWS_SECRET_ACCESS_KEY=2k78fpraq7rs5xlrti5p6cvb767a691h3jqi47ihbu75cx23twkzpok86sf1aw1e
AWS_REGION=cn-homelab-1
AWS_S3_ACCELERATE_URL=
AWS_S3_UPLOAD_BUCKET_URL=http://192.168.100.155:9000
AWS_S3_UPLOAD_BUCKET_NAME=outline
AWS_S3_UPLOAD_MAX_SIZE=26214400
AWS_S3_FORCE_PATH_STYLE=true
AWS_S3_ACL=private


# –––––––––––––– 认证 ––––––––––––––

# 第三方登录凭据，工作安装至少需要Google、Slack或Microsoft中的一个，否则您将没有登录选项。

# 要配置 Slack 身份验证，您需要在
# => https://api.slack.com/apps
#
# 配置Client ID时，在“OAuth & Permissions”下添加重定向URL：
# https://<URL>/auth/slack.callback
SLACK_KEY=
SLACK_SECRET=

# 要配置 Google 身份验证，您需要在以下位置创建 OAuth 客户端 ID
# => https://console.cloud.google.com/apis/credentials
#
# 配置Client ID时，添加Authorized redirect URI：
# https://<URL>/auth/google.callback
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=

# 要配置 Microsoft/Azure 身份验证，您需要创建一个 OAuth 客户端。
# 查看有关设置 Azure 应用程序的详细信息的指南:
# => https://wiki.generaloutline.com/share/dfa77e56-d4d2-4b51-8ff8-84ea6608faa4
AZURE_CLIENT_ID=
AZURE_CLIENT_SECRET=
AZURE_RESOURCE_APP_ID=

# 要配置通用 OIDC 身份验证，您需要某种身份提供者。
# 请参阅文档，了解您用于获取以下信息的任何 IdP：
# 重定向 URI 是 https://<URL>/auth/oidc.callback
# 此处的参数对应上面 OIDC 服务器的配置
# OIDC_CLIENT_ID 对应上面的 OIDC 服务器的 CLIENT_ID
# OIDC_CLIENT_SECRET 对应上面的 OIDC 服务器的 CLIENT_SECRET
# OIDC_AUTH_URI 是上面的 OIDC 服务器的对公网开放的地址
# OIDC_TOKEN_URI 和 OIDC_USERINFO_URI 应该是用 OIDC 服务器的对公网不开放的地址，当然用开放的也能用，不安全，我这里用开放的地址
OIDC_CLIENT_ID=b8c40013-cc03-4bc5-b3a5-6a31046fa415
OIDC_CLIENT_SECRET=26272010-37d9-4bea-a58e-6b0a382d7626
OIDC_AUTH_URI=http://192.168.100.155:3000/dialog/authorize
OIDC_TOKEN_URI=http://192.168.100.155:3000/oauth/token
OIDC_USERINFO_URI=http://192.168.100.155:3000/api/outline/oidc

# 指定要从中派生用户信息的声明支持使用JWT负载的任何有效JSON路径
OIDC_USERNAME_CLAIM=preferred_username

# OIDC 认证的显示名称
OIDC_DISPLAY_NAME=SZC_SSO

# 空格分隔的身份验证范围。
OIDC_SCOPES=openid profile email


# –––––––––––––––– 可选 ––––––––––––––––

# 用于 HTTPS 终止的 Base64 编码私钥和证书。This is only
# required if you do not use an external reverse proxy. See documentation:
# https://wiki.generaloutline.com/share/1c922644-40d8-41fe-98f9-df2b67239d45
SSL_KEY=
SSL_CERT=

# If using a Cloudfront/Cloudflare distribution or similar it can be set below.
# This will cause paths to javascript, stylesheets, and images to be updated to
# the hostname defined in CDN_URL. In your CDN configuration the origin server
# should be set to the same as URL.
CDN_URL=

# 在生产中自动重定向到https。
# 默认值为true，但如果可以确保SSL在外部负载平衡器处终止，则可以将其设置为false。
FORCE_HTTPS=false

# 通过向维护人员发送匿名统计信息，让安装人员检查更新情况
ENABLE_UPDATES=false

# 应该产生多少进程。作为一个合理的规则，将服务器的可用内存除以512进行粗略估计
WEB_CONCURRENCY=1

# 如果有嵌入图像的特别大的Word文档，可能需要覆盖文档导入的最大大小
MAXIMUM_IMPORT_SIZE=5120000

# 如果您的反向代理已经记录了传入的http请求，并且结果是重复的，则可以删除这一行
DEBUG=http

# 允许登录wiki的域的逗号分隔列表。如果未设置，则在使用Google OAuth登录时默认允许所有域
ALLOWED_DOMAINS=

# 为了实现与搜索和发布到渠道的完整集成，还需要以下配置，以及更多详细信息
# => https://wiki.generaloutline.com/share/be25efd1-b3ef-4450-b8e5-c4a4fc11e02a
#
SLACK_VERIFICATION_TOKEN=your_token
SLACK_APP_ID=A0XXXXXXX
SLACK_MESSAGE_ACTIONS=true

# 还可以选择启用google analytics来跟踪知识库中的页面浏览量
GOOGLE_ANALYTICS_ID=

# 可选地启用Sentry（Sentry.io）来跟踪错误和性能
SENTRY_DSN=

# 要支持发送“文档更新”或“您已被邀请”等传出事务性电子邮件，您需要为SMTP服务器提供身份验证
SMTP_HOST=
SMTP_PORT=
SMTP_USERNAME=
SMTP_PASSWORD=
SMTP_FROM_EMAIL=
SMTP_REPLY_EMAIL=
SMTP_TLS_CIPHERS=
SMTP_SECURE=true

# 显示在认证屏幕上的自定义徽标，缩放至高度：60px
# TEAM_LOGO=https://example.com/images/logo.png

# 默认的接口语言。有关可用语言代码及其大致翻译百分比的列表，请参见 translate.getoutline.com 。
DEFAULT_LANGUAGE=zh_CN


请注意：该文件没写完整，补充可以参考

该配置文件适用于版本 0.63.0，新版可能需要重新进行更改

运行前需要先迁移数据库

1
2
3
4
5
6

	
docker run --rm \
    --env-file=.env \
    --link postgres_12 \
    --link redis_6 \
    outlinewiki/outline:0.63.0 \
    yarn db:migrate --env production-ssl-disabled


运行

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

	
docker run -d \
    --restart=always \
    --name=outline \
    --env-file=.env \
    --link postgres_12 \
    --link redis_6 \
    -p 13090:3000 \
    outlinewiki/outline:0.63.0

docker logs outline


访问浏览器 http://192.168.100.155:13090

【Outline】纯Docker部署指南

https://biteax.com/b9dce220.html

作者

石志超

发布于

2022-05-07

更新于

2023-09-27

许可协议

#
Outline
Wiki
喜欢这篇文章？打赏一下作者吧
支付宝
微信
【Rust】WASM 编译使用方法

石志超

　

中国 浙江 杭州

文章

66

分类

34

标签

46

关注我
最新文章

2022-05-07

【Outline】纯Docker部署指南

OUTLINE

2022-05-07

【Rust】WASM 编译使用方法

RUST

2022-05-05

【Zynq】PetaLinux 2019.2使用USB口虚拟化网口

ZYNQ

2022-05-02

【Windows】连接非445端口的SMB服务器

WINDOWS

2022-05-01

【Vue】在Vue2中使用Route

VUE

标签
Allegro
1
Atlassian
1
Cadence
3
Centos7
2
DiyCPU
1
Docker
4
Duktape
1
ESP32
1
ESP8266
1
Electron
1
F1c100s
1
Frp
2
Git
1
Gitlab-CE
1
Hexo
10
JIRA
1
Labview
3
Linux
3
Luat
2
MacOS
1
Micro-XRCE-DDS
2
MicroROS
1
Multisim
4
NextCloud
1
Nginx
1
Nodejs
1
OpenWRT
1
OrCAD
2
Outline
1
Printer
1
Python3
3
ROS2
2
Rust
3
TrueNAS
1
Unraid
1
VS
1
VSCode
3
Vue
2
Web
3
Wiki
1
Windows
5
Zynq
4
git
1
iRTU
2
icarus
4
全志
1
链接
Hexo
hexo.io
Icarus
ppoffice.github.io
Bulma
bulma.io
张羿
luckzym.com

© 2023 石志超  Powered by Hexo & Icarus
共19774个访客

ICP备案号：浙ICP备2021031571号-1

浙公网安备 33042402000517号

# 【Outline】纯Docker部署指南
- URL: https://biteax.com/b9dce220.html
- Added At: 2025-03-20 14:20:55
- [Link To Text](2025-03-20-【outline】纯docker部署指南_raw.md)

## TL;DR
本文详细介绍了如何在UnRaid系统中使用Docker部署开源文档编辑工具Outline。内容包括安装Docker、配置PostgreSQL、Redis、Minio和OIDC服务器，以及Outline的镜像拉取、环境变量设置和运行步骤。适用于Outline 0.63.0版本，新版可能需要调整配置。

## Summary
1. **Outline简介**：Outline是一款开源、免费且功能强大的在线文档编辑工具，类似于Typora的在线版本，适合用于知识管理和团队协作。

2. **部署环境**：
   - **系统要求**：UnRaid系统，使用纯Docker部署。
   - **依赖服务**：
     - PostgreSQL（v9.5+）
     - Redis（v4+）
     - Minio、S3或S3兼容的对象存储服务
     - 自建的OIDC服务器（用于登录授权）

3. **Docker部署步骤**：
   - **安装Docker**：确保Docker已安装并运行。
   - **部署PostgreSQL**：
     - 使用Docker运行PostgreSQL 12，配置密码和数据存储路径。
     - 创建用户和数据库（`outline`和`outline_test`）。
   - **部署Redis**：
     - 使用Docker运行Redis 6，配置端口和自动重启。
   - **部署Minio**：
     - 使用Docker运行Minio，配置API地址、管理地址、存储路径和随机生成的用户凭证。
     - 创建名为`outline`的Bucket，用于存储上传的文件和图片。
   - **部署OIDC服务器**：
     - 使用Docker运行sso-server，配置客户端ID、密钥和默认密码。
     - 提供登录页面，默认用户名为`username`，密码为`USER_PASS`字段设置的值。

4. **Outline配置**：
   - **拉取Outline镜像**：使用`docker pull outlinewiki/outline:0.63.0`拉取指定版本的镜像。
   - **编辑.env文件**：
     - 配置数据库连接、Redis连接、Minio存储、OIDC认证等关键参数。
     - 生成随机密钥（如`SECRET_KEY`和`UTILS_SECRET`）。
     - 配置第三方登录（如Google、Slack、Microsoft）或OIDC认证。
   - **数据库迁移**：运行`yarn db:migrate`命令，确保数据库结构正确。

5. **运行Outline**：
   - 使用Docker运行Outline容器，配置环境变量、端口映射和自动重启。
   - 访问`http://192.168.100.155:13090`，查看部署结果。

6. **注意事项**：
   - **Minio配置**：确保API地址和管理地址正确，反向代理需开启`proxy_pass`。
   - **OIDC服务器**：确保客户端ID、密钥和URI配置正确。
   - **版本兼容性**：配置文件适用于Outline 0.63.0版本，新版可能需要调整。

7. **总结**：本文详细介绍了如何在UnRaid系统中使用Docker部署Outline，包括PostgreSQL、Redis、Minio和OIDC服务器的配置，以及Outline的运行和调试步骤。

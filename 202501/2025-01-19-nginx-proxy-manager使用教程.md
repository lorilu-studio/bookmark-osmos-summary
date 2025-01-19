# Nginx Proxy Manager使用教程
- URL: https://www.golovin.cn/post/11#
- Added At: 2025-01-19 05:38:42
- [Link To Text](2025-01-19-nginx-proxy-manager使用教程_raw.md)

## TL;DR
Nginx Proxy Manager 是一个基于 Nginx 的反向代理管理工具，通过 Web 界面简化了反向代理、HTTPS 配置和访问权限管理。文章详细介绍了其安装、配置、SSL 证书申请、服务器监控设置及常见问题的解决方法，适合需要简化 Nginx 配置的用户使用。

## Summary
1. **反向代理概念**：
   - 反向代理允许通过不同的域名访问同一服务器上的不同服务，类似于菜鸟驿站分发包裹给不同家庭。
   - Nginx是一个广泛使用的反向代理服务器，但配置较为复杂。

2. **Nginx Proxy Manager简介**：
   - 提供基于Nginx的Web管理界面，简化反向代理和HTTPS配置。
   - 主要功能包括轻松设置反向代理、配置HTTPS和简单的访问权限管理。

3. **安装Nginx Proxy Manager**：
   - **前提**：需要安装Docker和Docker Compose。
   - **安装步骤**：
     - 创建专用文件夹并设置`docker-compose.yml`文件。
     - 启动服务并通过`ip:81`访问管理界面，默认登录凭据为`admin@example.com`和`changeme`。

4. **设置后台管理界面的反向代理**：
   - **前提**：安装Nginx Proxy Manager并拥有域名。
   - **操作步骤**：
     - 在Nginx Proxy Manager中添加反向代理，指定域名和端口。
     - 使用`ip addr show docker0`获取宿主机IP以正确配置`Forward Hostname / IP`。

5. **申请泛域名SSL证书**：
   - 在Nginx Proxy Manager中申请`*.test.com`的SSL证书，使用DNS Challenge验证域名所有权。
   - 配置DNS服务商的API Key或Token以完成证书申请。

6. **设置HTTPS**：
   - 在反向代理设置中选择已申请的SSL证书，并启用强制HTTPS选项。

7. **服务器监控设置**：
   - 使用Docker安装Ward服务器监控工具。
   - 在Nginx Proxy Manager中设置反向代理和SSL，并配置访问权限。

8. **权限设置**：
   - 在Nginx Proxy Manager中创建访问列表，设置用户名和密码，以及IP白名单或黑名单。

9. **其他更新和问题解决**：
   - **Minio桶列表加载问题**：通过开启WebSocket支持或添加自定义Nginx配置解决。
   - **Nacos路径自定义**：添加自定义Nginx配置以支持特定路径。
   - **HTML重定向**：在Nginx Proxy Manager中设置自定义位置和重写规则以实现页面重定向。
   - **Docker-compose重启登录失败**：修改应用的JavaScript代码以解决因网络请求导致的登录问题。

10. **总结**：
    - Nginx Proxy Manager提供了一个用户友好的界面来管理复杂的Nginx配置，包括反向代理、SSL证书和访问控制。
    - 通过Docker容器化部署，可以轻松地在不同环境中复制和扩展这些配置。

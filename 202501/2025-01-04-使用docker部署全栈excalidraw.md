# 使用Docker部署全栈Excalidraw
- URL: https://www.jamesflare.com/zh-cn/excalidraw-full-stack-docker/
- Added At: 2025-01-04 05:56:27
- [Link To Text](2025-01-04-使用docker部署全栈excalidraw_raw.md)

## TL;DR
文章介绍了如何使用Docker部署全栈Excalidraw，解决了现有教程仅部署前端导致功能缺失的问题。通过配置前端、后端、协作服务和Redis，实现了完整的分享和协作功能。文章详细说明了Docker Compose配置和部署步骤，并建议配置反向代理以支持HTTPS。适用于需要在本地私有化部署Excalidraw的用户。

## Summary
1. **文章背景**：
   - **主题**：使用Docker部署全栈Excalidraw。
   - **作者**：James。
   - **发布时间**：2023年1月13日。
   - **更新日期**：2024年3月11日。
   - **字数**：约1000字。
   - **阅读时间**：预计2分钟。

2. **问题描述**：
   - **现有部署问题**：大多数教程只部署了Excalidraw的前端（excalidraw-app），导致分享链接、在线协作和Libraries功能无法使用。
   - **原因**：缺少必要的后端服务（excalidraw-json和excalidraw-room）。

3. **解决方案**：
   - **前端**：使用9个月前的官方excalidraw-app版本，功能稳定且兼容性好。
   - **后端**：
     - **存储**：使用第三方实现的全功能后端excalidraw-storage-backend，支持v2 API。
     - **协作**：使用9个月前的官方excalidraw-room版本，与前端兼容。
   - **Redis**：用于临时存储分享画板的数据，但不保证数据可靠性。

4. **Docker Compose配置**：
   - **服务**：
     - **excalidraw**：前端服务，端口80。
     - **excalidraw-storage-backend**：存储后端服务，端口8080。
     - **excalidraw-room**：协作服务，端口5000。
     - **redis**：Redis服务，端口6379。
   - **环境变量**：配置了后端URL、库URL、Socket服务器URL等。
   - **网络配置**：支持自定义网络（excalidraw-net）以解决端口冲突问题。

5. **部署步骤**：
   - **创建目录**：新建或选择一个目录。
   - **创建docker-compose文件**：使用`nano docker-compose.yml`创建并填入配置。
   - **反向代理配置**：建议配置反向代理以支持HTTPS和WebSocket。

6. **总结**：
   - **适用场景**：适用于需要在本地私有化部署Excalidraw的用户。
   - **优势**：全栈部署，功能完整，支持分享和协作。
   - **注意事项**：需自行配置反向代理以支持HTTPS。

7. **相关资源**：
   - **合集**：Docker Compose。
   - **其他教程**：包括修正Flarum邮件发送问题、部署LobeChat服务端数据库版本、迁移Umami等。

8. **版权信息**：
   - **版权声明**：CC BY-NC 4.0。
   - **主题**：FixIt。
   - **驱动**：Hugo。

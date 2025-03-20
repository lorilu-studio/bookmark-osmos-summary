# 从零开始使用开源文档/Wiki软件 Outline（二）
- URL: https://soulteary.com/2021/09/11/opensource-documentation-wiki-software-outline-part-2.html
- Added At: 2025-03-20 14:17:12
- [Link To Text](2025-03-20-从零开始使用开源文档-wiki软件-outline（二）_raw.md)

## TL;DR
本文是《从零开始使用开源文档/Wiki软件 Outline》系列的第二部分，详细介绍了 Outline 的图片和附件管理功能。文章提供了解决图片上传错误和彻底删除图片的方法，并建议使用外部文件服务器管理附件。下一篇文章将探讨如何定制 Outline 以适应个人或团队需求。

## Summary
1. **文章概述**：本文是《从零开始使用开源文档/Wiki软件 Outline》系列的第二部分，主要介绍 Outline 的一些细节配置和功能扩展。

2. **代码更新**：
   - 作者对之前提到的示例代码进行了更新，添加了存储初始化脚本，并将 Outline 升级到最新版本。
   - 建议之前下载过代码的用户重新下载或使用 `git pull` 更新。

3. **图片管理问题**：
   - **问题描述**：用户在上传图片时可能会遇到错误提示，原因是 MinIO 存储未自动初始化。
   - **解决方案**：作者提供了一个 `docker-compose.minio-init.yml` 配置文件，用户只需在启动 Outline 后执行一条命令即可初始化 MinIO 存储。
   - **操作步骤**：
     - 执行命令：`docker-compose -f docker-compose.minio-init.yml up`
     - 查看日志确认初始化成功。
     - 再次尝试上传图片，问题应已解决。

4. **彻底删除图片**：
   - **问题描述**：Outline 编辑器中的“删除图片”功能并未真正删除图片文件。
   - **解决方案**：通过 MinIO 管理界面手动删除图片文件。
   - **操作步骤**：
     - 访问 MinIO 管理界面（`file.lab.com`）。
     - 使用 `MINIO_ROOT_USER` 和 `MINIO_ROOT_PASSWORD` 登录。
     - 在“Object Browser”中找到并删除图片文件。

5. **附件管理**：
   - **问题描述**：当前版本的 Outline 不支持附件功能。
   - **解决方案**：借助外部文件服务器实现附件管理。
   - **操作步骤**：
     - 访问文件服务器（`attachment.lab.com`），使用 Basic Auth 登录。
     - 上传文件并获取公开链接。
     - 将附件链接复制到 Outline 文章中使用。
   - **未来展望**：下个版本的 Outline 可能支持附件管理，但建议暂时使用外部存储方式。

6. **总结与预告**：
   - 本文详细介绍了 Outline 的图片和附件管理功能。
   - 下一篇文章可能会讨论如何快速定制 Outline，以更好地适应个人或团队的需求。

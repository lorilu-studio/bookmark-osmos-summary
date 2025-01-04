# 免费的云数据库PostgreSQL 
- URL: https://juejin.cn/post/7411047482651951119
- Added At: 2025-01-04 05:53:51
- [Link To Text](2025-01-04-免费的云数据库postgresql_raw.md)

## TL;DR
本文介绍了多款提供免费PostgreSQL服务的云平台，包括Supabase、Neno、Xata、Vercel Postgres和Memfire Cloud，详细说明了它们的免费使用额度和创建数据库的步骤。同时，文章还提醒用户在使用云数据库时应注意数据备份、环境分离和资源监控等事项，并推荐Supabase作为首选平台。

## Summary
1. **引言**：
   - PostgreSQL 以其丰富的功能性、卓越的扩展性和优秀的并发性能成为开发者的首选。
   - 本文将介绍几款提供 PostgreSQL 服务免费使用额度的云平台，助力个人项目和原型项目开发。

2. **免费的云数据库**：
   - **Supabase**：
     - 开源 BasS 平台，基于 PostgreSQL 构建，提供类似 Firebase 的功能。
     - 免费使用额度：500 MB 空间，共享 CPU，500 MB RAM。
     - 数据库创建步骤：
       1. 登录后点击「New project」按钮。
       2. 填写基本信息并保存数据库密码。
       3. 等待数据库初始化完成，点击「Connect」按钮复制数据库链接 URL。
     - 资源池模式：
       - Transcation mode：端口号 6543，适合无服务环境和边缘计算环境。
       - Session mode：端口号 5432，直接连接到数据库，有最大连接数量限制。
   - **Neno**：
     - 提供专业的 PostgreSQL 云服务，是 Vercel PostgreSQL 服务的供应商。
     - 免费使用额度：500 MB 空间，0.25 CPU / 500 MB RAM ～ 2 CPU / 8 GB RAM。
     - 数据库创建步骤：登录后进入创建项目页面，填写基本信息。
   - **Xata**：
     - 完全托管的 PostgreSQL 数据库平台。
     - 免费使用额度：15 GB 空间，共享环境。
     - 数据库创建步骤：登录后点击「Add database」即可创建数据库。
   - **Vercel Postgres**：
     - 基于 Neon 的 PostgreSQL 服务，免费额度较少。
     - 免费使用额度：256 MB 空间，每月 60 小时时长。
     - 数据库创建步骤：登录后选中「Storage」面板，创建「Postgres」服务。
   - **Memfire Cloud（国内）**：
     - 采用开源的 Supabase 技术架构，兼容国内开发生态。
     - 免费使用额度：512 MB 空间，每月 1 GB 流量。
     - 创建数据库步骤：登录后进入云数据库管理页面，点击「创建数据库」即可。

3. **使用云数据库注意事项**：
   - 注意及时备份数据。
   - 建议开发环境和生产环境使用不同的数据库。
   - 定期查看云数据库使用额度、运行监控。
   - 根据应用运行的服务器的环境，选择合适的数据库连接 URL：
     - 如果应用运行在 Vercel 这种无服务器环境中，可以使用 Serverless 版的 PostgreSQL 数据库连接。
     - 如果应用运行在云服务器上，使用常规的数据库连接 URL 即可。

4. **结语**：
   - 推荐使用 Supabase，专业性和稳定性更胜一筹。
   - 欢迎分享其他不错的资源。

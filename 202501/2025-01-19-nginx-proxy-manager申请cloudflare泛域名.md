# Nginx Proxy Manager申请cloudflare泛域名
- URL: https://www.shawhow.com/archives/nginx-proxy-managershen-qing-cloudflarefan-yu-ming
- Added At: 2025-01-19 05:17:36
- [Link To Text](2025-01-19-nginx-proxy-manager申请cloudflare泛域名_raw.md)

## TL;DR
本文介绍了如何使用Nginx Proxy Manager和Cloudflare进行泛域名反向代理配置。文章详细说明了从申请Cloudflare API Token到在Nginx Proxy Manager中配置泛域名证书的步骤，帮助用户快速完成证书申请和配置，提升网站安全性和访问速度。

## Summary
1. **Nginx Proxy Manager简介**：
   - 基于Nginx的反向代理管理工具，提供用户友好的Web界面。
   - 主要功能：
     - **简易的用户界面**：快速添加和管理代理主机。
     - **SSL管理**：通过Let's Encrypt自动获取和续订SSL/TLS证书。
     - **访问控制**：设置IP限制或基本认证。
     - **HTTP代理与Websocket支持**：支持常规HTTP代理和WebSocket代理。
     - **简单的Docker部署**：方便通过Docker部署。
     - **多域名支持**：在同一实例中管理多个域名和主机。

2. **Cloudflare简介**：
   - 提供网络安全和性能优化服务。
   - 主要产品：
     - **内容分发网络（CDN）**：加速网站加载速度。
     - **DDoS防护**：抵御大规模流量攻击。
     - **域名解析服务（DNS）**：提供智能路由和负载均衡。
     - **网络应用防火墙（WAF）**：提高网站安全性。
   - 目标：提升在线内容的安全性和访问速度，改善用户体验。

3. **相关环境**：
   - **操作系统**：支持Docker的系统如Ubuntu、CentOS、Debian等。
   - **Nginx Proxy Manager版本**：建议使用最新版本。
   - **Cloudflare账号**：需有效账号并已添加至少一个域名。
   - **网络环境**：确保服务器能访问互联网。

4. **相关地址**：
   - **Cloudflare官网**：[https://www.cloudflare.com](https://www.cloudflare.com)
   - **Cloudflare API Token申请地址**：[https://dash.cloudflare.com/profile/api-tokens](https://dash.cloudflare.com/profile/api-tokens)
   - **Nginx Proxy Manager官方文档**：[https://nginxproxymanager.com/](https://nginxproxymanager.com/)
   - **Cloudflare官方文档**：[https://developers.cloudflare.com/](https://developers.cloudflare.com/)

5. **Cloudflare API Token申请**：
   - **申请地址**：[https://dash.cloudflare.com/profile/api-tokens](https://dash.cloudflare.com/profile/api-tokens)
   - **创建令牌**：
     - 使用模板或自建。
     - **权限设置**：选择DNS。
     - **区域设置**：选择所有区域。
     - **客户端IP地址**：可设置以增加安全性。
   - **确认信息**：确认无误后创建令牌。
   - **保存令牌**：令牌单次显示，务必保存好。

6. **Nginx Proxy Manager泛域名反代**：
   - **进入后台**：在申请证书页面添加新的泛域名证书。
   - **填写域名信息**：
     - **域名**：填写需要申请的泛域名。
     - **邮箱地址**：填写Cloudflare的邮箱地址。
     - **DNS供应商**：选择Cloudflare。
   - **填写凭证**：
     - 将`dns_cloudflare_api_token`后的值替换为申请的API令牌。
   - **确认信息**：确认无误后同意服务条款并存储。
   - **等待证书生成**：Nginx Proxy Manager自动申请证书，成功后可在证书列表中查看。

7. **总结**：
   - 文章详细讲解了从Cloudflare申请API Token到在Nginx Proxy Manager中配置泛域名证书的步骤。
   - 通过Nginx Proxy Manager和Cloudflare，用户可以快速完成泛域名证书的申请和配置。

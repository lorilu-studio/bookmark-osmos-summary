Title: 「服务器」Nginx Proxy Manager申请cloudflare泛域名

URL Source: https://www.shawhow.com/archives/nginx-proxy-managershen-qing-cloudflarefan-yu-ming

Published Time: 2024-09-26T13:30:14.084854153Z

Markdown Content:
**概述**
------

Nginx Proxy Manager 是一个基于 Nginx 的反向代理管理工具，它提供了一个用户友好的 Web 界面，方便用户管理和配置 Nginx 反向代理。主要功能包括：

1.  **简易的用户界面** ：通过图形界面，可以快速添加和管理代理主机（即反向代理规则）。
    
2.  **SSL 管理** ：支持通过 Let's Encrypt 自动获取和续订 SSL/TLS 证书，以保护网站的安全性。
    
3.  **访问控制** ：可以对代理主机设置访问控制，例如限制某些 IP 地址的访问，或者要求基本认证。
    
4.  **HTTP 代理与 Websocket 支持** ：支持常规的 HTTP 代理以及 WebSocket 代理。
    
5.  **简单的 Docker 部署** ：可以很方便地通过 Docker 部署 Nginx Proxy Manager。
    
6.  **多域名支持** ：可以在同一个实例中管理多个域名和主机。
    

Nginx Proxy Manager 适合需要在多个服务之间设置反向代理并希望简化配置过程的用户。

Cloudflare是一家提供网络安全和性能优化服务的公司。其主要产品包括内容分发网络（CDN）、DDoS防护、网站加速、域名解析服务（DNS）、以及网络应用防火墙（WAF）等。

通过使用Cloudflare的服务，网站可以实现：

1\. **加速加载速度**：通过全球分布的CDN节点，将网站内容缓存到离用户更近的服务器上，从而减少加载时间。

2\. **提高安全性**：提供DDoS防护，抵御大规模的流量攻击，保护网站免受恶意攻击。

3\. **改善可靠性**：通过智能路由和负载均衡，提高网站的可用性和性能。

4\. **易于管理**：提供用户友好的界面和API，使网站管理员能够方便地管理和配置。

总的来说，Cloudflare旨在帮助用户提升在线内容的安全性和访问速度，改善用户体验。

文章将详细讲解从Cloudflare申请API Token到在Nginx Proxy Manager中配置泛域名证书的每一步骤，帮助快速上手并完成配置。

**相关环境**
--------

*   **操作系统** ：适用于所有支持Docker的操作系统，如Ubuntu、CentOS、Debian等。并且正确安装Nginx Proxy Manager
    
*   **Nginx Proxy Manager版本** ：建议使用最新版本，以确保兼容性和安全性。
    
*   **Cloudflare账号** ：需要一个有效的Cloudflare账号，并已添加至少一个域名。
    
*   **网络环境** ：确保服务器能够访问互联网，以便与Cloudflare API通信。
    

**相关地址**
--------

*   **Cloudflare官网：**
    

[https://www.cloudflare.com](https://www.cloudflare.com/)

*   **Cloudflare API Token申请地址** ：  
    [https://dash.cloudflare.com/profile/api-tokens](https://dash.cloudflare.com/profile/api-tokens)
    
*   **Nginx Proxy Manager官方文档** ：  
    [https://nginxproxymanager.com/](https://nginxproxymanager.com/)
    
*   **Cloudflare官方文档** ：  
    [https://developers.cloudflare.com/](https://developers.cloudflare.com/)
    

Cloudflare申请 API Token
----------------------

**申请API Token地址** 
------------------

打开以下网址：[https://dash.cloudflare.com/profile/api-tokens](https://dash.cloudflare.com/profile/api-tokens)  
或者从任意一个域名页面内的API进入。  
![Image 27](https://www.shawhow.com/upload/image-wmtv.png)

创建令牌 
-----

![Image 28](https://www.shawhow.com/upload/image-zcsj.png)

可以使用模板，或者自建都是一样的

![Image 29](https://www.shawhow.com/upload/image-jjpe.png)

*   权限设置：选择DNS即可。
    
*   区域设置：选择所有区域。
    
*   为了安全，可以设置一个客户端IP地址。
    

![Image 30](https://www.shawhow.com/upload/image-pxhi.png)

**确认信息** 
---------

确认信息无误后，即可创建令牌。

![Image 31](https://www.shawhow.com/upload/image-uwas.png)

**保存令牌**
--------

成功创建后，即会显示创建的令牌信息。

![Image 32](https://www.shawhow.com/upload/image-jtzk.png)

> **注意 ：令牌是单次显示，请务必保存好令牌。**

Nginx Proxy Manager泛域名反代
------------------------

**进入Nginx Proxy Manager后台**
---------------------------

在申请证书页面，添加一个新的泛域名证书。

![Image 33](https://www.shawhow.com/upload/image-rxql.png)

**填写域名信息**
----------

*   域名：填写需要申请的泛域名。
    
*   邮箱地址：填写Cloudflare的邮箱地址。
    
*   DNS供应商：选择Cloudflare。
    

![Image 34](https://www.shawhow.com/upload/image-ybsi.png)

**填写凭证**
--------

选择DNS供应商后，会自动弹出凭证。凭证的格式会自动帮我们填写好。将`dns_cloudflare_api_token`后面的值替换成刚才我们申请的API令牌。

```
# Cloudflare API token
dns_cloudflare_api_token=<刚才申请API的令牌>
```

![Image 35](https://www.shawhow.com/upload/image-ecky.png)

**确认信息**
--------

确认信息没有问题后，同意服务条款，然后选择存储。

![Image 36](https://www.shawhow.com/upload/image-aglq.png)

**等待证书生成**
----------

稍等一段时间后，Nginx Proxy Manager会自动帮我们申请证书。成功申请后，就可以在证书列表中查看到。

![Image 37](https://www.shawhow.com/upload/image-knye.png)

这样，就完成了通过Nginx Proxy Manager和Cloudflare申请泛域名证书的全部步骤。

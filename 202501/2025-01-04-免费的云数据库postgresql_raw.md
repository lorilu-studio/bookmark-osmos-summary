Title: 分享：一些免费的 PostgreSQL 云数据库PostgreSQL 以其丰富的功能性、卓越的扩展性和优秀的并发性能等优 - 掘金

URL Source: https://juejin.cn/post/7411047482651951119

Markdown Content:
引言
--

在全栈应用开发中，数据库扮演着核心角色。随着 PostgreSQL 以其丰富的功能性、卓越的扩展性和优秀的并发性能等优势逐渐成为开发者的首选，本文将介绍几款提供 PostgreSQL 服务免费使用额度的云平台，助力个人项目和原型项目开发。

免费的云数据库
-------

### 1\. Supabase

Supabase 是一个开源的 BasS 平台，旨在为开发者提供类似 Firebase 的功能，但基于 PostgreSQL 构建。它简化了数据库、身份验证、存储和 API 的集成，帮助开发者快速构建现代 Web 应用。

官网：[supabase.com/](https://link.juejin.cn/?target=https%3A%2F%2Fsupabase.com%2F "https://supabase.com/")

**Supabase 提供的数据库免费使用额度：500 MB 空间，共享 CPU，500 MB RAM。**

数据库创建步骤：

1.  登录之后，点击 [Dashboard 页面](https://link.juejin.cn/?target=https%3A%2F%2Fsupabase.com%2Fdashboard%2Fprojects "https://supabase.com/dashboard/projects") 右上角的「New project」按钮
2.  在创建项目页面，填写基本信息 **（请保存这一步填写的数据库密码！）**

完成这两步之后会跳转到新建的项目首页，等待数据库初始化完成。

然后点击右上角的「Connect」按钮，在弹出的弹窗中便可以复制数据库链接 URL。

![Image 12: Area480.gif](https://p6-xtjj-sign.byteimg.com/tos-cn-i-73owjymdk6/828bba5e1e1043ab86fb031a55bff686~tplv-73owjymdk6-jj-mark-v1:0:0:0:0:5o6Y6YeR5oqA5pyv56S-5Yy6IEAg5Lq66Ze06KeC5a-f5ZGY:q75.awebp?rk3s=f64ab15b&x-expires=1736465324&x-signature=3ztZydfTq3Gk7NCzBdLEnDRzltg%3D)

复制的 URL 类似下面这种，将 `[YOUR-PASSWORD]` 替换为刚才创建数据库时你输入的密码即可：

```
postgresql://postgres.foo:[YOUR-PASSWORD]@bar.supabase.com:5432/postgres
```

此外，在弹窗中可以看到有这么个选择器：

![Image 13: image.png](https://p6-xtjj-sign.byteimg.com/tos-cn-i-73owjymdk6/26d9a1757807427ca4e89bb489aba804~tplv-73owjymdk6-jj-mark-v1:0:0:0:0:5o6Y6YeR5oqA5pyv56S-5Yy6IEAg5Lq66Ze06KeC5a-f5ZGY:q75.awebp?rk3s=f64ab15b&x-expires=1736465324&x-signature=ICAZAnrArRNu1%2FcrirhtR4MwItA%3D)

这里选择的是连接的资源池模式（pooling modes）。Supabase 支持 2 种资源池模式：

1.  Transcation mode 端口号对应 `6543` ，这种模式更适合无服务环境和边缘计算环境（Serveless and Edge enviroments），此时某些基于 PostgreSQL 会话的功能将无法使用，如预处理语句
2.  Session mode 端口号对应 `5432` ，这种模式会直接连接到数据库，此时会有最大连接数量限制，因为连接会从建立之后一直保持直到客户端断开连接

更多可参考：[Supabase: Connecting to your database](https://link.juejin.cn/?target=https%3A%2F%2Fsupabase.com%2Fdocs%2Fguides%2Fdatabase%2Fconnecting-to-postgres%23how-connection-pooling-works "https://supabase.com/docs/guides/database/connecting-to-postgres#how-connection-pooling-works")

### 2\. Neno

Neno 提供专业的 PostgreSQL 云服务，是 Vercel PostgreSQL 服务的供应商。

官网：[neon.tech/](https://link.juejin.cn/?target=https%3A%2F%2Fneon.tech%2F "https://neon.tech/")

**Neno 提供的数据库免费使用额度：500 MB 空间，0.25 CPU / 500 MB RAM ～ 2 CPU / 8 GB RAM。**

数据库创建步骤：登录之后，进入创建项目页面，填写基本信息。

Neno 提供数据库连接同样支持无服务器和边缘计算环境。按需选择即可。

### 3\. Xata

Xata是一个完全托管的 PostgreSQL 数据库的平台。

官网：[xata.io/](https://link.juejin.cn/?target=https%3A%2F%2Fxata.io%2F "https://xata.io/")

**Xata 提供的数据库免费使用额度：15 GB 空间，共享环境。**

数据库创建步骤：登录之后，点击右上角的「Add database」即可创建数据库。

### 4\. Vercel Postgres

Vercel Postgres 服务基于上面提到的 Neon，但是免费额度更少、收费更高 🤣。想要用 Vercel Postgres 不如直接用 Neon。

官网：[vercel.com/](https://link.juejin.cn/?target=https%3A%2F%2Fvercel.com%2F "https://vercel.com/")

**Vercel Postgres 提供的数据库免费使用额度：256 MB 空间，每月 60 小时时长。**

数据库创建步骤：登录之后，选中「Storage」面板，创建「Postgres」服务即可。

![Image 14: image.png](https://p6-xtjj-sign.byteimg.com/tos-cn-i-73owjymdk6/a21e4058430449009ca6810724054982~tplv-73owjymdk6-jj-mark-v1:0:0:0:0:5o6Y6YeR5oqA5pyv56S-5Yy6IEAg5Lq66Ze06KeC5a-f5ZGY:q75.awebp?rk3s=f64ab15b&x-expires=1736465324&x-signature=rYQ%2BhqvUzXCgfYX8524SeLHtnv0%3D)

### 5\. Memfire Cloud（国内）

Memfire Cloud 采用开源的 Supabase 技术架构，兼容国内开发生态，内置通用服务，加速小程序 / Web /移动应用的开发。

官网： [memfiredb.com/](https://link.juejin.cn/?target=https%3A%2F%2Fcloud.memfiredb.com%2Fauth%2Flogin%3Ffrom%3D8qU4lV "https://cloud.memfiredb.com/auth/login?from=8qU4lV")

**Memfire Cloud 提供的数据库免费使用额度：512 MB 空间，每月 1 GB 流量。**

创建数据库步骤：登录之后，进入 [云数据库管理页面](https://link.juejin.cn/?target=https%3A%2F%2Fcloud.memfiredb.com%2Fdb%2Fmanage%2Fdatabases "https://cloud.memfiredb.com/db/manage/databases")，点击「创建数据库」即可。

使用云数据库注意事项
----------

*   注意及时备份数据
    
*   建议开发环境和生产环境使用不同的数据库
    
*   定期查看云数据库使用额度、运行监控
    
*   根据应用运行的服务器的环境，选择合适的数据库连接 URL
    
    *   如果应用运行在 Vercel 这种无服务器环境中，可以使用 Serverless 版的 PostgreSQL 数据库连接
    *   如果应用运行在云服务器上，使用常规的数据库连接 URL 即可

结语
--

以上就是我要分享的可以免费使用 PostgreSQL 数据库的云服务商，总得来说，我更推荐 [supabase.com](https://link.juejin.cn/?target=https%3A%2F%2Fsupabase.com "https://supabase.com") ，专业性和稳定性都更胜一筹。

当然如果你也有不错的资源欢迎分享～

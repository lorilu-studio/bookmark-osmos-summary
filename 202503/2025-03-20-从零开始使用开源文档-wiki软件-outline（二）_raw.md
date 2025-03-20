Title: 从零开始使用开源文档/Wiki软件 Outline（二）

URL Source: https://soulteary.com/2021/09/11/opensource-documentation-wiki-software-outline-part-2.html

Published Time: 2021-09-11T18:03:00+08:00

Markdown Content:
上篇文章中，我们提到了如何快速部署和使用 Outline，本篇文章将展开介绍 Outline 的一些细节配置。

写在前面
----

为了方便使用，我对上篇文章中提到的示例代码 [https://github.com/soulteary/docker-outline](https://github.com/soulteary/docker-outline) 进行了一些更新，添加了一个存储初始化脚本，并将 Outline 升级到了官方最新的版本。

所以，如果你之前已经下载过代码，那么建议你重新下载一份新的代码或者进行 `git pull` 更新。

下文中的提到的“配置常量”，均指代项目中的 `.env` 文件中的内容，如果你还不了解这部分内容，请移步[《从零开始使用开源文档/Wiki软件 Outline（一）》](https://soulteary.com/2021/09/05/opensource-documentation-wiki-software-outline-part-1.html)。

如何进行图片管理
--------

相信有一些跟着上篇文章搭建完毕的同学，会发现 Outline 无法正确上传图片，页面左下角提示：“抱歉，上传图片时出现错误（Sorry, an error occurred uploading the image）”。

引起这个问题的原因是因为 minio 并未自动初始化，在我们之前使用的软件中，不少软件会判断存储空间是否存在，如果不存在，则进行自动创建，但是在当前版本的 Outline 和 MinIO 中，这个功能并未实现，所以我们需要手动进行创建。

考虑到多数同学的实践体验，为了让操作更简单一些，我额外创建了一个名为 `docker-compose.minio-init.yml` 的配置文件：

```
version: "3"
services:

  minio-client:
    image: ${DOCKER_MINIO_CLIENT_IMAGE_NAME}
    entrypoint: >
      /bin/sh -c "
      /usr/bin/mc config host rm local;
      /usr/bin/mc config host add --quiet --api s3v4 local http://outline_minio:9000 ${MINIO_ROOT_USER} ${MINIO_ROOT_PASSWORD};
      /usr/bin/mc mb --quiet local/${AWS_S3_UPLOAD_BUCKET_NAME}/;
      /usr/bin/mc policy set public local/${AWS_S3_UPLOAD_BUCKET_NAME};
      "      
    networks:
      - outline

networks:
  outline:
    external: true
```

有了上面这个配置文件之后，只需要在启动 Outline 之后，再执行一条命令行就行了：

```
docker-compose -f docker-compose.minio-init.yml up
```

命令执行完毕，不出意外，你将会看到类似下面的日志输出。

```
Creating docker-outline_minio-client_1 ... done
Attaching to docker-outline_minio-client_1
minio-client_1  | Removed `local` successfully.
minio-client_1  | Added `local` successfully.
minio-client_1  | Bucket created successfully `local/outline/`.
minio-client_1  | Access permission for `local/outline` is set to `public`
docker-outline_minio-client_1 exited with code 0
```

接着，在 Outline 中再次尝试上传图片，会发现已经能够正常使用这个功能啦。

![Image 1: 图片顺利上传 Outline](https://attachment.soulteary.com/2021/09/11/outline-image-upload.png)

图片顺利上传 Outline

### 如何彻底删除图片

虽然在 Outline 编辑器中包含了“从文章中删除图片”的功能，但是我们实际上我们上传的内容并没有被正确的删除。我们以默认配置中的设置来讲解一下如何彻底删除掉上传的图片文件。

浏览器打开 `file.lab.com`（`DOCKER_MINIO_HOSTNAME`），会被自动跳转至 `file-admin.lab.com/login`（`DOCKER_MINIO_ADMIN_DOMAIN`）这个管理地址。

![Image 2: MinIO 登陆界面](https://attachment.soulteary.com/2021/09/11/outline-minio-login.png)

MinIO 登陆界面

使用配置中 `MINIO_ROOT_USER` 和 `MINIO_ROOT_PASSWORD` 的内容作为账号和密码进行登录之后，能够看到 MinIO 的管理界面。

![Image 3: MinIO 管理界面](https://attachment.soulteary.com/2021/09/11/outline-minio-dashboard.png)

MinIO 管理界面

在左侧侧边栏中找到“Object Browser”，然后在其中找到我们上传的图片名称，在此处进行删除，即可达到我们预期的彻底删除的效果。

![Image 4: 在对象浏览器中找到文件](https://attachment.soulteary.com/2021/09/11/outline-minio-objects.png)

在对象浏览器中找到文件

后续，我会考虑提交一个 PR 来解决这个问题，或者使用一个更简单的方式来做图片附件管理，这个话题距离本篇文章比较远，就不展开了。

如何使用附件
------

当前版本的 Outline 并不支持附件功能，所以我们需要暂时借助“外力”来解决这个问题，在上篇文章中，我们已经启动了一个小巧高效的文件服务器，本篇文章我们就来介绍如何结合 Outline 进行使用。

首先使用浏览器访问 `attachment.lab.com`（`DOCKER_ATTACHMENT_HOSTNAME`），然后会看到浏览器提示需要输入用户密码，这是为了避免未授权的用户进行提交，如果你不希望使用 Basic Auth，也可以了解一下 [《Traefik 2 基础授权验证（前篇）》](https://soulteary.com/2020/12/02/traefik-2-basic-authorization-verification-part-1.html)、[《Traefik 2 基础授权验证（后篇）》](https://soulteary.com/2020/12/02/traefik-2-basic-authorization-verification-part-2.html)，使用更现代化的方式进行访问保护。

![Image 5: 提示需要 Basic Auth 登陆](https://attachment.soulteary.com/2021/09/11/outline-file-login.png)

提示需要 Basic Auth 登陆

使用 `DOCKER_ATTACHMENT_BASIC_AUTH` 中配置的用户名和密码进行登录后，就能够看的文件服务器的页面了。

![Image 6: 默认的附件管理首页](https://attachment.soulteary.com/2021/09/11/outline-file-home.png)

默认的附件管理首页

界面非常简单，将需要上传的文件拖拽到上传区域，或者使用文件选择器的方式选中文件，就能开始对任意大小的附件的上传操作了。

![Image 7: 附件上传过程](https://attachment.soulteary.com/2021/09/11/outline-file-upload.png)

附件上传过程

在上传过程中，我们能够实时看到上传进度。当文件上传完毕之后，我们点击 `delete` 前的文本链接，能够进入到附件的详情页面。

![Image 8: 获取附件公开链接](https://attachment.soulteary.com/2021/09/11/outline-file-url.png)

获取附件公开链接

在附件详情页面中，对 `get` 文本链接进行复制，将能够得到一个包含 “`raw`”字符串的地址，这个地址是能够进行公开访问的。（不需要前文中的登录操作）。

![Image 9: 使用外部附件链接](https://attachment.soulteary.com/2021/09/11/outline-files.png)

使用外部附件链接

然后，将附件地址复制至 Outline 文章中，就能够自由使用了。

据说下个版本的 Outline 将支持附件管理，不过考虑到存储数据稳定性，建议先使用这类外部存储的方式，等待新功能和数据管理逻辑稳定后，再进行迁移切换。

最后
--

在下篇 Outline 相关内容中，我或许将聊聊如何快速的对 Outline 进行定制。

毕竟一个属于、适合你或者你的团队的文档程序，才是真的好用的文档程序。

–EOF

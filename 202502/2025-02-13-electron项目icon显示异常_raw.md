Title: electron项目icon显示异常

URL Source: https://www.cnblogs.com/xwwin/p/16581249.html

Published Time: 2022-08-12T20:16:00.0000000+08:00

Markdown Content:
electron项目icon显示异常 - ！win ！ - 博客园
===============

*   [![Image 14: 博客园logo](https://assets.cnblogs.com/logo.svg)](https://www.cnblogs.com/ "开发者的网上家园")
*   [会员](https://cnblogs.vip/)
*   [周边](https://cnblogs.vip/store)
*   [众包](https://www.cnblogs.com/cmt/p/18500368)
*   [新闻](https://news.cnblogs.com/)
*   [博问](https://q.cnblogs.com/)
*   [闪存](https://ing.cnblogs.com/)
*   [赞助商](https://www.cnblogs.com/cmt/p/18341478)
*   [Chat2DB](https://chat2db-ai.com/)

*    ![Image 15: 搜索](https://assets.cnblogs.com/icons/search.svg) ![Image 16: 搜索](https://assets.cnblogs.com/icons/enter.svg)
    
    *   ![Image 17: 搜索](https://assets.cnblogs.com/icons/search.svg)
        
        所有博客
    *   ![Image 18: 搜索](https://assets.cnblogs.com/icons/search.svg)
        
        当前博客
    
*    [![Image 19: 写随笔](https://assets.cnblogs.com/icons/newpost.svg)](https://i.cnblogs.com/EditPosts.aspx?opt=1 "写随笔")[![Image 20: 我的博客](https://assets.cnblogs.com/icons/myblog.svg)](https://passport.cnblogs.com/GetBlogApplyStatus.aspx "我的博客")[![Image 21: 短消息](https://assets.cnblogs.com/icons/message.svg)](https://msg.cnblogs.com/ "短消息")[![Image 22: 简洁模式](https://assets.cnblogs.com/icons/lite-mode-on.svg)](javascript:void(0) "简洁模式启用，您在访问他人博客时会使用简洁款皮肤展示")
    
    [![Image 23: 用户头像](https://assets.cnblogs.com/icons/avatar-default.svg)](https://home.cnblogs.com/)
    
    [我的博客](https://passport.cnblogs.com/GetBlogApplyStatus.aspx) [我的园子](https://home.cnblogs.com/) [账号设置](https://account.cnblogs.com/settings/account) [会员中心](https://vip.cnblogs.com/my) [简洁模式 ![Image 24](https://www.cnblogs.com/images/lite-mode-check.svg)...](javascript:void(0) "简洁模式会使用简洁款皮肤显示所有博客") [退出登录](javascript:void(0))
    
    [注册](https://account.cnblogs.com/signup) [登录](javascript:void(0);)

[](https://github.com/xw5)

[![Image 25: 返回主页](https://www.cnblogs.com/skins/custom/images/logo.gif)](https://www.cnblogs.com/xwwin/)

[！win ！](https://www.cnblogs.com/xwwin)
=======================================

如果你去做了，一切便皆有可能！ 跬步千里！
---------------------

*   [博客园](https://www.cnblogs.com/)
*   [首页](https://www.cnblogs.com/xwwin/)
*   [新随笔](https://i.cnblogs.com/EditPosts.aspx?opt=1)
*   [联系](https://msg.cnblogs.com/send/%EF%BC%81win%20%EF%BC%81)
*   [订阅](javascript:void(0))
*   [管理](https://i.cnblogs.com/)

[electron项目icon显示异常](https://www.cnblogs.com/xwwin/p/16581249.html "发布于 2022-08-12 20:16")
==========================================================================================

### 前情

* * *

公司有个桌面端项目是基于Electron开发的。

### 坑

* * *

构建打包好的项目在桌面和任务栏上图标显示正常，但是在任务栏弹框上左上角的图标确不显示

### Why?

* * *

经过反复搜索，网上有文章说如果ico图标过大会导致这类问题，于是看了下我项目中ico图标大小，吓一跳，竟然有210K，而源png只有20K

### 解决方案

* * *

重新生成ico图标，在网上尝试了二个网址，20K的png转成ico图标大小都长了十倍左右，最终还是找到满意的在线工具了，生成的ico和PNG大小基本持平，在线转换工具地址如下：[https://convertio.co/zh/image-converter/](https://convertio.co/zh/image-converter/)

在如上地址重样生成新的ico文件，再替换掉旧的ico图标，重新打包，自测完美解决问题。

参考网址：[https://segmentfault.com/q/1010000019780156](https://segmentfault.com/q/1010000019780156)

好好学习！天天向上！

posted @ 2022-08-12 20:16  [！win ！](https://www.cnblogs.com/xwwin)  阅读(911)  评论(0)  [编辑](https://i.cnblogs.com/EditPosts.aspx?postid=16581249)  [收藏](javascript:void(0))  [举报](javascript:void(0))

努力加载评论中...

[刷新页面](https://www.cnblogs.com/xwwin/p/16581249.html#)[返回顶部](https://www.cnblogs.com/xwwin/p/16581249.html#top)

[![Image 26](https://img2024.cnblogs.com/blog/35695/202502/35695-20250207193659673-708765730.jpg)](https://www.doubao.com/chat/coding?channel=cnblogs&source=hw_db_cnblogs)

### 公告

Copyright © 2025 ！win ！  
Powered by .NET 9.0 on Kubernetes

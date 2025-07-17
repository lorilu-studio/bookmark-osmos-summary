# HEXO系列教程 | 将Qexo接入Hexo，实现静态博客的动态管理！ – 夜梦星尘の折腾日记
- URL: https://tech.yemengstar.com/hexo-use-qexo-to-manage/
- Added At: 2025-07-17 13:49:55
- [Link To Text](2025-07-17-hexo系列教程-将qexo接入hexo，实现静态博客的动态管理！-–-夜梦星尘の折腾日记_raw.md)

## TL;DR
本文详细介绍了如何将Qexo接入Hexo博客实现动态管理，包括Qexo的初始化配置、GitHub/Vercel密钥设置、文章发布和主题更换等操作步骤，并提供了相关教程链接。

## Summary
1. **教程概述**  
   - 文章介绍如何将Qexo接入Hexo静态博客，实现动态管理功能  
   - 相关前置教程链接：
     - [Hexo部署教程](https://tech.yemengstar.com/github-actions-auto-hexo/)  
     - [Qexo部署教程](https://tech.yemengstar.com/hexo-qexo-manager/)

2. **Qexo配置步骤**  
   - 2.1 用户名密码设置  
     - 在Vercel部署后通过默认域名进入初始化界面  
     - 建议绑定自定义域名（Vercel默认域名可能被阻断）  
     - 初始化时只需设置用户名密码，API密钥可留空自动生成  
   - 2.2 GitHub密钥配置  
     - 需要在GitHub生成具有Repo & Workflow权限的Token  
     - 具体权限设置建议：
       - 选择classic类型Token  
       - 勾选repo和workflow权限  
       - 设置永不过期  
     - 将生成的Token（格式如`ghp_EcJ44DIF...`）填入Qexo后台  
   - 2.3 Vercel密钥与项目ID  
     - 在Vercel账户创建Token  
     - 项目ID可在Settings → General中找到  

3. **Qexo使用指南**  
   - 3.1 发布文章  
     - 通过后台"文章"模块直接编写内容  
     - 支持Markdown格式编辑  
     - 保存后可立即发布到Hexo博客  
   - 3.2 更换主题  
     - 需本地操作后推送至GitHub仓库  
     - 推荐参考作者的Yun主题配置系列教程：
       - [PART1 基础配置](https://tech.yemengstar.com/hexo-tutorial-theme-yun1-beginner/)  
       - [PART2 进阶配置](https://tech.yemengstar.com/hexo-tutorial-theme-yun2-beginner/)  
       - [PART3 高级配置](https://tech.yemengstar.com/hexo-tutorial-theme-yun3-beginner/)

4. **补充信息**  
   - 版权声明：采用CC BY-NC-SA 4.0许可协议  
   - 相关标签：hexo, qexo, 网站建设  
   - 前后关联文章：
     - 上一篇：GitHub Actions部署Hexo教程  
     - 下一篇：Poste.io邮局部署教程

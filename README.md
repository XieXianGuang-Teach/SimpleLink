 # 简链SimpleLink

- 🎉打破长链接的束缚，释放创意的空间。用我们的短链接系统，为您的想法插上翅膀，让传播更自由

#### **介绍** 
- 本项目是一个短链接生成系统，旨在将冗长复杂的网址转化为简短易记的链接。系统操作简单，生成的短链接稳定可靠，支持快速跳转，适用于社交媒体分享、营销推广、二维码生成等多种场景，有效提升链接的传播效率和用户体验。

####  **软件开发环境** 
- PHP：7.4
- Nginx：1.26.3
- Html
- CSS

####  **安装教程** 
1. Fork本仓库
2. 服务器安装宝塔面板（bt.cn），安装必要的环境（php7.4+nginx1.26.3）
3. 点击宝塔面板左侧的 **网站** 按钮，类型默认PHP项目，然后新建一个网站，域名一栏输入你的域名（主域名或者二级甚至三级域名都可以），然后直接点击确定
4. 进入刚刚创建好的网站，进入网站根目录，删除根目录下的所有文件
5. 上传刚刚fork下来的压缩包，上传到网站根目录，并赋予777权限
6. 配置网站伪静态（你的站点 → 设置 → 伪静态），复制下面的代码到伪静态的输入页面

```
# 短链接路由：/ @link=abc → redirect.php?code=abc
location ~ "^/@link=([a-zA-Z0-9]{3,10})$" {
    try_files $uri $uri/ /redirect.php?code=$1;
    add_header X-ShortLink "SimpleLink" always;
}

# PHP 处理（保留原配置）
location ~ \.php$ {
    include fastcgi_params;
    fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    fastcgi_param PATH_INFO $fastcgi_path_info;
}

# 静态资源缓存
location ~* \.(html|css|js|png|jpg|svg)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}
```
备选方案（若报错）：


```
location ~ "^/@link=([a-zA-Z0-9]{3,10})$" {
    try_files $uri $uri/ /redirect.php?code=$1;
}
```


7. 开启SSL（非必要，但建议开启，提高安全性）：你的站点 → 设置 → SSL → 免费证书 → 申请证书 → 品牌和验证方法默认 → 勾选全选按钮 → 申请证书 → 等待申请（1分钟左右）→ 开启强制HTTPS
8. 访问网站主页和网站后台，默认管理员凭证：🔐 用户名：admin， 密码：SimpleLink666@
> ⚠️ 重要安全提示：
> 首次登录后台后请立即修改密码（编辑 admin.php 中的 ADMIN_PASS 常量）
> 该密码为代码明文存储，仅适用于内网/测试环境
> 公网部署务必：修改为高强度密码（建议16位以上含大小写/数字/符号）；通过 .htaccess 限制后台IP访问；将 admin.php 重命名为随机字符串（如 a7f3k9.php）。

####  **官方博客文章** 
- [简链SimpleLink 搭建教程](https://www.xiexianguang.com/forum.php?mod=viewthread&tid=49)
- [简链SimpleLink 中的常见问题](https://www.xiexianguang.com/forum.php?mod=viewthread&tid=50)


####  **参与贡献** 

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request

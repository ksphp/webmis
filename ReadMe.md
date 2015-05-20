<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<div sytle="font-size: 12px;">
<p>
<h1>WebMIS简介</h1>
WEBMIS是免费开源PHP开发CMS系统，基于CI的MVC模式开发的多用户、多权限解决方案，可以后台添加管理菜单，整合了Jquery，TinyMCE编辑器等插件、实现简洁、美观的弹框效果！
</p>
<p>
官方网站：<a href="http://www.ksphp.com/" target="_blank">灵创网络</a><br>
开源项目：<a href="https://github.com/ksphp/webmis/" target="_blank">WebMIS</a><br>
在线体验：<a href="http://webmis.ksphp.com/admin" target="_blank">http://webmis.ksphp.com/admin</a><br>
账户：webmis&nbsp;&nbsp;&nbsp;&nbsp;密码：ksphp.com
</p>
<p>
<h2>安装和配置</h2>
<h3>一、下载</h3>
<a href="https://github.com/ksphp/webmis/releases" target="_blank">https://github.com/ksphp/webmis/releases</a>
</p>
<p>
<h3>二、安装</h3>
文件解压到网站跟目录；<br><br>
<b>方法一：安装向导</b><br>
访问“install”目录<br><br>
<b>方法二：手动安装</b><br>
（1）创建数据库、导入“install”下的“webmis.sql”数据库文件； <br>
（2）修改数据库配置文件；<br>
管理后台：admin/app/config/database.php<br>
网站前台：web/config/database.php<br>
（3）修改 &ldquo;/&rdquo; 根目录和 &ldquo;/admin&rdquo; 下面的 .htaccess 文件（必须支持重写）；<br><br>
<b>问题1、二级目录 或 多级目录</b><br>
（1）编辑“/”下的“.htaccess”文件<br>
RewriteBase /二级目录/<br>
（2）编辑“/admin/”下的“.htaccess”文件<br>
RewriteBase /二级目录/admin/<br>
（3）编辑“/webmis/”下的“jquery.webmis.js”文件<br>
$webmis_root = '/二级目录/webmis/';<br>
（4）编辑“/admin/controllers/”下的“sys_filemanager.php”文件<br>
$upload = '/二级目录/upload';<br><br>
<b>问题2、环境不支持重写</b><br>
（1）编辑“/admin/config/”下的“config.php”文件<br>
$config['index_url'] = 'index.php/';<br>
（2）编辑“/web/config/”下的“config.php”文件<br>
$config['index_url'] = 'index.php/';<br>
注意：如果出现“403”错误，更改为“index.php?/”<br><br>
</p>
<p>
<h3>三、测试</h3>
网站前台：http://localhost/web<br>
管理员后台：http://localhost/admin (帐号：admin 密码：admin)
</p>
<p>
<h2>目录说明</h2>
admin-----------------------------<b>后台管理</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;backup------------------------数据备份目录 <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;config------------------------配置文件<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;views--------------------------视图目录：包括视图、主题目录、后台JS动作<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.htaccess---------------------后台重写文件、屏蔽index.php<br>
install---------------------------安装向导<br>
system----------------------------CI框架目录<br>
themes----------------------------前台样式目录<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;css---------------------------样式目录<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;images------------------------图片目录<br>
upload----------------------------上传目录<br>
web-------------------------------<b>网站前台</b><br>
webmis----------------------------前端样式插件<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;plugin------------------------第三方插件<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;src---------------------------JS插件<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;themes------------------------样式目录<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;jquery.webmis.js--------------webmis插件<br>
index.php-------------------------接口文件<br>
.htaccess-------------------------前台重写文件、屏蔽index.php
</p>
<p>&nbsp;</p>
<h2>去除index.php的方法</h2>
<h3>一、Apache</h3>
<p>
开启重写<br>
方法一：<br>
[...]<br>
&nbsp;&nbsp;&nbsp;&nbsp;AllowOverride All  #开启重写<br>
&nbsp;&nbsp;&nbsp;&nbsp;Require all granted<br>
&nbsp;&nbsp;&nbsp;&nbsp;Options Indexes FollowSymLinks  #浏览目录<br>
[...]
</p>
<p>
方法二：<br>
> a2enmod rewrite
</p>
<p>
然后配置根目录和admin下的 .htaccess 文件 <br>
</p>
<h3>二、Nginx</h3>
<p>
location / {<br>
&nbsp;&nbsp;&nbsp;&nbsp;try_files $uri $uri/ /index.html;<br>
&nbsp;&nbsp;&nbsp;&nbsp;#Hide index.php<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!-e $request_filename) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rewrite ^/(.*) /index.php last;<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
}<br>
<br>
location /admin/ {<br>
&nbsp;&nbsp;&nbsp;&nbsp;try_files $uri $uri/ /index.html;<br>
&nbsp;&nbsp;&nbsp;&nbsp;#Hide index.php<br>
&nbsp;&nbsp;&nbsp;&nbsp;if (!-e $request_filename) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rewrite ^/admin/(.*) /admin/index.php last;<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
}<br>
</p>
<p>注意：如果ci无法读取真实URL地址，需要配置 admin/config/config.php 文件，如：$config['base_url'] = 'http://www.ksphp.com/admin';</p>
</div>

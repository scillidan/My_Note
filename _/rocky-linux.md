## CDN

个人网站上，常见的是图文。如果你已经预处理过媒体文件，并且使用CDN节点来访问它们，以及Web字体、部分CSS和JS脚本，即使是低配的VPS，也可以获得十分高的速度。但是较流行的做法是将大型的音频、视频等媒体文件上传到各个平台。

1. 云产品 → 对象存储 → 存储桶列表 → 创建存储桶 ... 公有读私有写
2. 内容分发网络 → 域名管理 → 添加域名 ... 静态加速/流媒体点播加速 → COS源
    1. 高级配置 → 宽带封顶配置 → 访问闸值
3. DNS解析 → 添加记录 → 记录类型CNAME...

coscli config
coscli -c .yaml sync ./ cos://.cos/ -r
https://console.cloud.tencent.com/cos5/bucket
https://console.cloud.tencent.com/cam/capi

控制台 → 访问管理 → 用户/用户列表 → 新建用户 → 快速创建 ... 成功新建用户 → 下载CSV文件
打开访客窗口或无痕窗口 → 登录界面/子账号 → 腾讯云 → 右上角 → 填写账号ID, 初始密码 → 重置密码 → 完善关联手机信息
主账号 → 控制台 → 访问管理 → 用户/用户设置 → 目标子账号 → 授权 → 搜索`COS`并全选条目 → 搜索`CDN`并全选条目 → 确定
子账号 → 控制台 → 访问管理 → API密钥管理 → 新建密钥 → 创建SecretKey → 下载CSV文件 → 我已知晓并保存SecretKey (On) → 确定

主账号 → 控制台 → 内容分发网路 → 添加域名 → 域名配置 → 验证方法 ... 验证

```
加速区域 全球
加速类型 CDN网页小文件
    当你文件类型是html, css, js等网页文件、Web字体、vtt字幕等时，选择此类型。这只是经验，不是标准。
    是音频、视频文件时，选择CDN音视频点播
源站类型 COS源
源站类型 目标COS桶
```

下一步 ... 提升访问性能 → 智能压缩 (Off)
下一步 → 防止费用超额 → 配置封顶配置 → 生效下方配置项 (On) → 新增规则:

```
统计类型 累计用量
统计周期 每小时
流量封顶 流量封顶 10GB
解封时间 永不解封
告警阈值 开启
```

```
统计类型 瞬间用量
封顶配置 流量封顶 1536MB(1.5GB)
解封时间 永不解封
```
... 提交所有配置

配置CNAME → 一键配置 → 确定


如果你在重启`httpd`或者设置SSL时出错，通常跟`/etc/httpd/conf/httpd.conf`和`/etc/httpd/sites-available/`里的站点配置有关

按提示`systemctl status httpd.service`后，可尝试删除报错的文件，然后重试。
步骤被分割得细碎，如果你在某个地方卡壳，可以向前退回到某个还没报错节点

## HTTPS

1. 云产品 → SSL证书 → 我的证书 → 申请
2. 内容分发网络 → 域名管理 → 管理 → HTTPS配置 → 配置证书

## CORS

可用于CDN字体服务等。详情请参考[设置静态网站](https://cloud.tencent.com/document/product/436/14984)、[设置跨域访问](https://cloud.tencent.com/document/product/436/13318)。大致流程为：
1. 新建储存桶，用于静态网站
    1. 储存桶 → 安全管理 → 跨域访问CORS设置 → 添加规则
    2. 上传网页字体文体到储存桶
2. 给储存桶设置CDN加速
    1. 设置HTTP响应头配置
3. 在`.css`文件中调用字体文件的网址，进行测试

## PM2

以部署[excalith/excalith-start-page](https://github.com/excalith/excalith-start-page)为例。安装依赖项：

```bash
dnf install nodejs -y
npm install --global yarn
yarn global add pm2
```

克隆库：

```bash
cd /var/www
git clone https://github.com/excalith/excalith-start-page
cd excalith-start-page
```

安装`package.json`中的依赖项：

```bash
yarn
```

README.md中提到了`yarn dev`命令。这里用`package.json`中写的另外的`script`：

```bash
yarn build
yarn start
```

但我在运行时遇到了`error`信息，根据这个回答[error Delete `··` prettier/prettie](https://github.com/prettier/eslint-plugin-prettier/issues/219#issuecomment-835770395)，需要先：

```bash
yarn lint --fix
```

这次运行成功后。按`Ctrl + C`退出。

```bash
pm2 start npm --name "excalith-start-page" --watch -- start
```

```bash
rsync -r "/cygdrive/d/yourpath/excalith-start-page/" "root@yourvpsip:/var/www/excalith-start-page" --include={'.*'} --exclude={'.github','.next/','build/','node_modules/','.git'}
```

这里用子域名来访问。新建一个VirtualHost（虚拟主服务器）配置

```bash
vi /etc/httpd/conf.d/sub.example.com.conf
```

```bash title="sub.example.com.conf"
<VirtualHost *:80>
  ServerName www.sub.example.com
  ServerAlias sub.example.com

  ErrorLog /var/log/httpd/sub.example.com-error.log
  CustomLog /var/log/httpd/sub.example.com-access.log combined
  ProxyPreserveHost On
  ProxyPass / http://localhost:3000/
  ProxyPassReverse / http://localhost:3000/
</VirtualHost>
```

↪ †	[How to deploy Next.js website on Apache webserver](https://stackoverflow.com/questions/74681648)

Todo:

```sh
vi package.json
```

``` package.json linenums="7"
		"start": "next start",
```

To

```json title="package.json" linenums="7"
		"start": "next start -p 3100",
```

↪ [How to specify a port number for pm2](https://stackoverflow.com/questions/31502351/how-to-specify-a-port-number-for-pm2)
↪ [How to change the port in nextjs?](https://medium.com/frontendweb/how-to-change-port-in-nextjs-1b99930bb81f)

## VNC

```bash
sudo dnf update -y
sudo dnf install -y epel-release
sudo dnf groupinstall -y "Xfce" "base-x"
sudo systemctl set-default graphical
sudo reboot
```

```bash
sudo dnf install tigervnc-server
sudo adduser vncuser
sudo passwd vncuser
sudo su - vncuser
```

```bash
sudo dnf install firewalld -y
sudo systemctl enable firewalld
sudo systemctl start firewalld
sudo firewall-cmd --state
firewall-cmd --zone=public --permanent --add-service=vnc-server
firewall-cmd --reload
```

```bash
su vncuser
vim ~/.vnc/config
```

``` title="config"
session=xfce
geometry=1280x800
# localhost
# alwaysshared
```

```bash
sudo systemctl start firewalld
```

If you need to kill the process:

```bash
pf -fu vncuser
kill -9 vncuser
```

↪ [Install and Configure VNC Server on Rocky Linux 8](https://techviewleo.com/install-and-configure-vnc-server-on-rocky-linux)  
↪ [How To Set Up a Firewall Using firewalld on Rocky Linux 8](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-rocky-linux-8)

on PC:

```bash
scoop install tightvnc
tvnviewer vpsip::5901 -password=yourpassword
```

↪ [How to Install VNC Server on Rocky Linux](https://www.howtoforge.com/how-to-install-vnc-server-on-rocky-linux/)
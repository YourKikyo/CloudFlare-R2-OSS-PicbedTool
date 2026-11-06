# README

## 这是什么？

一个**设计精美**，用HTML实现的**自动压缩图片、转换为webp格式、上传至CloudFlare R2 OSS**的小工具。如果你使用R2当图床来**写博客**，那么这个工具会很方便。

## 使用方法

双击 **index.html** 后点 **设置** 配置CloudFlare R2。

### 1. 建 API 令牌

Cloudflare 控制台 → **R2** → 右侧 **Manage R2 API Tokens** → **Create API token**

- Permissions 选 **Object Read & Write**
- 建议 Specify bucket 只勾选你的图床桶

拿到 **Access Key ID**、**Secret Access Key**（只显示一次）和 **Account ID**。

### 2. 拿公开域名

R2 → 桶 → **Settings** → **Public access**

- 绑了自定义域名：`https://img.你的域名.com`（**推荐**，r2.dev 有速率限制）
- 只有 r2.dev：`https://pub-xxxxxxxx.r2.dev`

### 3. 填进页面

打开 `index.html`，首次会自动弹出设置面板。

## 它做了什么

拖进去的每一张图，浏览器会在**本机**完成这些处理，然后再上传：

1. 按 EXIF 方向摆正（手机竖拍照片不会躺倒）
2. 长边超过 **1280px** 的等比缩小
3. 统一编码为 **WebP，质量 0.72**
4. 上传到你的 R2，返回公开 URL

处理全在你的电脑上跑，图片不会先经过任何中转服务器。

### 实测压缩效果

拿一张 `2610*1628` 分辨率的游戏截图做基准：

|          | 体积     | 说明                 |
| -------- | -------- | -------------------- |
| 原图 JPG | 7.27 MB  | 100%                 |
| 工具输出 | 135.4 KB | 1.8%，省下 **98.2%** |


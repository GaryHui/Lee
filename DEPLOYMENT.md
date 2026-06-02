# 李家优品网站手动更新与部署文档

这份文档用于在无法连接 Codex 时，手动更新并部署 `greenzo.online` 网站。

适用环境：Windows PowerShell  
项目目录：`E:\2026\Lee`  
GitHub 仓库：`https://github.com/GaryHui/Lee.git`  
Vercel 项目：`garyhuis-projects/lee`  
线上域名：

- `https://greenzo.online`
- `https://www.greenzo.online`

## 1. 进入项目目录

打开 PowerShell，执行：

```powershell
cd E:\2026\Lee
```

确认当前仓库状态：

```powershell
git status
```

如果看到 `On branch main`，说明位置正确。

## 2. 更新网站内容

常用文件：

- `index.html`：页面结构、标题、文案、二维码说明、产品展示内容。
- `styles.css`：页面视觉样式、颜色、布局、手机端适配。
- `assets/`：logo、二维码、产品图片。
- `vercel.json`：Vercel 缓存配置，一般不要动。

修改完成后，可以本地预览：

```powershell
npx serve .
```

如果提示端口，例如 `http://localhost:3000`，在浏览器打开查看。

不用 `serve` 也可以直接部署，但建议先本地看一下。

## 3. 提交到 GitHub

查看改动：

```powershell
git status
```

添加所有改动：

```powershell
git add .
```

提交：

```powershell
git commit -m "Update website"
```

推送到 GitHub：

```powershell
git push
```

如果提示登录 GitHub，按终端提示完成登录即可。

## 4. 手动部署到 Vercel

在项目目录执行：

```powershell
npx vercel --prod --yes
```

部署成功后，终端会输出类似：

```text
Production  https://lee-xxxx-garyhuis-projects.vercel.app
```

复制这个新的部署地址，下面用 `<部署地址>` 表示。

示例：

```text
https://lee-my9gvggea-garyhuis-projects.vercel.app
```

## 5. 绑定正式域名

部署后，把两个正式域名指向新部署。

```powershell
npx vercel alias set <部署地址> greenzo.online
```

```powershell
npx vercel alias set <部署地址> www.greenzo.online
```

示例：

```powershell
npx vercel alias set lee-my9gvggea-garyhuis-projects.vercel.app greenzo.online
npx vercel alias set lee-my9gvggea-garyhuis-projects.vercel.app www.greenzo.online
```

看到 `Success!` 就说明域名已经指向新版本。

## 6. 验证线上网站

打开：

- `https://greenzo.online`
- `https://www.greenzo.online`

确认：

- 页面能打开。
- 标题、文案、图片是最新的。
- 二维码能正常显示。
- 手机端能正常浏览。

也可以在 PowerShell 做简单检查：

```powershell
curl https://greenzo.online
```

如果返回 HTML 内容，说明网站在线。

## 7. 更换产品图片

把新图片放到 `assets/` 目录。

建议命名方式：

```text
assets/product-name.jpg
```

然后在 `index.html` 中找到对应图片：

```html
<img src="assets/sea-monster-color-pack.jpg" ...>
```

替换成新文件名：

```html
<img src="assets/product-name.jpg" ...>
```

图片建议：

- 单张尽量控制在 `50KB-150KB`。
- 优先使用 `.jpg` 或 `.webp`。
- 图片宽度控制在 `760px-1000px` 通常足够。
- 不要上传几 MB 的原图，会影响手机打开速度。

## 8. 常见问题

### `git push` 失败

先确认网络和 GitHub 登录状态。

```powershell
git status
git remote -v
```

如果提示认证失败，按 GitHub 登录提示重新登录。

### `npx vercel --prod --yes` 失败

重新登录 Vercel：

```powershell
npx vercel login
```

登录后再部署：

```powershell
npx vercel --prod --yes
```

### 域名没有更新

重新执行 alias：

```powershell
npx vercel alias set <部署地址> greenzo.online
npx vercel alias set <部署地址> www.greenzo.online
```

然后等待 1-3 分钟再刷新浏览器。

### 浏览器看到旧页面

可能是缓存。

处理方式：

- 按 `Ctrl + F5` 强制刷新。
- 手机浏览器退出后重新打开。
- 换一个浏览器或无痕窗口查看。

## 9. 推荐完整流程

每次手动更新，按这个顺序走：

```powershell
cd E:\2026\Lee
git status
git add .
git commit -m "Update website"
git push
npx vercel --prod --yes
npx vercel alias set <部署地址> greenzo.online
npx vercel alias set <部署地址> www.greenzo.online
```

最后打开 `https://greenzo.online` 检查。


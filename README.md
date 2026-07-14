# 林镇伟｜中文 GitHub Pages 简历

使用 Vue 3 + Vite 制作的中文个人简历网站，内容聚焦 AI 产品、AI Workflow、AI Agent、企业智能自动化和低代码平台。

## 本地运行

```bash
npm install
npm run dev
```

## 修改简历内容

主要文字集中在：

```text
src/data/resume.js
```

页面结构在：

```text
src/App.vue
```

样式在：

```text
src/style.css
```

## 部署到 GitHub Pages

1. 在 GitHub 新建一个仓库，例如 `resume`。
2. 将本项目全部文件上传到仓库，并推送到 `main` 分支。
3. 打开仓库 `Settings` → `Pages`。
4. 在 `Build and deployment` 的 `Source` 中选择 `GitHub Actions`。
5. 等待 Actions 中的部署任务完成。

网站地址通常是：

```text
https://你的GitHub用户名.github.io/resume/
```

如果仓库名是 `你的GitHub用户名.github.io`，地址则是：

```text
https://你的GitHub用户名.github.io/
```

## 打印或保存 PDF

网页中的“打印 / 保存 PDF”会调用浏览器打印功能，可直接选择“另存为 PDF”。

# Tech Blog

个人技术博客,基于 GitHub Pages 纯静态托管。

## 结构

```
index.html      博客首页(文章列表)
pi/             Pi · 我的终端 AI 编排者(单文件展示页)
```

## 如何添加一篇文章

1. 新建目录 `<slug>/`,放一个 `index.html`(或 `index.md`,需要开 Jekyll 才支持 Markdown 渲染)
2. 在根目录 `index.html` 的 `.posts` 列表里加一条(日期 + 标题 + 摘要 + 链接)
3. push 到 `main` 分支,GitHub Pages 自动部署

## 部署

GitHub Pages → Deploy from a branch → `main` / root。仓库根目录有 `.nojekyll`,跳过 Jekyll 构建,HTML 原样托管。

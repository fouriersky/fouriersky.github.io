# 快速参考 / Quick Reference

本文档提供常用命令和操作的快速参考。

This document provides quick reference for common commands and operations.

---

## 🚀 启动开发 / Start Development

### 方法一：推荐 / Method 1: Recommended
```bash
bash tools/run.sh
```

### 方法二 / Method 2
```bash
bundle exec jekyll serve
```

### 查看草稿 / View Drafts
```bash
bundle exec jekyll serve --drafts
```

### 指定端口 / Specify Port
```bash
bundle exec jekyll serve --port 4001
```

### 生产模式 / Production Mode
```bash
JEKYLL_ENV=production bundle exec jekyll serve
```

---

## 📝 写文章 / Writing Posts

### 创建新文章 / Create New Post
```bash
# 文件名格式 / File name format: YYYY-MM-DD-title.md
touch _posts/2026-01-11-my-new-post.md
```

### 文章模板 / Post Template
```yaml
---
title: 文章标题 / Post Title
date: 2026-01-11 14:00:00 +0800
categories: [分类1, 分类2] / [Category1, Category2]
tags: [标签1, 标签2] / [tag1, tag2]
---

文章内容... / Content...
```

### 创建草稿 / Create Draft
```bash
# 不需要日期前缀 / No date prefix needed
touch _drafts/my-draft-post.md
```

---

## 🛠️ 构建和测试 / Build & Test

### 仅构建 / Build Only
```bash
bundle exec jekyll build
```

### 生产环境构建 / Production Build
```bash
JEKYLL_ENV=production bundle exec jekyll build
```

### 运行测试 / Run Tests
```bash
bash tools/test.sh
```

### 清理构建文件 / Clean Build
```bash
bundle exec jekyll clean
```

---

## 📦 依赖管理 / Dependency Management

### 安装依赖 / Install Dependencies
```bash
bundle install
```

### 更新依赖 / Update Dependencies
```bash
bundle update
```

### 查看过时的包 / Check Outdated Gems
```bash
bundle outdated
```

### 查看 Jekyll 版本 / Check Jekyll Version
```bash
bundle exec jekyll -v
```

---

## 🖼️ 添加图片 / Adding Images

### 图片位置 / Image Location
```
assets/img/your-image.jpg
```

### 在文章中引用 / Reference in Posts
```markdown
![描述 / Description](/assets/img/your-image.jpg)
```

---

## 🎨 自定义 / Customization

### 头像 / Avatar
```yaml
# _config.yml
avatar: /assets/img/avatar/avatar.jpg
```

### 网站标题 / Site Title
```yaml
# _config.yml
title: Your Site Title
tagline: Your Tagline
```

### 语言 / Language
```yaml
# _config.yml
lang: zh-CN  # 中文
lang: en     # English
```

---

## 🔍 常用路径 / Common Paths

| 中文 | English | Path |
|------|---------|------|
| 文章 | Posts | `_posts/` |
| 草稿 | Drafts | `_drafts/` |
| 页面 | Pages | `_tabs/` |
| 配置 | Config | `_config.yml` |
| 图片 | Images | `assets/img/` |
| 数据 | Data | `_data/` |

---

## 🐛 故障排除 / Troubleshooting

### 重启开发服务器 / Restart Server
```bash
# Ctrl+C 停止 / Stop
# 然后重新运行 / Then run again
bash tools/run.sh
```

### 清理并重建 / Clean & Rebuild
```bash
bundle exec jekyll clean
bundle exec jekyll build
```

### 重新安装依赖 / Reinstall Dependencies
```bash
rm -rf vendor/bundle
bundle install
```

### 检查端口占用 / Check Port Usage
```bash
# macOS/Linux
lsof -i :4000

# Windows
netstat -ano | findstr :4000
```

---

## 📚 Front Matter 选项 / Front Matter Options

### 基础选项 / Basic Options
```yaml
---
title: 标题 / Title
date: 2026-01-11 14:00:00 +0800
categories: [分类] / [Category]
tags: [标签] / [Tags]
---
```

### 高级选项 / Advanced Options
```yaml
---
title: 标题 / Title
date: 2026-01-11 14:00:00 +0800
categories: [分类] / [Category]
tags: [标签] / [Tags]
author: 作者名 / Author Name
image: /path/to/image.jpg
pin: true              # 置顶 / Pin post
toc: false            # 隐藏目录 / Hide TOC
comments: false       # 关闭评论 / Disable comments
math: true            # 启用数学公式 / Enable math
mermaid: true         # 启用 Mermaid 图表 / Enable Mermaid
---
```

---

## 🌐 访问地址 / URLs

- 本地开发 / Local Dev: http://localhost:4000
- 备用端口 / Alternative: http://127.0.0.1:4000
- 生产环境 / Production: 见 `_config.yml` 中的 `url` 配置 / See `url` in `_config.yml`

---

## 💡 小技巧 / Tips

1. **修改 `_config.yml` 后必须重启服务器** / Must restart server after modifying `_config.yml`
2. **使用 Dev Container 最简单** / Using Dev Container is easiest
3. **草稿不会发布到生产环境** / Drafts won't be published to production
4. **图片建议使用相对路径** / Use relative paths for images
5. **提交前本地测试** / Test locally before committing

---

## 📖 更多资源 / More Resources

- 详细中文指南 / Detailed Chinese Guide: [本地开发指南.md](./本地开发指南.md)
- Detailed English Guide: [LOCAL_DEVELOPMENT.md](./LOCAL_DEVELOPMENT.md)
- Jekyll 文档 / Jekyll Docs: https://jekyllrb.com/docs/
- Chirpy 主题 / Chirpy Theme: https://github.com/cotes2020/jekyll-theme-chirpy/

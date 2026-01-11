# 常见问题解决方案 / Troubleshooting Guide

本文档收集了本地开发过程中常见的问题和解决方案。

This document collects common issues and solutions during local development.

---

## 🔧 安装问题 / Installation Issues

### 问题 1: `bundle install` 失败 / Issue 1: `bundle install` fails

#### 症状 / Symptoms
```
ERROR: While executing gem...
Permission denied
```

#### 解决方案 / Solutions

**方案 A: 使用用户级 gem 目录（推荐）/ Use user-level gem directory (recommended)**
```bash
# Linux/macOS
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# 重新安装 / Reinstall
gem install bundler
bundle install
```

**方案 B: 使用 Dev Container（最简单）/ Use Dev Container (easiest)**
- 无需配置 Ruby 环境 / No Ruby environment configuration needed
- 参见主文档 / See main documentation

---

### 问题 2: Ruby 版本过低 / Issue 2: Ruby version too old

#### 症状 / Symptoms
```
Your Ruby version is X.X.X, but your Gemfile specified >= 3.0
```

#### 解决方案 / Solutions

**macOS:**
```bash
brew install ruby@3.3
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
ruby -v  # 确认版本 / Verify version
```

**Ubuntu/Debian:**
```bash
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:brightbox/ruby-ng
sudo apt-get update
sudo apt-get install ruby3.3 ruby3.3-dev
```

**Windows:**
- 卸载旧版本 / Uninstall old version
- 下载并安装 Ruby+Devkit 3.3 from https://rubyinstaller.org/

---

### 问题 3: Windows 上缺少开发工具 / Issue 3: Missing development tools on Windows

#### 症状 / Symptoms
```
ERROR: Failed to build gem native extension
```

#### 解决方案 / Solution
```bash
# 运行 RubyInstaller 的开发工具安装程序 / Run RubyInstaller's devkit installer
ridk install

# 选择选项 3: MSYS2 and MINGW development toolchain
# Select option 3: MSYS2 and MINGW development toolchain
```

---

## 🚀 运行问题 / Runtime Issues

### 问题 4: 端口 4000 被占用 / Issue 4: Port 4000 in use

#### 症状 / Symptoms
```
Address already in use - bind(2) for 127.0.0.1:4000
```

#### 解决方案 / Solutions

**方案 A: 使用其他端口 / Use different port**
```bash
bundle exec jekyll serve --port 4001
```

**方案 B: 查找并关闭占用进程 / Find and kill the process**
```bash
# macOS/Linux
lsof -i :4000
kill -9 <PID>

# Windows
netstat -ano | findstr :4000
taskkill /PID <PID> /F
```

---

### 问题 5: 修改 `_config.yml` 后网站没有更新 / Issue 5: Changes to `_config.yml` not reflected

#### 症状 / Symptoms
配置修改后网站仍显示旧配置 / Site still shows old configuration after changes

#### 解决方案 / Solution
`_config.yml` 的修改需要重启服务器 / Changes to `_config.yml` require server restart

```bash
# 按 Ctrl+C 停止服务器 / Press Ctrl+C to stop server
# 然后重新启动 / Then restart
bash tools/run.sh
```

---

### 问题 6: 其他文件修改后网站没有更新 / Issue 6: Changes to other files not reflected

#### 症状 / Symptoms
修改 Markdown 文件后网站没有更新 / Markdown changes not showing up

#### 解决方案 / Solutions

**方案 A: 检查文件名格式 / Check file name format**
- 文章必须以 `YYYY-MM-DD-` 开头 / Posts must start with `YYYY-MM-DD-`
- 例如: `2026-01-11-my-post.md`

**方案 B: 检查 Front Matter / Check Front Matter**
```yaml
---
title: 标题必填 / Title required
date: 2026-01-11 14:00:00 +0800  # 日期必填 / Date required
---
```

**方案 C: 清理并重建 / Clean and rebuild**
```bash
bundle exec jekyll clean
bash tools/run.sh
```

---

### 问题 7: 数学公式不显示 / Issue 7: Math formulas not displaying

#### 症状 / Symptoms
LaTeX 公式显示为纯文本 / LaTeX formulas show as plain text

#### 解决方案 / Solution
在文章的 Front Matter 中启用数学支持 / Enable math support in post Front Matter

```yaml
---
title: 我的文章 / My Post
math: true  # 添加这一行 / Add this line
---
```

---

### 问题 8: Mermaid 图表不显示 / Issue 8: Mermaid diagrams not displaying

#### 症状 / Symptoms
Mermaid 代码块显示为纯文本 / Mermaid code blocks show as plain text

#### 解决方案 / Solution
在文章的 Front Matter 中启用 Mermaid / Enable Mermaid in post Front Matter

```yaml
---
title: 我的文章 / My Post
mermaid: true  # 添加这一行 / Add this line
---
```

---

## 🐳 Dev Container 问题 / Dev Container Issues

### 问题 9: Dev Container 构建失败 / Issue 9: Dev Container build fails

#### 症状 / Symptoms
容器无法启动 / Container fails to start

#### 解决方案 / Solutions

**方案 A: 重建容器 / Rebuild container**
```
F1 → Dev Containers: Rebuild Container
```

**方案 B: 清理 Docker / Clean Docker**
```bash
# 清理所有停止的容器 / Clean all stopped containers
docker container prune

# 清理未使用的镜像 / Clean unused images
docker image prune
```

**方案 C: 检查 Docker 资源 / Check Docker resources**
- 确保 Docker Desktop 有足够的内存（至少 4GB）/ Ensure Docker Desktop has enough memory (at least 4GB)
- 增加磁盘空间限制 / Increase disk space limit

---

### 问题 10: Dev Container 中无法访问网站 / Issue 10: Cannot access site in Dev Container

#### 症状 / Symptoms
服务器运行但无法在浏览器中访问 / Server running but can't access in browser

#### 解决方案 / Solutions

**方案 A: 检查端口转发 / Check port forwarding**
- 在 VS Code 中打开"端口"标签 / Open "PORTS" tab in VS Code
- 确认端口 4000 已转发 / Confirm port 4000 is forwarded
- 点击端口号打开浏览器 / Click port number to open browser

**方案 B: 使用正确的主机地址 / Use correct host address**
```bash
bash tools/run.sh --host 0.0.0.0
```

---

## 📦 依赖问题 / Dependency Issues

### 问题 11: 某个 gem 安装失败 / Issue 11: Specific gem fails to install

#### 症状 / Symptoms
```
ERROR: Failed to build gem native extension
```

#### 解决方案 / Solutions

**方案 A: 安装编译工具 / Install build tools**

**macOS:**
```bash
xcode-select --install
```

**Ubuntu/Debian:**
```bash
sudo apt-get install build-essential
```

**Windows:**
```bash
ridk install
# 选择选项 3 / Select option 3
```

**方案 B: 使用 Dev Container / Use Dev Container**
- 所有工具已预装 / All tools pre-installed

---

### 问题 12: `webrick` 相关错误 / Issue 12: `webrick` related errors

#### 症状 / Symptoms
```
cannot load such file -- webrick
```

#### 解决方案 / Solution
Ruby 3.0+ 需要显式添加 webrick / Ruby 3.0+ requires explicit webrick

```bash
bundle add webrick
```

---

## 🔐 权限问题 / Permission Issues

### 问题 13: 文件权限错误 / Issue 13: File permission errors

#### 症状 / Symptoms
```
Permission denied @ rb_sysopen
```

#### 解决方案 / Solutions

**方案 A: 修复文件权限 / Fix file permissions**
```bash
# macOS/Linux
chmod -R u+w .
```

**方案 B: 清理并重新生成 / Clean and regenerate**
```bash
bundle exec jekyll clean
rm -rf _site .jekyll-cache
bundle exec jekyll build
```

---

## 🌐 网络问题 / Network Issues

### 问题 14: 无法下载 gem / Issue 14: Cannot download gems

#### 症状 / Symptoms
```
Could not fetch specs from https://rubygems.org/
```

#### 解决方案 / Solutions

**方案 A: 检查网络连接 / Check network connection**
```bash
ping rubygems.org
```

**方案 B: 使用镜像源（中国用户）/ Use mirror (for users in China)**
```bash
# 临时使用清华镜像 / Temporarily use Tsinghua mirror
bundle config mirror.https://rubygems.org https://mirrors.tuna.tsinghua.edu.cn/rubygems

# 如需恢复默认源 / To revert to default source
bundle config --delete mirror.https://rubygems.org
```

**注意:** 使用前请确认镜像源可用 / **Note:** Verify mirror availability before use

**方案 C: 配置代理 / Configure proxy**
```bash
# HTTP 代理 / HTTP proxy
export http_proxy=http://proxy.example.com:8080
export https_proxy=http://proxy.example.com:8080

# SOCKS5 代理 / SOCKS5 proxy
export http_proxy=socks5://127.0.0.1:1080
export https_proxy=socks5://127.0.0.1:1080
```

---

## 🎨 样式问题 / Styling Issues

### 问题 15: 样式显示不正确 / Issue 15: Styles not displaying correctly

#### 症状 / Symptoms
网站显示但样式缺失或错误 / Site displays but styles are missing or wrong

#### 解决方案 / Solutions

**方案 A: 清理缓存 / Clear cache**
```bash
bundle exec jekyll clean
rm -rf _site .jekyll-cache .sass-cache
bundle exec jekyll build
```

**方案 B: 检查 baseurl 配置 / Check baseurl configuration**
```yaml
# _config.yml
baseurl: ""  # 本地开发应为空 / Should be empty for local development
             # 如果部署到子目录，例如 /blog，则生产环境需设置
             # For production on subdirectory like /blog, set accordingly
```

**注意:** 本项目部署在根目录，baseurl 应保持为空 / **Note:** This project deploys to root, baseurl should remain empty

**方案 C: 硬刷新浏览器 / Hard refresh browser**
- Windows/Linux: `Ctrl + Shift + R`
- macOS: `Cmd + Shift + R`

---

## 📝 内容问题 / Content Issues

### 问题 16: 中文字符显示为乱码 / Issue 16: Chinese characters display as gibberish

#### 症状 / Symptoms
中文显示为 `????` 或其他乱码 / Chinese displays as `????` or gibberish

#### 解决方案 / Solution
确保文件使用 UTF-8 编码 / Ensure files use UTF-8 encoding

**VS Code:**
- 右下角点击编码 / Click encoding in bottom right
- 选择 "Save with Encoding" → "UTF-8"

---

### 问题 17: 文章不显示在首页 / Issue 17: Post doesn't show on homepage

#### 症状 / Symptoms
文章已创建但不出现在首页 / Post created but doesn't appear on homepage

#### 检查清单 / Checklist

1. **文件名格式** / **File name format**
   ```
   ✅ 正确 / Correct: _posts/2026-01-11-my-post.md
   ❌ 错误 / Wrong: _posts/my-post.md
   ```

2. **日期不在未来** / **Date not in future**
   ```yaml
   # 文章日期不能超过当前时间 / Post date cannot be in the future
   date: 2026-01-11 14:00:00 +0800
   ```

3. **Front Matter 格式正确** / **Front Matter format correct**
   ```yaml
   ---
   title: 标题  # 必需 / Required
   date: 2026-01-11 14:00:00 +0800  # 必需 / Required
   ---
   ```

4. **文件位置正确** / **File location correct**
   - 放在 `_posts/` 目录 / Place in `_posts/` directory
   - 不在 `_drafts/` 目录 / Not in `_drafts/` directory

---

## 💻 性能问题 / Performance Issues

### 问题 18: 构建速度很慢 / Issue 18: Build is very slow

#### 症状 / Symptoms
`jekyll build` 或 `jekyll serve` 需要很长时间 / `jekyll build` or `jekyll serve` takes very long

#### 解决方案 / Solutions

**方案 A: 使用增量构建 / Use incremental build**
```bash
bundle exec jekyll serve --incremental
```

**方案 B: 排除不必要的文件 / Exclude unnecessary files**
```yaml
# _config.yml
exclude:
  - vendor
  - node_modules
  - .git
```

**方案 C: 限制文章数量（开发时）/ Limit posts (during development)**
```bash
bundle exec jekyll serve --limit_posts 10
```

---

## 🆘 仍然无法解决？/ Still Cannot Resolve?

如果上述方案都无法解决您的问题：/ If none of the above solutions work:

1. **查看详细错误信息** / **Check detailed error messages**
   ```bash
   bundle exec jekyll serve --trace --verbose
   ```

2. **搜索错误信息** / **Search for error messages**
   - Google / 百度搜索完整的错误信息 / Search complete error message
   - 查看 Jekyll 或 Chirpy 的 Issues / Check Jekyll or Chirpy Issues

3. **寻求帮助** / **Ask for help**
   - [Jekyll 论坛](https://talk.jekyllrb.com/)
   - [Chirpy GitHub Issues](https://github.com/cotes2020/jekyll-theme-chirpy/issues)
   - [Stack Overflow](https://stackoverflow.com/questions/tagged/jekyll)

4. **提供完整信息** / **Provide complete information**
   - 操作系统和版本 / OS and version
   - Ruby 版本 (`ruby -v`)
   - 完整的错误信息 / Complete error message
   - 尝试过的解决方案 / Solutions attempted

---

## 📚 相关文档 / Related Documentation

- [本地开发指南.md](./本地开发指南.md) - 完整安装指南 / Complete installation guide
- [LOCAL_DEVELOPMENT.md](./LOCAL_DEVELOPMENT.md) - English installation guide
- [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - 快速参考 / Quick reference
- [Jekyll 故障排除](https://jekyllrb.com/docs/troubleshooting/)
- [Chirpy 文档](https://github.com/cotes2020/jekyll-theme-chirpy/wiki)

---

## 💡 预防性建议 / Preventive Tips

1. **使用 Dev Container** / **Use Dev Container**
   - 最稳定可靠的方式 / Most stable and reliable way
   - 避免大多数环境问题 / Avoids most environment issues

2. **定期更新依赖** / **Regularly update dependencies**
   ```bash
   bundle update
   ```

3. **提交前测试** / **Test before committing**
   ```bash
   JEKYLL_ENV=production bundle exec jekyll build
   ```

4. **保持环境整洁** / **Keep environment clean**
   ```bash
   bundle exec jekyll clean
   ```

5. **使用版本控制** / **Use version control**
   - 定期提交 / Commit regularly
   - 便于回滚 / Easy to rollback

---

祝您顺利解决问题！/ Hope this helps you resolve issues!

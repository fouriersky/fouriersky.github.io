# Local Development Guide

This document explains how to edit and preview this Jekyll blog website in your local environment.

## About This Project

This website is built using the [Jekyll](https://jekyllrb.com/) static site generator with the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/) theme. Jekyll is Ruby-based, which may differ from common Node.js frontend projects, so the development environment setup is slightly different.

## Development Environment Requirements

### Required Software

1. **Ruby** (version >= 3.0)
2. **RubyGems** (Ruby package manager)
3. **Bundler** (Ruby dependency management tool)
4. **Git**

## Method 1: Using VS Code Dev Container (Recommended)

This is the easiest method and doesn't require installing Ruby locally.

### Prerequisites
- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- VS Code Extension: [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/fouriersky/fouriersky.github.io.git
   cd fouriersky.github.io
   ```

2. **Open in VS Code**
   ```bash
   code .
   ```

3. **Use Dev Container**
   - VS Code will detect the `.devcontainer` folder
   - Click "Reopen in Container" in the popup notification
   - Or press `F1` and type "Dev Containers: Reopen in Container"

4. **Wait for container to build**
   - First build may take a few minutes
   - Container will automatically install all dependencies

5. **Start development server**
   ```bash
   bash tools/run.sh
   ```

6. **Access the website**
   - Open browser at http://localhost:4000
   - Changes to files will automatically regenerate the site

## Method 2: Local Ruby Installation

If you prefer not to use Docker, you can install Ruby locally.

### macOS

1. **Install Ruby (using Homebrew)**
   ```bash
   # Install Homebrew (if not already installed)
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   
   # Install Ruby
   brew install ruby@3.3
   
   # Add to PATH (use path shown by Homebrew)
   echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
   source ~/.zshrc
   ```

2. **Verify installation**
   ```bash
   ruby -v  # Should show Ruby 3.x
   gem -v   # Should show RubyGems version
   ```

3. **Clone repository and install dependencies**
   ```bash
   git clone https://github.com/fouriersky/fouriersky.github.io.git
   cd fouriersky.github.io
   
   # Install Bundler
   gem install bundler
   
   # Install project dependencies
   bundle install
   ```

4. **Start development server**
   ```bash
   bash tools/run.sh
   # Or use Jekyll command directly
   bundle exec jekyll serve
   ```

5. **Access the website**
   - Open browser at http://127.0.0.1:4000

### Windows

1. **Install Ruby**
   - Download and install [RubyInstaller](https://rubyinstaller.org/) (recommend Ruby+Devkit version)
   - During installation, select "Add Ruby executables to your PATH"
   - After installation, run `ridk install` and select MSYS2 toolchain installation

2. **Verify installation**
   ```bash
   ruby -v
   gem -v
   ```

3. **Clone repository and install dependencies**
   ```bash
   git clone https://github.com/fouriersky/fouriersky.github.io.git
   cd fouriersky.github.io
   
   gem install bundler
   bundle install
   ```

4. **Start development server**
   ```bash
   bundle exec jekyll serve
   ```

5. **Access the website**
   - Open browser at http://127.0.0.1:4000

### Linux (Ubuntu/Debian)

1. **Install Ruby and dependencies**
   ```bash
   sudo apt-get update
   sudo apt-get install -y ruby-full build-essential zlib1g-dev
   
   # Configure gem installation path (avoid using sudo)
   echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
   echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
   echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
   source ~/.bashrc
   ```

2. **Install Bundler**
   ```bash
   gem install bundler
   ```

3. **Clone repository and install dependencies**
   ```bash
   git clone https://github.com/fouriersky/fouriersky.github.io.git
   cd fouriersky.github.io
   bundle install
   ```

4. **Start development server**
   ```bash
   bash tools/run.sh
   # Or
   bundle exec jekyll serve
   ```

5. **Access the website**
   - Open browser at http://127.0.0.1:4000

## Daily Usage Guide

### Writing New Posts

1. Create a new file in `_posts` directory with format: `YYYY-MM-DD-title.md`
   ```bash
   # Example
   touch _posts/2026-01-11-my-new-post.md
   ```

2. Add Front Matter at the beginning:
   ```yaml
   ---
   title: Post Title
   date: 2026-01-11 14:00:00 +0800
   categories: [Category1, Category2]
   tags: [tag1, tag2]
   ---
   
   Your content starts here...
   ```

3. Save the file and the development server will automatically regenerate

### Modifying Site Configuration

- Edit `_config.yml` file
- Must restart development server for changes to take effect

### Adding Images

1. Place images in `assets/img/` directory
2. Reference in posts:
   ```markdown
   ![Image description](/assets/img/your-image.jpg)
   ```

### Viewing Drafts

1. Create posts in `_drafts` directory (no date prefix needed)
2. Preview drafts with:
   ```bash
   bundle exec jekyll serve --drafts
   ```

## Common Commands

```bash
# Start development server (with live reload)
bash tools/run.sh
# Or
bundle exec jekyll serve

# Build site (without starting server)
bundle exec jekyll build

# Clean build files
bundle exec jekyll clean

# Run tests (check link validity, etc.)
bash tools/test.sh

# Check Jekyll version
bundle exec jekyll -v

# Update dependencies
bundle update
```

## Troubleshooting

### Q1: Error running `bundle install`

**Solution:**
```bash
# Ensure correct Ruby version
ruby -v  # Should be 3.0 or higher

# Clean and reinstall
rm -rf vendor/bundle
bundle install
```

### Q2: Cannot access site after starting server

**Solution:**
- Check if port 4000 is in use
- Try different port: `bundle exec jekyll serve --port 4001`

### Q3: Site doesn't update after file changes

**Solution:**
- `_config.yml` changes require server restart
- Other files should auto-update; try `Ctrl+C` to stop and restart

### Q4: Compilation errors on Windows during dependency installation

**Solution:**
- Ensure Ruby+Devkit version is installed
- Run `ridk install` to install development toolchain
- Re-run `bundle install`

### Q5: How to access website in Dev Container?

**Solution:**
- VS Code automatically forwards ports
- Check "PORTS" tab
- Or access directly at http://localhost:4000

## Deployment

This website is automatically deployed via GitHub Actions:

1. Push to `main` or `master` branch
2. GitHub Actions automatically builds and deploys to GitHub Pages
3. Visit https://fouriersky.github.io to see deployed site

**Note:** Local preview and production deployment may have subtle differences. Test build locally before pushing:
```bash
JEKYLL_ENV=production bundle exec jekyll build
```

## Project Structure

```
.
├── _config.yml          # Site configuration
├── _posts/              # Blog posts
├── _drafts/             # Draft posts
├── _tabs/               # Top navigation pages
├── _data/               # Data files
├── _plugins/            # Jekyll plugins
├── assets/              # Static assets (images, CSS, JS)
├── .devcontainer/       # VS Code Dev Container config
├── tools/               # Helper scripts
│   ├── run.sh          # Start development server
│   └── test.sh         # Run tests
└── Gemfile              # Ruby dependency definitions
```

## Further Learning

- [Jekyll Official Documentation](https://jekyllrb.com/docs/)
- [Chirpy Theme Documentation](https://github.com/cotes2020/jekyll-theme-chirpy/wiki)
- [Markdown Syntax Guide](https://www.markdownguide.org/)
- [Liquid Template Language](https://shopify.github.io/liquid/)

## Getting Help

If you encounter issues:
1. Check [Jekyll Official Documentation](https://jekyllrb.com/docs/troubleshooting/)
2. Check [Chirpy Theme Issues](https://github.com/cotes2020/jekyll-theme-chirpy/issues)
3. Search for error messages online

---

Happy blogging! 🎉

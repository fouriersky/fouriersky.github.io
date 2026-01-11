# Chirpy Starter

[![Gem Version](https://img.shields.io/gem/v/jekyll-theme-chirpy)][gem]&nbsp;
[![GitHub license](https://img.shields.io/github/license/cotes2020/chirpy-starter.svg?color=blue)][mit]

When installing the [**Chirpy**][chirpy] theme through [RubyGems.org][gem], Jekyll can only read files in the folders
`_data`, `_layouts`, `_includes`, `_sass` and `assets`, as well as a small part of options of the `_config.yml` file
from the theme's gem. If you have ever installed this theme gem, you can use the command
`bundle info --path jekyll-theme-chirpy` to locate these files.

The Jekyll team claims that this is to leave the ball in the user’s court, but this also results in users not being
able to enjoy the out-of-the-box experience when using feature-rich themes.

To fully use all the features of **Chirpy**, you need to copy the other critical files from the theme's gem to your
Jekyll site. The following is a list of targets:

```shell
.
├── _config.yml
├── _plugins
├── _tabs
└── index.html
```

To save you time, and also in case you lose some files while copying, we extract those files/configurations of the
latest version of the **Chirpy** theme and the [CD][CD] workflow to here, so that you can start writing in minutes.

## Local Development

For detailed instructions on how to set up and run this website locally, please refer to:

- 📘 [本地开发指南.md](./本地开发指南.md) - Comprehensive guide in Chinese (中文完整指南)
- 📗 [LOCAL_DEVELOPMENT.md](./LOCAL_DEVELOPMENT.md) - Comprehensive guide in English
- ⚡ [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - Quick reference for common commands (快速参考)
- 🔧 [TROUBLESHOOTING.md](./TROUBLESHOOTING.md) - Troubleshooting guide (问题解决指南)

### Quick Start

**Option 1: Using Dev Container (Recommended)**
1. Open this repository in VS Code
2. Click "Reopen in Container" when prompted
3. Run `bash tools/run.sh`
4. Visit http://localhost:4000

**Option 2: Local Installation**
```bash
# Install dependencies
bundle install

# Start development server
bundle exec jekyll serve
# Or use the helper script
bash tools/run.sh
```

Visit http://127.0.0.1:4000 to preview your site.

## Usage

Check out the [theme's docs](https://github.com/cotes2020/jekyll-theme-chirpy/wiki).

## Contributing

This repository is automatically updated with new releases from the theme repository. If you encounter any issues or want to contribute to its improvement, please visit the [theme repository][chirpy] to provide feedback.

## License

This work is published under [MIT][mit] License.

[gem]: https://rubygems.org/gems/jekyll-theme-chirpy
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy/
[CD]: https://en.wikipedia.org/wiki/Continuous_deployment
[mit]: https://github.com/cotes2020/chirpy-starter/blob/master/LICENSE

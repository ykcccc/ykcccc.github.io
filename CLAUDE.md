# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个基于 Hugo 静态网站生成器的个人博客项目，使用 LoveIt 主题（一个简洁、优雅且功能丰富的博客主题）。

## 核心命令

### 开发服务器
```bash
# 启动开发服务器（默认端口 1313）
hugo server

# 启动开发服务器并允许外部访问
hugo server --bind 0.0.0.0

# 构建并启动开发服务器（包含草稿和未来文章）
hugo server -D --buildFuture
```

### 构建和部署
```bash
# 构建生产版本（输出到 public/ 目录）
hugo

# 清理构建输出后重新构建
rm -rf public/ && hugo
```

### 内容创建
```bash
# 创建新文章（使用 default.md archetype）
hugo new posts/my-post.md

# 创建新页面
hugo new about.md
```

## 项目结构

### 核心目录说明
- `hugo.toml` - Hugo 主配置文件（网站设置、主题参数、菜单配置等）
- `content/` - 内容目录（所有 Markdown 文章和页面）
  - `posts/` - 博客文章（Hugo 标准约定）
- `layouts/` - 自定义布局模板（覆盖主题默认布局）
- `static/` - 静态资源（图片、CSS、JS、favicon 等）
- `assets/` - 资源文件（通过 Hugo Pipes 处理的 SCSS、JS 等）
- `archetypes/` - 内容模板（`hugo new` 命令使用）
- `data/` - 数据文件（YAML/JSON/ TOML，供模板和 shortcodes 使用）
- `i18n/` - 国际化文件
- `LoveIt/` - LoveIt 主题子模块（Git Submodule）
- `public/` - 构建输出目录（`.gitignore`）

### 主题配置
LoveIt 主题作为 Git 子模块集成：
- 主题路径：`LoveIt/`（根目录）
- 主题仓库：https://github.com/dillonzq/LoveIt
- Hugo 配置：`hugo.toml` 中的 `theme = "LoveIt"`

**重要**：如果 `LoveIt/` 目录为空，需要初始化子模块：
```bash
git submodule update --init --recursive
```

## LoveIt 主题特性

### 内容管理
- **Front Matter 参数**：支持标题、日期、分类、标签、封面图、摘要等
- **文章类型**：posts（博客文章）、普通页面
- **多语言支持**：可配置多语言内容
- **短代码（Shortcodes）**：
  - `{{< admonition >}}` - 提示框
  - `{{< echarts >}}` - 数据可视化
  - `{{< mermaid >}}` - 流程图
  - `{{< music >}}` - 音乐播放器
  - `{{< bilibili >}}` - Bilibili 视频
  - `{{< mapbox >}}` - 地图嵌入

### 配置要点
- **分页设置**：`pagination.pagerSize` 控制每页文章数
- **默认内容语言**：`defaultContentLanguage` 和 `languageCode`
- **SEO 配置**：`enableRobotsTXT`、`enableGitInfo`
- **资源处理**：图片优化、懒加载支持

## 开发注意事项

### 内容文件位置
- 所有新内容应放在 `content/` 目录下
- 博客文章建议放在 `content/posts/` 目录
- Front Matter 中设置 `draft = true` 可标记为草稿

### 自定义配置
- 修改网站设置：编辑 `hugo.toml`
- 覆盖主题模板：在 `layouts/` 目录创建对应文件（保持与主题相同的路径结构）
- 添加自定义样式：在 `assets/` 或 `static/` 中添加 CSS
- 自定义 archetype：编辑 `archetypes/default.md` 或创建新模板

### 主题参考
- LoveIt 主题文档：https://hugoloveit.com/
- 主题示例配置：`LoveIt/exampleSite/hugo.toml`
- 主题示例内容：`LoveIt/exampleSite/content/`

### Hugo 版本要求
- 最低版本：Hugo 0.128.0
- 当前版本：Hugo 0.154.5+extended（支持 extended SCSS 构建）

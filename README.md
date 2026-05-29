# Easy Know Hard Insist

一个基于 Docusaurus 2 构建的知识分享文档网站，记录学习过程中的"易知难坚持"。

## 技术栈

- **框架**: [Docusaurus 2](https://docusaurus.io/) - 现代静态网站生成器
- **前端**: React 17, MDX
- **包管理**: Yarn
- **部署**: GitHub Pages

## 快速开始

### 环境要求

- Node.js >= 16.0
- Yarn >= 1.22.0

### 安装依赖

```bash
yarn install
```

### 本地开发

```bash
yarn start
```

启动本地开发服务器后，浏览器会自动打开 `http://localhost:3000`。大多数更改会实时反映，无需重启服务器。

## 构建与部署

### 构建项目

```bash
yarn build
```

此命令会在 `build` 目录中生成静态内容，可以使用任何静态内容托管服务提供服务。

### 部署到 GitHub Pages

```bash
# 设置环境变量
export GIT_USER=<Your GitHub username>
export USE_SSH=true

# 部署
yarn deploy
```

如果使用 GitHub Pages 托管，此命令会自动构建网站并推送到 `gh-pages` 分支。

## 项目结构

```
├── docs/              # 文档内容
│   ├── home.md       # 首页
│   ├── math/         # 数学相关文档
│   └── program/      # 编程相关文档
├── src/              # 源代码
│   ├── components/   # React 组件
│   ├── css/          # 样式文件
│   └── pages/        # 页面组件
├── static/           # 静态资源
├── docusaurus.config.js  # Docusaurus 配置
├── sidebars.js       # 侧边栏配置
└── package.json      # 项目依赖
```

## 贡献指南

欢迎贡献！请遵循以下步骤：

1. Fork 本仓库
2. 创建功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'feat: add amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 创建 Pull Request

## 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。

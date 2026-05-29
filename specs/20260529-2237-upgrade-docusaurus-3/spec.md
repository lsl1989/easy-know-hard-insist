# Feature Specification: Docusaurus 3 升级

**Feature Branch**: `20260529-2237-upgrade-docusaurus-3`

**Created**: 2026/5/29

**Status**: Draft

**Input**: User description: "将这个项目使用的 Docusaurus 2 升级成 Docusaurus 3"

## User Scenarios & Testing

### User Story 1 - 平滑升级体验 (Priority: P1)

作为项目维护者，我希望将 Docusaurus 从 2.4.3 升级到 3.x 版本，以便获得最新的功能、性能改进和安全更新，同时确保现有文档内容和功能不受影响。

**Why this priority**: 这是核心升级任务，确保项目保持技术栈的现代性和可维护性。

**Independent Test**: 运行 `yarn start` 启动开发服务器，验证所有页面正常渲染，导航功能正常，数学公式正确显示。

**Acceptance Scenarios**:

1. **Given** 当前 Docusaurus 2.4.3 项目，**When** 执行升级到 Docusaurus 3.x，**Then** 所有现有文档页面正常显示
2. **Given** 升级后的项目，**When** 运行 `yarn build`，**Then** 构建成功无错误
3. **Given** 升级后的项目，**When** 访问数学相关文档，**Then** KaTeX 公式正确渲染

---

### User Story 2 - 开发体验优化 (Priority: P2)

作为开发者，我希望升级后的开发服务器启动更快、热更新更流畅，以便提高文档编写效率。

**Why this priority**: Docusaurus 3 提供了更好的开发体验，包括更快的构建速度和改进的 HMR。

**Independent Test**: 启动开发服务器，修改文档内容，验证热更新在 2 秒内生效。

**Acceptance Scenarios**:

1. **Given** 升级后的项目，**When** 运行 `yarn start`，**Then** 开发服务器在 10 秒内启动完成
2. **Given** 开发服务器运行中，**When** 修改 docs/home.md，**Then** 浏览器在 2 秒内自动刷新

---

### User Story 3 - 依赖兼容性 (Priority: P3)

作为项目维护者，我希望所有依赖包版本兼容，避免安全漏洞和版本冲突。

**Why this priority**: 确保项目依赖健康，减少潜在的安全风险和维护负担。

**Independent Test**: 运行 `yarn install` 无警告，`npm audit` 无高危漏洞。

**Acceptance Scenarios**:

1. **Given** 升级后的 package.json，**When** 运行 `yarn install`，**Then** 无版本冲突警告
2. **Given** 升级后的项目，**When** 运行 `npm audit`，**Then** 无 critical 或 high 级别漏洞

---

### Edge Cases

- 如果某些 MDX 语法在 v2 中不兼容，需要提供迁移方案
- 如果 KaTeX 样式加载失败，需要有降级方案
- 如果构建时间显著增加，需要优化配置

## Requirements

### Functional Requirements

- **FR-001**: 系统 MUST 将 @docusaurus/core 从 2.4.3 升级到 3.x 最新稳定版
- **FR-002**: 系统 MUST 将 @docusaurus/preset-classic 从 2.4.3 升级到 3.x 最新稳定版
- **FR-003**: 系统 MUST 将 React 从 17.x 升级到 18.x
- **FR-004**: 系统 MUST 将 @mdx-js/react 从 1.x 升级到 3.x（Docusaurus 3 依赖）
- **FR-005**: 系统 MUST 更新 remark-math 和 rehype-katex 到兼容版本
- **FR-006**: 系统 MUST 更新 docusaurus.config.js 配置以兼容 Docusaurus 3 格式
- **FR-007**: 系统 MUST 确保所有现有文档（docs/、blog/）正常渲染
- **FR-008**: 系统 MUST 确保数学公式（KaTeX）正确显示
- **FR-009**: 系统 MUST 确保侧边栏导航正常工作
- **FR-010**: 系统 MUST 确保搜索功能正常工作

### Key Entities

- **package.json**: 包含项目依赖和脚本配置
- **docusaurus.config.js**: Docusaurus 主配置文件
- **sidebars.js**: 侧边栏配置
- **docs/**: 文档内容目录
- **blog/**: 博客内容目录
- **src/**: 自定义组件和样式

## Success Criteria

### Measurable Outcomes

- **SC-001**: 升级后 `yarn build` 成功完成，构建时间不超过原来的 150%
- **SC-002**: 升级后 `yarn start` 开发服务器正常启动，所有页面可访问
- **SC-003**: 升级后所有数学公式正确渲染，无样式丢失
- **SC-004**: 升级后 `npm audit` 无 critical 或 high 级别安全漏洞
- **SC-005**: 升级后文档页面加载时间不超过原来的 120%

## Assumptions

- 假设现有文档内容使用标准 Markdown/MDX 语法，无大量不兼容的自定义语法
- 假设项目部署在 GitHub Pages，升级后部署流程不变
- 假设用户使用现代浏览器访问（Chrome、Firefox、Safari 最新版本）
- 假设 Node.js 版本 >= 18.0（Docusaurus 3 要求）
- 假设可以接受短暂的开发环境调整时间来解决潜在的兼容性问题
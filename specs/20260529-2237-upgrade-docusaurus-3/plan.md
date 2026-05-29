# Implementation Plan: Docusaurus 3 升级

**Branch**: `20260529-2237-upgrade-docusaurus-3` | **Date**: 2026/5/29 | **Spec**: [link](spec.md)

**Input**: Feature specification from `/specs/20260529-2237-upgrade-docusaurus-3/spec.md`

## Summary

将 Docusaurus 从 2.4.3 升级到 3.x 最新稳定版，同时升级 React 17 到 18、MDX 1.x 到 3.x，确保所有现有文档、数学公式（KaTeX）、侧边栏导航和搜索功能正常工作。

## Technical Context

**Language/Version**: JavaScript ES6+, Node.js >= 18.0

**Primary Dependencies**:
- @docusaurus/core: 2.4.3 → 3.x
- @docusaurus/preset-classic: 2.4.3 → 3.x
- react: ^17.0.1 → ^18.x
- react-dom: ^17.0.1 → ^18.x
- @mdx-js/react: ^1.6.21 → ^3.x
- remark-math: 3.0.1 → 6.x
- rehype-katex: ^5.0.0 → ^7.x

**Storage**: N/A (静态文档站点)

**Testing**: 手动测试（yarn start, yarn build）

**Target Platform**: Web (GitHub Pages)

**Project Type**: Docusaurus 文档网站

**Performance Goals**:
- 构建时间不超过原来的 150%
- 开发服务器启动 < 10 秒
- 热更新 < 2 秒

**Constraints**:
- 保持现有文档内容不变
- 保持 GitHub Pages 部署流程不变
- 保持数学公式渲染正常

**Scale/Scope**: 小型文档站点（约 20 个文档页面）

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

✅ 项目类型：Docusaurus 文档网站 - 符合规范
✅ 技术栈：JavaScript/Node.js - 符合规范
✅ 无复杂架构变更 - 仅依赖升级

## Project Structure

### Documentation (this feature)

```text
specs/20260529-2237-upgrade-docusaurus-3/
├── plan.md              # This file
└── spec.md              # Feature specification
```

### Source Code (repository root)

```text
# Docusaurus 文档站点结构
├── docs/                # 文档内容
│   ├── home.md         # 首页
│   ├── math/           # 数学文档
│   └── program/        # 编程文档
├── blog/               # 博客内容
├── src/                # 自定义组件和样式
│   ├── components/
│   ├── css/
│   └── pages/
├── static/             # 静态资源
├── docusaurus.config.js  # 主配置文件
├── sidebars.js         # 侧边栏配置
└── package.json        # 依赖配置
```

**Structure Decision**: 保持现有 Docusaurus 项目结构不变，仅更新依赖版本和配置。

## Implementation Phases

### Phase 0: Research - 依赖版本调研

**目标**: 确定 Docusaurus 3 的最新稳定版本和所有依赖的兼容版本

**任务**:
- [ ] R001 查询 @docusaurus/core 最新 3.x 稳定版本
- [ ] R002 查询 @mdx-js/react 兼容版本
- [ ] R003 查询 remark-math 和 rehype-katex 兼容版本
- [ ] R004 研究 Docusaurus 2 到 3 的破坏性变更
- [ ] R005 研究 MDX 1.x 到 3.x 的迁移要求

**输出**: research.md - 包含版本号和迁移注意事项

---

### Phase 1: Design - 升级方案设计

**目标**: 制定详细的升级步骤和配置变更

**任务**:
- [ ] D001 设计 package.json 依赖更新方案
- [ ] D002 设计 docusaurus.config.js 配置更新方案
- [ ] D003 识别需要修改的 MDX 文件
- [ ] D004 制定回滚方案

**输出**:
- data-model.md - 依赖关系和配置变更
- quickstart.md - 升级步骤指南

---

### Phase 2: Implementation - 执行升级

**目标**: 实际执行升级操作

**任务**:
- [ ] I001 更新 package.json 依赖版本
- [ ] I002 运行 yarn install 安装新依赖
- [ ] I003 更新 docusaurus.config.js 配置
- [ ] I004 修复 MDX 兼容性问题（如有）
- [ ] I005 更新 KaTeX 样式引入方式
- [ ] I006 测试开发服务器启动
- [ ] I007 测试所有页面渲染
- [ ] I008 测试数学公式显示
- [ ] I009 测试构建命令
- [ ] I010 测试部署流程

**输出**: 升级完成的代码

---

### Phase 3: Validation - 验证测试

**目标**: 验证升级后的功能完整性

**任务**:
- [ ] V001 验证所有文档页面可访问
- [ ] V002 验证侧边栏导航正常
- [ ] V003 验证搜索功能正常
- [ ] V004 验证数学公式渲染正确
- [ ] V005 验证博客功能正常
- [ ] V006 运行 npm audit 检查安全漏洞
- [ ] V007 测量构建时间

**输出**: 验证报告

---

## Dependencies & Execution Order

### Phase Dependencies

- **Phase 0 (Research)**: 无依赖 - 可立即开始
- **Phase 1 (Design)**: 依赖 Phase 0 完成
- **Phase 2 (Implementation)**: 依赖 Phase 1 完成
- **Phase 3 (Validation)**: 依赖 Phase 2 完成

### Parallel Opportunities

- Phase 0 中的 R001-R003 可并行执行
- Phase 2 中的 I001-I002 必须顺序执行
- Phase 3 中的 V001-V005 可并行执行

---

## Risk Mitigation

### 风险 1: MDX 语法不兼容

**缓解措施**:
- Phase 0 中详细研究 MDX 迁移指南
- Phase 2 中逐个检查 MDX 文件
- 准备回滚方案

### 风险 2: KaTeX 样式问题

**缓解措施**:
- Phase 0 中确认 KaTeX 版本兼容性
- Phase 2 中测试数学公式渲染
- 准备降级方案

### 风险 3: 构建时间显著增加

**缓解措施**:
- Phase 3 中测量构建时间
- 如超阈值，优化配置
- 考虑增量构建

---

## Rollback Plan

如果升级失败：

1. `git checkout main` - 恢复到升级前状态
2. `rm -rf node_modules` - 清除依赖
3. `yarn install` - 重新安装旧版本依赖
4. 验证功能正常

---

## Success Criteria

- [x] Phase 0: 确定所有依赖版本
- [ ] Phase 1: 设计升级方案
- [ ] Phase 2: 成功升级所有依赖
- [ ] Phase 3: 所有功能验证通过
- [ ] 最终: `yarn build` 成功，`yarn start` 正常
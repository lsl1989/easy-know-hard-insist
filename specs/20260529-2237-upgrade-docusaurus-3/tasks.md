# Tasks: Docusaurus 3 升级

**Input**: Design documents from `/specs/20260529-2237-upgrade-docusaurus-3/`

**Prerequisites**: plan.md (required), spec.md (required)

**Tests**: 本项目使用手动测试验证功能

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 [P] [US1] 创建功能分支 20260529-2237-upgrade-docusaurus-3
- [ ] T002 [P] [US1] 备份当前 package.json 和 docusaurus.config.js

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [ ] T003 [US1] 查询 @docusaurus/core 最新 3.x 稳定版本
- [ ] T004 [US1] 查询 @mdx-js/react 兼容版本
- [ ] T005 [US1] 查询 remark-math 和 rehype-katex 兼容版本
- [ ] T006 [US1] 研究 Docusaurus 2 到 3 的破坏性变更文档
- [ ] T007 [US1] 研究 MDX 1.x 到 3.x 的迁移要求

**Checkpoint**: Foundation ready - user story implementation can now begin

---

## Phase 3: User Story 1 - 平滑升级体验 (Priority: P1) 🎯 MVP

**Goal**: 将 Docusaurus 从 2.4.3 升级到 3.x，确保所有现有文档正常显示

**Independent Test**: 运行 `yarn start` 启动开发服务器，验证所有页面正常渲染，导航功能正常，数学公式正确显示

### Implementation for User Story 1

- [ ] T008 [US1] 更新 package.json 中 @docusaurus/core 版本到 3.x
- [ ] T009 [US1] 更新 package.json 中 @docusaurus/preset-classic 版本到 3.x
- [ ] T010 [US1] 更新 package.json 中 react 版本到 ^18.x
- [ ] T011 [US1] 更新 package.json 中 react-dom 版本到 ^18.x
- [ ] T012 [US1] 更新 package.json 中 @mdx-js/react 版本到 ^3.x
- [ ] T013 [US1] 更新 package.json 中 remark-math 版本到 6.x
- [ ] T014 [US1] 更新 package.json 中 rehype-katex 版本到 ^7.x
- [ ] T015 [US1] 运行 yarn install 安装新依赖
- [ ] T016 [US1] 更新 docusaurus.config.js 配置以兼容 Docusaurus 3
- [ ] T017 [US1] 更新 KaTeX 样式引入方式（如需要）
- [ ] T018 [US1] 测试开发服务器启动 yarn start
- [ ] T019 [US1] 测试所有文档页面渲染
- [ ] T020 [US1] 测试数学公式显示
- [ ] T021 [US1] 测试侧边栏导航
- [ ] T022 [US1] 测试构建命令 yarn build

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - 开发体验优化 (Priority: P2)

**Goal**: 验证升级后的开发体验改进

**Independent Test**: 启动开发服务器，修改文档内容，验证热更新在 2 秒内生效

### Implementation for User Story 2

- [ ] T023 [US2] 测量开发服务器启动时间
- [ ] T024 [US2] 测试热更新响应时间
- [ ] T025 [US2] 验证 MDX 文件修改后自动刷新

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - 依赖兼容性 (Priority: P3)

**Goal**: 确保所有依赖包版本兼容，无安全漏洞

**Independent Test**: 运行 `yarn install` 无警告，`npm audit` 无高危漏洞

### Implementation for User Story 3

- [ ] T026 [US3] 运行 yarn install 检查版本冲突
- [ ] T027 [US3] 运行 npm audit 检查安全漏洞
- [ ] T028 [US3] 修复发现的安全问题（如有）

**Checkpoint**: All user stories should now be independently functional

---

## Phase N: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] T029 [P] 更新 README.md 中的 Docusaurus 版本说明
- [ ] T030 [P] 更新文档中的版本引用
- [ ] T031 测量构建时间并与升级前对比
- [ ] T032 验证 GitHub Pages 部署流程正常
- [ ] T033 提交所有更改

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after User Story 1 - Tests development experience
- **User Story 3 (P3)**: Can start after User Story 1 - Validates dependencies

### Within Each User Story

- Package.json updates before yarn install
- Config updates before testing
- All tests before moving to next story

### Parallel Opportunities

- T001-T002 can run in parallel (Setup)
- T003-T007 can run in parallel (Research)
- T008-T014 can run in parallel (Package updates)
- T019-T021 can run in parallel (Testing)

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently
4. Add User Story 3 → Test independently
5. Polish and finalize

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
- Keep backup of original files before making changes
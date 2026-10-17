# 通用 AI 辅助工程工作流与规范模板 (Universal AI Agent Template)

本目录提炼自成熟工程实践中的人机协同方法论与架构铁律，可直接复制到任意语言和框架的项目中（如 Node.js / TypeScript、Python、Go、Rust、Java、C# Web / API 等）。

---

## 📁 目录结构概览

```text
universal_agent_template/
├── README.md                      # 本使用说明
├── .agents/
│   ├── AGENTS.md                  # 【核心】项目长期规则、架构铁律与协作宪章
│   └── skills/
│       ├── project-init/          # 【工作流 0】首次接入与工程文档自适应初始化
│       │   └── SKILL.md
│       ├── session-bootstrap/     # 【工作流 1】新会话开局无损承接与基准唤醒
│       │   └── SKILL.md
│       └── git-commit-suggestion/ # 【工作流 2】阶段收尾、规则升华与纯文本提交归档
│           └── SKILL.md
└── docs/
    ├── SESSION_HANDOFF.md         # 【账本 1】唯一通用动态会话交接备忘录
    └── architecture_design.md     # 【账本 2】唯一通用系统架构与技术大账本
```

---

## 🚀 如何在其他新项目中一键启用？

### 步骤 1：直接复制目录到新项目根目录
将本目录下的 `.agents/` 和 `docs/` 两个文件夹直接复制到你的新项目根目录下即可：

```text
# 复制后的新工程目录结构：
your-new-project/
├── .agents/
│   ├── AGENTS.md
│   └── skills/
│       ├── project-init/
│       ├── session-bootstrap/
│       └── git-commit-suggestion/
├── docs/
│   ├── SESSION_HANDOFF.md
│   └── architecture_design.md
├── package.json (或 pyproject.toml / go.mod / Cargo.toml 等)
└── src/
```

### 步骤 2：对 AI 发送 `初始化` 或 `init`（零手动修改，全自动适配）
复制完成后，无需手动修改任何文件！直接在与 AI 的首轮对话中输入：
> **`初始化`** 或 **`init`**

AI 将自动激活 `project-init` 技能：
1. 深度扫描项目的语言、框架版本、持久层/数据库依赖与真实源码目录分层；
2. 调阅真实的 Git 提交历史与版本基准（提取 `package.json` / `Cargo.toml` 等版本）；
3. **全自动清洗并重写 `docs/architecture_design.md` 与 `docs/SESSION_HANDOFF.md`**，清除模板占位样例，替换为真实物理工程全景；
4. 输出《项目工程全景体检与工作流初始化就绪报告》，即刻进入开发待命状态！

---

## 🔄 敏捷人机协同完整工作流

### 0. 首次接入：输入 `初始化` 或 `init`
- **触发**：新项目首次复制模板后，对 AI 发送 `初始化` 或 `init`；
- **AI 动作**：全景扫描项目技术栈与真实代码结构，自动适配双账本（`architecture_design.md` & `SESSION_HANDOFF.md`），完成规则与工程基线对齐。

### 1. 开工承接：输入 `新会话`
- **触发**：日常新开启一个对话时，对 AI 发送 `新会话` 或 `开始`；
- **AI 动作**：
  1. 自动执行 `git status -s` 与 `git log -n 3 --stat` 查看物理状态与提交历史；
  2. 调阅动态状态真理源 `docs/SESSION_HANDOFF.md` 提取当前攻坚主线与最新业务里程碑；
  3. 核准 `AGENTS.md` 核心协同底座与架构红线；
  4. 给出清晰干练的 4 段式环境就绪汇报，并**纯粹待命**，绝不越权推荐下一步计划。

### 2. 敏捷开发：专注且轻量
- **AI 遵循的核心铁律**：
  - **用户为唯一执行者**：AI 绝不擅自运行测试脚本或启动服务；
  - **反馈闭环**：用户反馈报错后，AI 先分析根因并提出方案，确认后再动代码；
  - **KISS 与反过度工程化**：优先原生态实现，**连续失败两次强制触发警停**；
  - **保护微调**：尊重用户在样式与布局中的手动精调；
  - **过程防打扰**：编码中途不频繁递增版本号，不反复执行 git 校验。

### 3. 收尾归档：输入 `提交` 或 `commit`
- **触发**：当前功能开发测试完毕，对 AI 发送 `提交` 或 `commit`；
- **AI 动作**：
  1. 自动审查 `git diff HEAD --stat`（全量覆盖工作区与 GUI 暂存区真实物理变动）；
  2. **精细化版本号递增**：仅当包含功能演进或缺陷修复时集中递增工程最低位（Patch 号或第 4 位构建号），纯文档/工作流维护免递增；
  3. **审慎规则升华 (安全阀)**：仅在重大架构踩坑或确立跨模块通用底层契约时合并提炼写入 `AGENTS.md`，常规业务逻辑严禁追加，杜绝 Prompt 膨胀；
  4. 自动登记动态状态真理源 `docs/SESSION_HANDOFF.md` 业务里程碑；
  5. 给出严格遵循 Conventional Commits 规范的**纯文本代码块提交注释**（无命令行字符，支持一键复制粘贴），且绝不越权建议下一步。

---

## 💎 通用架构铁律速查
1. **单一真理源**：`AGENTS.md` 专管静态规则，`SESSION_HANDOFF.md` 独占动态现场。
2. **零硬编码**：业务分类与权重由配置/数据字典唯一驱动。
3. **软删除规范**：核心业务表一律 `is_delete`，区分“业务生命周期正常终结（保留）”与“系统软删除（撤销/脏数据）”。
4. **消灭 N+1**：循环内严禁单条查库或网络调用，一律批量拉取后内存 Hash 组装。
5. **静默成功**：成功操作无感响应（不弹多余提示弹窗），破坏性操作强制事前二次确认。
6. **人类直读**：入库数据反转义 Unicode，保持纯原生态 UTF-8 直读。

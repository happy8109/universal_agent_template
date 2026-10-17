---
name: project-init
description: >-
  当用户请求“初始化”、“项目初始化”、“初始化工作流”、“首次运行”、“适配项目”、“init”、“project-init”或相关工作流首次接入指令时激活此技能。
---

# 项目首次接入与工作流自适应初始化 (Project Init & Workflow Adaptation)

本技能用于在将本套通用协同规范与工作流模板复制到**任何新项目或现有存量项目**时，由 AI 自动对目标项目的代码、文档、依赖与 Git 历史进行全景扫描与体检，**全自动自适应更新 `docs/architecture_design.md` 和 `docs/SESSION_HANDOFF.md`**，识别项目技术栈与架构特征，实现零手动修改、即开即用的无缝接入。

---

## 核心执行流程

### 1. 全景代码与工程环境探测 (Deep Project Reconnaissance)
激活本技能后，AI 必须第一时间按序执行以下**纯只读**探测步骤：

1. **探测工程依赖与技术栈元数据**：
   - 检查根目录及子目录下的关键配置文件：
     * Node / TS: `package.json`, `tsconfig.json`, `pnpm-workspace.yaml`
     * Python: `pyproject.toml`, `requirements.txt`, `setup.py`, `Pipfile`
     * Go: `go.mod`, `go.sum`
     * Rust: `Cargo.toml`
     * Java / Kotlin: `pom.xml`, `build.gradle`, `build.gradle.kts`
     * .NET / C#: `*.sln`, `*.csproj`
     * Web 前端: `vite.config.*`, `next.config.*`, `webpack.config.*`, `tailwind.config.*`
   - 提取真实语言版本、核心 Web / API 框架、ORM / 数据库驱动、UI 库及核心第三方依赖；
2. **探测物理目录结构与分层架构**：
   - 查看根目录结构与关键源码目录（如 `src/`, `lib/`, `cmd/`, `internal/`, `app/`, `components/`, `controllers/`, `services/`, `models/` 等）；
   - 辨析工程形态：全栈单体 (Monolith)、前后端分离、纯前端 SPA、纯后端 API / 微服务、CLI 命令行工具、共享库 (SDK / Library) 或数据管道；
3. **探测 Git 状态与历史版本基准**：
   - 执行 `git status -s`、`git branch --show-current` 与 `git log -n 5 --stat`；
   - 检查是否存在 Git Tag 或 Release 发布历史；
   - 提取真实初始版本号（优先提取 `package.json`、`pyproject.toml`、`Cargo.toml`、`AssemblyInfo.cs` 中的 `version`，若无则默认为 `0.1.0` 或 `1.0.0.0`）；
4. **探测既有文档与业务背景**：
   - 查阅项目中既有的 `README.md`、需求设计文档、接口文档或 SQL 迁移脚本（如 `migrations/`, `sql/` 等），提炼核心业务目标与系统定位。

---

### 2. 动态账本自适应填充与清洗 (Ledgers & Memory Auto-Adaptation)
基于上述真实探测结果，AI 自动完成对模板占位符的清洗与替换，确保系统双账本 100% 映射真实物理工程：

1. **自动适配系统技术全景大账本 [docs/architecture_design.md](file:///docs/architecture_design.md)**：
   - **更新第 1 节【系统技术全景与选型】**：用真实检测到的语言、运行时版本、框架、数据库及缓存替换 `[如 Node.js 20+...]` 占位符；
   - **更新第 2 节【核心数据模型与规范】**：根据项目是否包含持久层，明确数据库规范；若非持久化项目（如 CLI 或纯前端），注明“本项目不涉及持久层存储”；
   - **更新第 3 节【核心模块与分层设计】**：将模板中的默认目录树替换为本项目**真实探测到的源码目录结构**，并附带各目录职责简注；
   - **更新第 4 节【全局需求演进与 Backlog】**：将首个 Milestone 标记为“工作流模板接入与工程环境初始化对齐”，并结合既有文档/提交提炼后续 2~3 个预期演进里程碑。
2. **自动适配动态状态唯一真理源 [docs/SESSION_HANDOFF.md](file:///docs/SESSION_HANDOFF.md)**：
   - **更新【当前进行中任务基准 (Active Context)】**：
     * **当前核心主线**：设为项目真实的当前开发模块或“工作流初始化就绪与首期功能准备”；
     * **当前版本基准**：填入探测到的真实版本号；
     * **当前分支状态**：填入真实当前分支名（如 `main` 或 `master` 等）；
   - **更新【核心业务与功能最新里程碑】**：
     * 清理模板自带的虚拟鉴权示例（AuthService 等）；
     * 写入本项目的初始业务基线：根据最新 Git 提交记录或现有核心资产建立初始台账；
     * 将探测到的核心已有模块/目录登记进【最新已就绪核心资产 (严禁重复返工)】；
   - **登记【最近一次工程与工作流维护记录】**：记录初始化时间与工作流模板接入；
   - **初始化【历史交接归档流水】**：登记首条 init 记录。
3. **核对与提示规则宪章 [.agents/AGENTS.md](file:///.agents/AGENTS.md) 裁剪建议**：
   - 若项目为纯前端、CLI 脚本、纯算法或无数据库组件，主动向用户说明：`.agents/AGENTS.md` 的【第二部分：企业级业务与持久层架构拓展包】可保持静默或按需裁撤；
   - 若项目中既有数据库使用了不同的软删除字段（如 `deleted_at` 代替 `is_delete`），在此步骤中主动向用户提示并建议同步对齐规则。

---

### 3. 生成结构化《项目工程全景体检与工作流初始化报告》
适配完成后，AI 向用户输出规范、清晰、专业的开局体检总览报告：

```markdown
### 🚀 项目工程全景体检与工作流初始化就绪报告

#### 1. 🔍 项目类型与核心技术栈判定
- **工程形态**：[如：前后端分离后端 API / Next.js 全栈应用 / Go CLI 工具 / 基础库]
- **核心语言与运行时**：[如：Node.js v20.x / TypeScript v5.3 / Go 1.22]
- **Web / 核心框架**：[如：FastAPI / Gin / Express / NestJS]
- **数据持久层与 ORM**：[如：PostgreSQL + Prisma / MySQL + GORM / 无数据库]
- **真实基准版本**：`[真实版本号]`（源自 `[package.json / Cargo.toml 等]`）
- **当前 Git 分支**：`[分支名]`

#### 2. 📂 真实源码结构与就绪资产映射
- [列出探测到的关键源码目录及对应职责说明，确认已登记入防返工台账]

#### 3. 📋 双账本自适应填充成果
- [x] **[docs/architecture_design.md](file:///docs/architecture_design.md)**：已按真实技术栈、分层目录与里程碑全量替换模板占位符；
- [x] **[docs/SESSION_HANDOFF.md](file:///docs/SESSION_HANDOFF.md)**：已清除虚拟样例，对齐当前版本基准与初始已就绪核心资产；
- [x] **[.agents/AGENTS.md](file:///.agents/AGENTS.md)**：宪章协同底座就绪[，针对本项目持久层特性的裁撤/对齐说明]。

#### 4. ⚠️ 本项目适用核心铁律与协作准则
- **用户为唯一执行者**：AI 绝不擅自执行构建、测试或启动服务；
- **单一真理源**：静态规则看 `AGENTS.md`，动态进度看 `SESSION_HANDOFF.md`，技术全景看 `architecture_design.md`；
- [列出与本项目最相关的 2~3 条红线，如：零硬编码 / 批量防 N+1 / 软删除规范 / 成功静默响应等]。

---
工程全景已扫描完成，双账本与规范已全自动适配就绪。请指示第一项攻坚任务！
```

---

### 4. 输出规范与红线约束（绝对红线）
- **严禁擅自执行破坏性代码或服务**：探测阶段仅允许使用只读命令（如文件查看、`git status`、`git log`），**严禁自行运行 `npm install`、`pip install`、构建编译命令或启动开发服务器**；
- **严禁擅自规划具体开发任务**：报告末尾**严禁附带任何诱导性待办建议或强推开发路线**，始终将系统方向的决策权 100% 交由用户；
- **纯粹待命**：完成报告输出后，保持待命状态，等待用户明确下达首个开发指令。

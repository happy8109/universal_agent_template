# 系统架构设计与技术大账本 (architecture_design.md)

本文档是系统**唯一长期技术全景大账本**。承载系统的全局技术选型、数据库与领域实体模型演进、核心 API 契约与全局需求 Backlog 清单。

---

## 1. 系统技术全景与选型 (Tech Stack & Architecture)
- **核心运行时 / 语言**：[如 Node.js 20+ / TypeScript 5.x / Go 1.22 / Python 3.11 / .NET 8]
- **应用框架**：[如 Express / NestJS / FastAPI / Gin / ASP.NET Core]
- **数据存储**：[如 PostgreSQL / MySQL / SQLite / Redis]
- **核心设计哲学**：
  - **KISS 原则**：优先原生态实现，严禁过度设计与滥用复杂抽象；
  - **零硬编码**：业务属性与分类完全由数据字典与配置驱动；
  - **防 N+1 批处理**：关联数据采用批量查询与内存 Hash 匹配。

---

## 2. 核心数据模型与规范 (Data Models & Standards)
- **统一软删除标准**：
  - 全线核心业务表包含 `is_delete INTEGER/BOOLEAN DEFAULT 0`；
  - 区分“业务关系终结（用状态与时间表达）”与“系统软删除（撤销/脏数据）”。
- **可读性标准**：
  - 数据库 JSON 字段入库前反转义 Unicode，保持纯原生态 UTF-8 中文直读。

---

## 3. 核心模块与分层设计 (Module Structure)
```text
src/
├── controllers/    # API 接口入口与参数校验
├── services/       # 核心业务逻辑与流程编排
├── repositories/   # 数据访问层与批处理防 N+1 契约
├── models/         # 领域实体模型
└── utils/          # 无状态通用工具函数
```

---

## 4. 全局需求演进与 Backlog (Roadmap)
- [x] **Milestone 1**：基础架构搭建与工程规范固化
- [ ] **Milestone 2**：核心业务功能与实体设计
- [ ] **Milestone 3**：综合查询与批量报表输出
- [ ] **Milestone 4**：性能调优、工作集缓存与压力验证

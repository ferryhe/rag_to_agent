# rag_to_agent 领域 Agent Ready 输出框架 Implementation Plan

> **For Hermes/Codex:** Use the project-isolated Codex worker pattern. Read `AGENTS.md` and `.hermes/project-status.md` before each run. Do not commit, push, or open PRs without explicit approval.

**Goal:** 建立从通用 RAG artifact 到领域 agent-ready 数据层和工具说明的转换框架。

**Architecture:** 通用 core 管 domain profile、ready_data manifest、tool spec；领域 adapter 先实现 regulatory/cross2 样板。

**Tech Stack:** Project-native stack plus CLI-first JSON/JSONL manifests. Python projects should use Typer/Pydantic where already present; TypeScript projects should preserve pnpm/OpenAPI workflow.

---

## Context

This repository is one module in the broader agent-operated knowledge pipeline:

```text
web_listening -> doc_to_md -> md_to_rag -> rag_to_agent/domain adapters -> ai_interface
```

Current project role: RAG artifact -> agent-ready domain module CLI，负责专业领域 ready_data、planning、tools/API contract。

Current planning scope: 把 c-ross-2 的法规样板泛化为可复用的 domain adapter/agent ready 输出层。

## Non-Negotiable Contracts

1. CLI outputs must be machine-readable and stable (`--json` where applicable).
2. Artifacts must be path-portable and manifest-driven.
3. Reruns must be idempotent.
4. Every derived artifact must preserve provenance back to its input.
5. Secrets/API keys must never be written into manifests or committed files.
6. Cross-repo integration happens through files/manifests/tool specs, not hidden imports.

## Proposed Tasks

### Task 1: 初始化 repo 骨架

**Objective:** 创建 pyproject.toml、src/rag_to_agent/cli.py、profiles/、adapters/、tests。

**Files:**
- Modify/Create project-specific files identified during the task.
- Update tests or fixtures for the changed contract.

**Steps:**
1. Inspect the current implementation and write down exact files touched.
2. Add or update the smallest contract/test fixture first.
3. Implement the minimal change.
4. Run the focused verification command.
5. Update `.hermes/project-status.md` with result and next action.

**Verification:** `rag-to-agent --help` 可运行。

### Task 2: 定义 agent-ready manifest

**Objective:** docs/contracts/rag-to-agent-ready-data-v1.md，字段含 domain、input_rag_manifest、outputs、tools、quality gates。

**Files:**
- Modify/Create project-specific files identified during the task.
- Update tests or fixtures for the changed contract.

**Steps:**
1. Inspect the current implementation and write down exact files touched.
2. Add or update the smallest contract/test fixture first.
3. Implement the minimal change.
4. Run the focused verification command.
5. Update `.hermes/project-status.md` with result and next action.

**Verification:** 文档包含 c-ross-2 示例。

### Task 3: 实现 profile validate

**Objective:** 读取 domain_profile.yaml，校验 adapter、input rag manifest、output schema。

**Files:**
- Modify/Create project-specific files identified during the task.
- Update tests or fixtures for the changed contract.

**Steps:**
1. Inspect the current implementation and write down exact files touched.
2. Add or update the smallest contract/test fixture first.
3. Implement the minimal change.
4. Run the focused verification command.
5. Update `.hermes/project-status.md` with result and next action.

**Verification:** 测试缺字段失败信息清楚。

### Task 4: 移植 c-ross-2 regulatory concepts

**Objective:** 把 title_aliases、sections_structured、formula_cards、relations_graph 设计成 adapter 输出。

**Files:**
- Modify/Create project-specific files identified during the task.
- Update tests or fixtures for the changed contract.

**Steps:**
1. Inspect the current implementation and write down exact files touched.
2. Add or update the smallest contract/test fixture first.
3. Implement the minimal change.
4. Run the focused verification command.
5. Update `.hermes/project-status.md` with result and next action.

**Verification:** 先写 contract 和 fixture，不急着完整迁移。

### Task 5: 实现 toolspec export

**Objective:** 输出 agent 可读 tools/index：search_titles、search_summaries、retrieve_evidence、plan、chat。

**Files:**
- Modify/Create project-specific files identified during the task.
- Update tests or fixtures for the changed contract.

**Steps:**
1. Inspect the current implementation and write down exact files touched.
2. Add or update the smallest contract/test fixture first.
3. Implement the minimal change.
4. Run the focused verification command.
5. Update `.hermes/project-status.md` with result and next action.

**Verification:** 生成 JSON schema/OpenAPI-like 描述。

### Task 6: 接 c-ross-2 smoke

**Objective:** 用 c-ross-2 小样本 ready_data 验证 rag_to_agent 输出一致。

**Files:**
- Modify/Create project-specific files identified during the task.
- Update tests or fixtures for the changed contract.

**Steps:**
1. Inspect the current implementation and write down exact files touched.
2. Add or update the smallest contract/test fixture first.
3. Implement the minimal change.
4. Run the focused verification command.
5. Update `.hermes/project-status.md` with result and next action.

**Verification:** 记录迁移路径和兼容限制。


---

## Acceptance Criteria

- A Codex worker can understand this repo's boundary from `AGENTS.md`.
- A future implementation branch can start from this plan without needing cross-chat context.
- The module's input/output contract is explicit enough for the next module in the chain.
- All new behavior is testable through CLI commands and fixture manifests.

## Recommended First PR

Start with documentation/contracts and fixture-only changes. Do not implement all runtime behavior in the first PR. The first PR should make the intended contract reviewable before code follows.

---
name: mastra-cn
description: "中文适配：Mastra 智能体、工作流与版本核对。Comprehensive Mastra framework guide for building agents, workflows, tools, memory, workspaces, and storage with current APIs. Use for native capability discovery, logging, tracing, metrics/cost estimates, dataset experiments, documentation lookup, API verification, TypeScript setup, common errors, migrations, building and deploying apps to Mastra Platform via Platform APIs and `mastra deploy`, and `mastra api` CLI tasks: inspect or call resources on local, Mastra platform, or remote servers. For Mastra Factory operations, discover and activate the companion mastra-factory skill. Report verified bugs and documentation defects via the feedback endpoint only when the user has explicitly authorized sending feedback."
license: Apache-2.0
metadata:
  author: Mastra
  version: "2.5.0"
  repository: https://github.com/mastra-ai/skills
---

# Mastra Framework Guide

Build AI applications with Mastra. This skill teaches you how to find current documentation and build agents and workflows.

## Critical: Do not trust internal knowledge

Everything you know about Mastra is likely outdated or wrong. Never rely on memory. Always verify against current documentation.

Your training data contains obsolete APIs, deprecated patterns, and incorrect usage. Mastra evolves rapidly - APIs change between versions, constructor signatures shift, and patterns get refactored.

## Prerequisites

Before writing any Mastra code, check if packages are installed:

```bash
ls node_modules/@mastra/
```

- If packages exist: Use embedded docs first (most reliable)
- If no packages: Install first or use remote docs

## Resources

### References

| User Question                       | First Check                                                      | How To                                         |
| ----------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------- |
| Create/install Mastra project     | [`references/create-mastra.md`](references/create-mastra.md)     | Setup guide with CLI and manual steps          |
| Choose Agent/Workflow/Tool/Memory/Storage | [`references/core-concepts.md`](references/core-concepts.md) | Core concepts and when to use each primitive |
| Add logging or set up tracing | [`references/embedded-docs.md`](references/embedded-docs.md) | Look up PinoLogger and observability configuration before custom instrumentation |
| Track automatic metrics or estimated model cost | [`references/embedded-docs.md`](references/embedded-docs.md) | Look up span-derived metrics, storage support, and pricing coverage |
| Evaluate quality or compare prompts/models | [`references/embedded-docs.md`](references/embedded-docs.md) | Look up datasets, experiments, and scorers |
| How do I use Agent/Workflow/Tool? | [`references/embedded-docs.md`](references/embedded-docs.md)     | Look up in `node_modules/@mastra/*/dist/docs/` |
| How do I use X? (no packages)     | [`references/remote-docs.md`](references/remote-docs.md)         | Fetch from `https://mastra.ai/llms.txt`        |
| Choose or validate a model        | [`references/model-selection.md`](references/model-selection.md) | Model format and provider registry lookup      |
| I'm getting an error...           | [`references/common-errors.md`](references/common-errors.md)     | Common errors and solutions                    |
| Upgrade from v0.x to v1.x         | [`references/migration-guide.md`](references/migration-guide.md) | Version upgrade workflows                      |
| Inspect/call server resources via CLI | [`references/mastra-api.md`](references/mastra-api.md)       | `mastra api` CLI for local, Mastra platform, or remote servers |
| Deploy to Mastra Platform, provision projects, or use Platform sandbox/filesystem | [`references/platform.md`](references/platform.md) | Platform REST APIs, credentials, and `mastra deploy` without browser automation |
| Find exact traces with complex predicates | [`references/trace-query.md`](references/trace-query.md) | Query completed traces by trace fields or related spans |
| Count traces or compute grouped measures (error rate, latency, tokens, cost) | [`references/trace-query.md`](references/trace-query.md#aggregate-traces) | Aggregate completed traces with `mastra api trace aggregate` over the same selection |
| List individual spans (failed tool calls, nested agent runs) | [`references/trace-query.md`](references/trace-query.md#query-spans) | Query completed spans with `mastra api span query` and span-field predicates |
| Compute measures per span (tool error rates, nested agent runs, model tokens) | [`references/trace-query.md`](references/trace-query.md#aggregate-spans) | Aggregate spans with `mastra api span aggregate`, grouped by span fields |
| Report a bug / documentation defect to Mastra | [`references/feedback.md`](references/feedback.md) | Report authorized eligible findings to the Mastra team |

### Scripts

- `scripts/provider-registry.mjs`: Look up current providers and models available in the model router. Always run this before using a model to verify provider keys and model names.

## Priority order for writing code

Never write code without checking current docs first.

1. Embedded docs first (if packages installed)

   Look up current docs in `node_modules` for a package. This matches the exact installed version and is the most reliable source of truth. See [`references/embedded-docs.md`](references/embedded-docs.md).

2. Source code second (if packages installed)

   If embedded docs don't cover the question, inspect the installed source and type definitions. This is the source of truth when docs are missing or unclear. See [`references/embedded-docs.md`](references/embedded-docs.md).

3. Remote docs third (if packages not installed)

   Use the latest published docs when packages are not installed or when exploring new features. Remote docs may be ahead of the user's installed version. See [`references/remote-docs.md`](references/remote-docs.md).

## Core concepts

Use [`references/core-concepts.md`](references/core-concepts.md) when choosing between agents, workflows, tools, memory, and storage.

- Agent: Use for open-ended tasks that make decisions and use tools.
- Workflow: Use for defined multi-step processes.

## Mastra Studio

Studio is the interactive UI for building, testing, and managing agents, workflows, and tools. Use Studio when advising a human to inspect or debug visually.

Inside a Mastra project, run:

```bash
npm run dev
```

Then open `http://localhost:4111` in a browser to show Mastra Studio to your human user.

## Mastra API CLI

Use `mastra api` to inspect or call resources on local dev servers, Mastra platform deployments, or remote Mastra endpoints. It is useful for agent-readable state, execution, traces, logs, scores, threads, and workflow operations. See [`references/mastra-api.md`](references/mastra-api.md) for usage patterns.

For exact trace selection that needs recursive predicates or conditions over related spans, read [`references/trace-query.md`](references/trace-query.md). Before using `mastra api trace query`, confirm that the installed CLI exposes the command. Use `--schema` for the target's request/response shape and structural constraints, and use the canonical documentation found through [`references/remote-docs.md`](references/remote-docs.md) for supported fields, operators, and semantics. Preserve opaque pagination cursors and fetch trace or span details only after selecting candidates.

## Deploy to Mastra Platform

When the user asks to deploy to Mastra, whether to build a new app and deploy it or to deploy an existing Mastra project, read [`references/platform.md`](references/platform.md) before running any deploy or Platform API command. It covers which steps need the human (sign-up and sign-in only), credentials, REST discovery and project creation, `PlatformFilesystem` and `PlatformSandbox`, `mastra deploy`, and verification. Build or locate the app first with the references above, then follow `platform.md` to deploy.

## Mastra Factory

For Factory projects, work items, queue health, decisions, session history, memory inspection, or authorized operations, activate the **`mastra-factory`** skill. Factory is an operational control plane, not a reason to scaffold or deploy a new Mastra app.

If the skill is missing, offer to install it from this repository:

```bash
npx skills add mastra-ai/skills --skill mastra-factory
```

Choose the user's intended agent and scope interactively. For global installation, target a supported agent explicitly with `--agent <agent> -g`; PromptScript does not support global installs. Verify installation and referenced files for the intended agent even if another agent target fails.

The Factory skill covers CLI checks, `mastra auth whoami` / authorized `mastra auth login`, and connecting via the user's actual instance URL from any directory. A deployed repository or `.mastra-project.json` is not required with `--url`. Never guess a shared Factory host or project IDs. Its connection and session-inspection references cover deployment-specific authentication, project discovery, threads, and observational memory limitations.

## Reporting feedback

Report verified Mastra bugs and concrete documentation defects when the criteria in [`references/feedback.md`](references/feedback.md) are met and the user has explicitly authorized sending feedback. Do not submit feedback merely because this skill was loaded. Leave feature requests to humans; do not submit them or reclassify them as defects. Do not report the same issue again within the current task or conversation. Capture only anonymized facts for feedback while solving the task. Skip automatic reporting when a finding remains unverified or its relevance is unclear; do not interrupt the user merely to classify it. Respect any user instruction not to report something.

## Critical requirements

### TypeScript config

Mastra requires ES2022 modules. CommonJS will fail. See [`references/create-mastra.md`](references/create-mastra.md) for setup and [`references/common-errors.md`](references/common-errors.md) for troubleshooting.

### Model format

Always use `"provider/model-name"` when defining models using Mastra's model router.

When the user asks to use a model or provider, always run `scripts/provider-registry.mjs` first to verify the provider key and model name are valid. Do not guess model names from memory as they change frequently. See [`references/model-selection.md`](references/model-selection.md).

## When you see errors

Type errors often mean your knowledge is outdated.

Common signs of outdated knowledge:

- `Property X does not exist on type Y`
- `Cannot find module`
- `Type mismatch` errors
- Constructor parameter errors

What to do:

1. Check [`references/common-errors.md`](references/common-errors.md)
2. Verify current API in embedded docs
3. Don't assume the error is a user mistake - it might be your outdated knowledge

## Development workflow

Always verify before writing code:

1. Identify whether Mastra already provides the requested behavior using [`references/core-concepts.md`](references/core-concepts.md#discover-native-capabilities-first), before designing custom infrastructure.
2. Check installed packages and versions, then verify the capability's APIs, configuration, and limits.
   - If installed: Use embedded docs [`references/embedded-docs.md`](references/embedded-docs.md) and installed types/source.
   - If not: Use remote docs [`references/remote-docs.md`](references/remote-docs.md); verify compatibility before adopting newer features.
3. Use the native capability where it fits; implement custom logic only for the identified gap or application-owned requirements.
4. Test with the project scripts or Studio when available.


## 中文开发适配 — mastra-cn 新增

保留上游文档优先、能力发现与开发流程，反馈发送改为需要用户明确授权。

- 中文说明任务与实现思路，API、包名、模型标识和报错保持原文。先从代码和依赖确认实际版本，不能把当前远程文档当作已安装版本。
- “做个智能体／加个工作流”先读 core-concepts 与 embedded-docs；“报类型错误”先读 common-errors 与本机类型定义；模型配置先按上游 registry 路径核对，不靠中文产品俗称猜 provider/model-name。
- “查日志／查追踪”和“调用工作流／部署”是不同的动作范围。按原参考选择工具，不把只读查询自动升级为运行、创建或发布。
- 反馈内容按原有脱敏与证据标准整理，但发送给 Mastra 团队须有用户明确授权；可以先给用户可审阅的草稿。不会因安装或审阅技能自动发送报告。
- 依赖安装、账号认证和部署遵守当前任务授权；不因阅读 setup 参考就执行初始化。没有 package 或外部权限时说明限制，不伪造模型列表、实验或部署结果。
- 用户未要求前端编译时，不主动运行前端 build。实际调用或验证使用目标项目已配置且获准的方式；未执行的检查明确标出。

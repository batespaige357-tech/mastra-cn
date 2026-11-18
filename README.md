# Mastra CN

**用中文讨论需求，按项目真实版本构建 Mastra 应用。**

## 功能与流程

文档优先、原生能力发现、agents/workflows/tools/memory/storage 开发指导，以及日志、追踪、模型选择、迁移和部署参考。保留完整参考目录和 provider-registry 辅助脚本，不另写一套 Mastra API。

## 小幅变化

- 补中文任务导航，包名、API、模型与错误保持原文。
- 明确区分已安装版本与远程文档，避免按过时记忆开发。
- 区分只读检查与运行、部署等动作。
- 自动发送反馈改为用户明确授权后发送，原有证据与脱敏规则保留。

## 安装与调用

```bash
npx skills add batespaige357-tech/mastra-cn --skill mastra-cn
```

对助手说“用 mastra-cn 按当前项目版本实现这个工作流”；Codex 可使用 `$mastra-cn`。也可将 `skills/mastra-cn` 整个目录复制到助手的技能目录，保留 references 和 scripts。

本项目不打包 Mastra 框架、Factory 配套技能或云账号。实际开发需要目标项目的依赖与相应工具权限；辅助脚本不会因安装自动运行。没有效果截图或演示网页。

## 来源与许可

基于 [mastra-ai/skills 的 mastra](https://github.com/mastra-ai/skills/tree/main/skills/mastra)，由本仓库维护。

Apache-2.0，保留 Kepler Software, Inc. 版权、原始许可文件与完整标准许可文本。[CHANGES.md](CHANGES.md) 记录参考提交及改动。

已检查 UTF-8、引用完整性、文件保留情况、技能格式与辅助脚本语法；未运行下载脚本，未进行真实框架、模型、反馈发送或部署测试。没有性能或成功率成绩，未执行前端编译。

\# Claude Code — Environment Notes



> 本文档用于在 Claude Code 环境中运行 Production Code Guidelines 规范。

> 通用行为约束见根目录 \[`SKILL.md`](../../SKILL.md)。



\## 环境注入方式

在项目根目录创建或更新 `CLAUDE.md` 文件（Claude Code 每次交互前必读文件），追加以下核心约束块。



\## CLAUDE.md 核心约束追加块

```markdown

\## Production Coding Constraints

\- 编写或修改代码前，必须严格阅读并遵循项目内 `skills/production-code-guidelines/SKILL.md` 的规范。

\- 严格执行“最小必要改动”，严禁在未授权的情况下重构无关代码或修改无关文件。

\- 严禁编写静默兜底逻辑（如无意义的 catch-and-return-default），除非需求明确要求。

\- 严禁在输出中包含教程式注释或 example usage 噪音。

\- 遇到不确定可信边界的输入时，立即停止并向用户确认防御策略。


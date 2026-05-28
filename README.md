# Production Code Guidelines

面向大语言模型（LLM）的生产代码生成/修改规范，专门纠正 LLM 5 类常见坏习惯：

1. **过度生成** — 加未要求的功能、抽象、扩展点
2. **过度防御** — 在可信层重复校验、猜测性判空
3. **静默兜底** — catch 后返回默认值、悄悄 fallback
4. **补丁式修复** — 修症状而不修根因
5. **教程式输出** — 加示例、解释性注释、演示型结构

> 核心原则：不要多做，不要乱防御，不要吞错，不要打无意义补丁，不要把生产代码写成教程。

---

## 文件结构

```
skills/production-code-guidelines/
├── SKILL.md                        # 主规范（英文，LLM 直接使用）
├── skill.json                      # 元数据（兼容 Claude Code / Codex）
├── agents/
│   ├── claude.yaml                 # Claude Code 界面配置
│   └── openai.yaml                 # Codex 界面配置
└── references/
    ├── agent-notes-claude.md       # Claude Code 环境注入说明
    └── agent-notes-codex.md        # Codex 环境注入说明
```

---

## 快速使用

**Claude Code** — 在项目根目录的 `CLAUDE.md` 中追加：

```markdown
## Production Coding Constraints
- 编写或修改代码前，必须遵循 `skills/production-code-guidelines/SKILL.md`。
- 严格执行最小必要改动，严禁重构无关代码。
- 严禁静默兜底（无意义的 catch-and-return-default）。
- 严禁教程式注释或 example usage 噪音。
```

**Codex** — 在 `AGENTS.md` 或系统指令中追加：

```markdown
## Core Constraints
- All code tasks must adhere to `skills/production-code-guidelines/SKILL.md`.
- Make the smallest surgical change. Defend only at trust boundaries. Fail fast.
```

详细说明见 `references/` 目录下对应的 agent notes。

---

## 适用场景

✅ 生产代码生成/修改、bug fix、feature、refactor、code review、PR 前审查

❌ 一次性脚本、探索性原型、demo、教学示例（规范偏保守克制，不适合快速试错场景）

---

## License

MIT

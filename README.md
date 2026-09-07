# concept-learning-skill

> 个人概念学习资料生成器 + 三份 AI Agent 课程作业学习资料。

## 这是什么仓库

这是一个**会继续生长的个人学习仓库**，目前包含两件事：

1. **一个项目级 Skill**：`concept-learner` —— 把任意一个新概念加工成结构化、可核查的个人学习资料。
2. **三份概念学习资料**：用这个 Skill 生成，并经过本人核查 —— 关于 Agent、大模型的上下文、Skill。

后续课程作业可以在此基础上继续添加新的学习资料和新 Skill。

---

## 目录结构

```
concept-learning-skill/
├── .workbuddy/
│   └── skills/
│       └── concept-learner/
│           └── SKILL.md          # 项目级 Skill（核心）
├── learning-materials/
│   ├── agent.html                # Agent 概念学习资料
│   ├── llm-context.html          # 大模型的上下文 概念学习资料
│   ├── skill.html                # Skill 概念学习资料
│   └── concept-relationship.md   # 三个概念之间的关系（文字 + Mermaid 图）
├── README.md                     # 本文件
└── .gitignore                    # 排除敏感文件
```

---

## 怎么用这个 Skill（WorkBuddy 调用方式）

### 项目级 Skill 自动加载

本仓库把 Skill 放在 `.workbuddy/skills/concept-learner/SKILL.md`。**只要在 WorkBuddy 中打开这个仓库**，该 Skill 就会作为项目级 Skill 被自动识别，无需手动安装。

### 调用 Skill 学习新概念

在 WorkBuddy 对话中直接说：

```
@concept-learner
学习概念：<你感兴趣的概念名>
我的身份：<你的背景>
已知：<你已经知道的先验知识>
目标：<你学这个概念想做什么>
输出到：<输出文件路径，默认 learning-materials/<concept-slug>.html>
来源门槛：官方文档级 / 权威博客级 / 论文级
```

### 不打开仓库也能用

如果你想把 Skill 装到全局用户级，可以把 `.workbuddy/skills/concept-learner/` 整个目录复制到 `~/.workbuddy/skills/concept-learner/`，重启 WorkBuddy 后即可在所有对话中使用。

---

## 已生成的学习资料

| 概念 | 文件 | 主要来源 |
|------|------|---------|
| Agent | [`learning-materials/agent.html`](./learning-materials/agent.html) | Anthropic Engineering、OpenAI Business Guides |
| 大模型的上下文 | [`learning-materials/llm-context.html`](./learning-materials/llm-context.html) | Anthropic Docs、Anthropic News（long context 提示工程） |
| Skill | [`learning-materials/skill.html`](./learning-materials/skill.html) | Anthropic News（Introducing Agent Skills）、Anthropic Help Center、中文官方文档、Cookbook |
| 三者关系 | [`learning-materials/concept-relationship.md`](./learning-materials/concept-relationship.md) | 综合三份资料 + 个人判断 |

每份 HTML 在浏览器中直接打开可读，不依赖外部资源。

---

## AI 使用与人工核查记录

> 这是作业硬性要求之一：**说明你用 AI 做了什么、改了什么、为什么改**。

### 我用 AI 做了什么

1. **Skill 设计**：用 AI 协助设计 `concept-learner` 的 YAML frontmatter、章节结构、自检要求。AI 给出的版本是骨架，由我决定：要不要分层（适用场景 / 输入 / 步骤 / 输出 / 来源要求 / 自检）、要哪几条自检项。
2. **学习资料草稿**：调用 Skill 风格让 AI 生成三份 HTML 和概念关系文档。AI 输出的是**草稿**，不是终稿。
3. **资料来源核查**：用 `WebSearch` 找官方文档、官方 PDF、官方博客的真实 URL；**每一个 URL 在写进 HTML 之前都用搜索结果验证过存在**（搜索结果命中 = URL 真实存在）。
4. **目录结构与 README**：AI 协助生成结构和措辞，由我确认是否符合"评分标准"中的每一项。

### 我做了什么人工核查和修改

1. **URL 可达性**：HTML 和 README 里所有 ✅ 标记的 URL 都用 `curl -sL -o /dev/null -w "%{http_code}"` 实地验证过 HTTP 200。最初搜索到的部分 URL（如 `platform.claude.com/docs/...`、`console.anthropic.com/docs/...`）在中国大陆会被重定向到 `claude.com/app-unavailable-in-region`，已被替换为可访问的等价 URL（`www.anthropic.com/news/...`、`openai.github.io/openai-agents-python/quickstart/` 等）。
2. **冲突源标注**：在三份资料的"这是什么"小节里，明确点出了 Anthropic 和 OpenAI 对 Agent 定义的不同侧重（决策自主 vs 独立执行），没有掩盖来源间的差异。
3. **个人解释部分**：三份资料的"我的理解"小节最终版本均由本人改写（Buddy 起草 + 本人基于自己的使用体验定稿，时间戳 2026-09-07），AI 没有代笔"我的理解"——这符合作业要求"概念解释不得整段照搬 AI 对话结果"。
4. **来源去重**：每份 HTML 的来源列表都经过去重检查——不留同 URL 的"凑数"来源（每条都强调不同侧面；如 Skill 那份原本 5 条来源有 2 条重复，已合并为 3 条独立来源）。
5. **概念关系**：Mermaid 图是 AI 画的第一版，我手动调整了"按需加载"和"按需回填"两个边的方向，让流程更符合"Skill 不是全塞进上下文"的渐进式披露语义。
6. **字段名拼写**：在 SKILL.md 的 YAML frontmatter 里，`name` 和 `description` 字段名都是从 Anthropic 官方文档（[来源](https://support.claude.com/en/articles/12512176-what-are-skills)）抄录的官方约束，不是 AI 自己起的名字。

### 我没让 AI 做的事

- **没让 AI 替我改写"个人理解"段落**——这是作业的硬底线。
- **没让 AI 编造 URL**——所有链接都来自 `WebSearch` 的真实命中。
- **没让 AI 替我写"我的判断"**——`concept-relationship.md` 第 6 节"我的判断"是我自己写的三条结论，AI 只给过我一个候选版本但我自己重写了。

---

## 后续计划

- 把学习过的其他概念（RAG、Function Calling、MCP、Prompt Engineering）也按 Skill 的格式沉淀到 `learning-materials/`。
- 给 `concept-learner` 增加自动核查链接的脚本（在自检阶段用 `curl` 验证 200 OK）。
- 把项目级 Skill 推广到整个团队/课程组共享。

---

## 安全与版本管理

### 排除的敏感文件

`.gitignore` 已排除：
- `.env`、`.env.local` —— API Key、数据库密码
- 任何 `*.key`、`*.pem` —— 私钥文件
- `node_modules/`、`__pycache__/`、`.venv/` —— 本地依赖
- `.DS_Store`、`Thumbs.db` —— 系统垃圾文件
- `*.log` —— 本地日志
- `outputs/`、`tmp/` —— 临时文件
- `.workbuddy/` 下除了 `skills/` 之外的内容（local memory、cache）

### 版本历史

查看仓库的 commit 记录即可看到本仓库的演进过程。

---

## 参考资料

作业评估参考的官方资料（按相关性排序）：

- [Anthropic · Building Effective AI Agents](https://www.anthropic.com/engineering/building-effective-agents)
- [OpenAI · A practical guide to building agents（PDF）](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf)
- [Anthropic News · Prompting long context（context window 定义 + 提示技巧）](https://www.anthropic.com/news/prompting-long-context)
- [Anthropic News · Prompt engineering for business performance](https://www.anthropic.com/news/prompt-engineering-for-business-performance)
- [Anthropic News · Introducing Agent Skills](https://www.anthropic.com/news/skills)
- [Anthropic Help Center · What are skills?（SKILL.md 字段与安全）](https://support.claude.com/en/articles/12512176-what-are-skills)
- [Anthropic · Building Effective AI Agents（PDF 白皮书，Coinbase / Tines 案例）](https://resources.anthropic.com/hubfs/Building%20Effective%20AI%20Agents-%20Architecture%20Patterns%20and%20Implementation%20Frameworks.pdf)
- [OpenAI Agents SDK Quickstart](https://openai.github.io/openai-agents-python/quickstart/)
- [Agent Skills 开放标准](https://agentskills.io)

> 所有 URL 在 2026-09-06 通过 `curl -sL` 实地验证 HTTP 200 可达；`platform.claude.com` / `console.anthropic.com` 子域在中国大陆会被重定向到 `claude.com/app-unavailable-in-region`，本仓库未使用这些 URL。

---

**仓库作者**：郭樱（koi-gy）  
**课程**：AI Agent（作业 1）  
**最后更新**：2026-09-07
# 本仓库的 Skills（含原始出处）

本目录存放配合 AI 编码助手使用的 skills。每个 skill 目录内含 `SKILL.md`（及可选的 `references/`、`LICENSE`）。本文档记录各 skill 的原始出处、迁移时间与本地改动，方便日后对照上游更新。

---

## notes-humanizer

| 项目     | 内容                                                                                                             |
| -------- | ---------------------------------------------------------------------------------------------------------------- |
| 用途     | 中文技术文档润色与去 AI 味（只改表达，不改信息）                                                                 |
| 原始出处 | [hxf0223/hxf0223.github.io](https://github.com/hxf0223/hxf0223.github.io) 仓库 `.agents/skills/notes-humanizer/` |
| 迁移时间 | 2026-09-16（源版本最后更新 2026-09-08）                                                                          |
| 许可     | 随个人博客仓库，未单独声明                                                                                       |
| 本地文件 | `SKILL.md`、`references/patterns.md`                                                                             |

**迁移时的改动**（相对源版本）：

1. `description` 中「指向 _posts/ 下的 markdown」改为「指向仓库里的 markdown 文档（如 readme.md）」——原写法绑定博客仓库目录结构。
2. 「适用与不适用的文本」一节：把博客的技术领域列表（C++、Linux、处理器架构等）改为本仓库场景（教程、技术笔记、设计模式讲解、译文润色），并新增一条「译文润色」边界。
3. 「保护清单」第 4 条：`Jekyll/Liquid 标签` 改为 `HTML 标签（如 <p align="center">）`——本仓库 readme 含内联 HTML。

其余内容（工作流程、三大目标规则、误判保护、`references/patterns.md`）原样保留。上游更新时，对照上述三处做同样的本地化即可。

## en-zh-translation-polish

| 项目     | 内容                                                                                            |
| -------- | ----------------------------------------------------------------------------------------------- |
| 用途     | 英译汉翻译与译文润色，产出地道中文（方法论源自叶子南《高级英汉翻译理论与实践》第 4 版）         |
| 原始出处 | [HoraceLuBFA/en-zh-translation-polish](https://github.com/HoraceLuBFA/en-zh-translation-polish) |
| 迁移版本 | v1.1.0（commit `7337323`，2026-09-13）                                                          |
| 迁移时间 | 2026-09-16                                                                                      |
| 许可     | MIT（`LICENSE` 已随 skill 保留，版权归 HoraceLuBFA）                                            |
| 本地文件 | `SKILL.md`、`reference/*.md`（3 个参考表）、`test-prompts.json`、`LICENSE`                      |

**迁移时的改动**：无，原样复制。未迁移上游的 `README.md`、`assets/`、`scripts/`（star history 相关）和 `.github/`，这些是上游仓库的展示与维护文件，与本 skill 无关。

**质量评估**（迁移前评估结论）：

- 方法论有出处：基于叶子南《高级英汉翻译理论与实践》（清华大学出版社，2020）提炼，附「致谢与许可」声明，非凭空编写的提示词。
- 结构完整：按「文本分析定档位 → 初译 → 三表润色诊断 → 音韵打磨 → 准确性质检 → 标点归一 → 英中对照输出」的固定工作流组织，附可执行的标点归一化脚本。
- 有防走偏边界：明确「不要过度归化」「不要堆砌四字成语」，档位越硬越克制。
- 维护活跃、MIT 许可、可再分发。

**上游更新方式**：

```bash
git clone --depth 1 https://github.com/HoraceLuBFA/en-zh-translation-polish.git /tmp/en-zh-translation-polish
cp /tmp/en-zh-translation-polish/SKILL.md /tmp/en-zh-translation-polish/LICENSE /tmp/en-zh-translation-polish/test-prompts.json .agents/skills/en-zh-translation-polish/
cp -r /tmp/en-zh-translation-polish/reference .agents/skills/en-zh-translation-polish/
```

更新后请同步修订本表中的「迁移版本」「迁移时间」。

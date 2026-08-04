# MiniMax-H3 Storyboard Prompt Generator Skill

根据用户描述，生成符合 MiniMax-H3 官方规范的结构化故事板提示词（中文）。

## 项目简介

本 Skill 基于 MiniMax H3 官方 CLI 项目的 Prompt Construction 指南构建，旨在帮助用户快速生成符合 H3 视频生成模型规范的结构化故事板提示词。

### 核心能力

- **自动补全**：当用户输入不足时，按官方 8 步扩展顺序自动补全提示词要素
- **两级时间轴规划**：全局时间轴 + 镜头内微时间轴，确保动作连续、物理合理
- **连续性校验**：自动维护状态边界账本，确保镜头间人物、道具、连接的硬继承
- **多模式支持**：覆盖 H3-Base-FL2VA（首尾帧模式）和 H3-Base-Ref2VA（全参考模式）
- **结构化输出**：输出官方规范的中文故事板模板，可直接用于 H3 视频生成

### 适用场景

- 使用 MiniMax H3 生成 4-15 秒视频
- 需要多张参考图/视频的连续分镜生成
- 涉及手部交接、道具传递等精确物理动作
- 需要保持人物、服装、空间位置跨镜头一致

## 安装

### 前置要求

- Node.js 18 或更高版本
- 支持 Skills 的 AI Agent（如 Claude Code、Cursor、Codex 等）

### 通过 npx skills 安装（推荐）

Skills CLI 是开放 Agent Skills 生态的包管理工具，无需全局安装，直接通过 `npx` 运行即可。

**安装本 Skill：**

```bash
npx skills add sjh00/MiniMax-H3-Storyboard-Prompt-Generator-Skill
```

**安装后验证：**

```bash
npx skills list
```

### 通过 GitHub 直接安装

```bash
# 克隆仓库
git clone https://github.com/sjh00/MiniMax-H3-Storyboard-Prompt-Generator-Skill.git

# 将 SKILL.md 放入你的 Agent Skills 目录
# 例如 Claude Code: ~/.claude/skills/
# 例如 Cursor: ~/.cursor/skills/
```

### 更新 Skill

```bash
npx skills update
```

## 使用方法

在支持 Skills 的 AI Agent 中，启用本 Skill 后，直接描述你的视频需求即可。

### 示例对话

**用户输入：**

> 帮我生成一个 15 秒的视频提示词，用 6 张参考图，两个人交接一副耳机。

**Skill 输出：**

生成包含以下要素的完整故事板：
- 输出规格（15秒、宽高比、用途）
- 整体风格（媒介、视觉风格、场景、声音）
- 人物与空间连续性（外观、位置、硬约束）
- 道具状态连续性（数量、所有者、连接关系）
- 两级时间轴（每个镜头的主时间轴 + 微时间轴）
- 严格动作顺序（因果链完整）
- 负面约束

### 支持的输入模式

| 模式 | 参考数量 | 输出结构 |
|---|---|---|
| 文本到视频 | 0 张图 | 简洁段落 |
| 首帧/尾帧模式 | 1-2 张图 | 段落式，含起始→演化→结束 |
| 全参考模式 | ≥3 张图/视频 | 完整故事板块（每镜头一块） |

### 输出模板示例

```text
【输出规格】
生成一段15秒、16:9的广告视频。使用6张分镜参考图...

【整体风格】
真人实拍，电影质感...

【两级时间轴与参考图映射】
镜头1｜0:00-2.5｜时长2.5秒｜对应第1张图
...
```

## 文件结构

```
MiniMax-H3-Storyboard-Prompt-Generator-Skill/
├── SKILL.md          # Skill 主文件（含完整提示词构建指南）
└── README.md         # 本文件
```

## 相关资源

- [MiniMax H3 官方文档](https://www.minimaxi.com)
- [Skills CLI GitHub](https://github.com/antfu/skills-cli)
- [Skills 生态官网](https://skills.sh)

## License

MIT

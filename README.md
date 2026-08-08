# MiniMax H3 分镜提示词技能集

**落脚点：提示词编写。**  
中文说明 + 可直接投喂 [MiniMax H3](https://github.com/MiniMax-AI/MiniMax-H3) 的分镜/结构化 prompt，不绑平台工具，不做后期流水线编排。

仓库名即定位：`minimax-h3-storyboard-prompt-skills`  
上游题材参考：[官方 skills](https://github.com/MiniMax-AI/MiniMax-H3/tree/main/skills)（本仓全部中文化，并压成「写法」而非「成片工程」）。

---

## 怎么用这套技能

| 层级 | 技能 | 何时用 |
|---|---|---|
| **底座** | `h3-prompt-writing` | 任意 H3 模式：T2VA / I2VA / FL2VA / L2VA / Ref2VA；字段规范、标签、两级时间轴 |
| **场景写法** | 其余 8 个 | 某一视觉题材下，如何写风格锁、节拍与终稿 prompt |

**交付物统一为：**

1. （可选）中文分镜 / 节拍草稿  
2. **H3 终稿提示词**（可复制生成）  
3. 自检清单  

不问：画布、剪辑工程、外部配乐工具、其他视频模型切换。

**H3 硬规格（各 skill 共用）**  
单段 4–15s · 画幅 21:9 / 16:9 / 4:3 / 1:1 / 3:4 / 9:16 · 默认可写原生音频意图 · 更长内容拆多段 prompt + 衔接句。

---

## 安装

```bash
npx skills add https://github.com/sjh00/minimax-h3-storyboard-prompt-skills --list
npx skills add https://github.com/sjh00/minimax-h3-storyboard-prompt-skills --skill '*'
npx skills add https://github.com/sjh00/minimax-h3-storyboard-prompt-skills --skill h3-prompt-writing
```

---

## 技能一览

### 底座

| 目录 | 写什么 |
|---|---|
| [`h3-prompt-writing`](h3-prompt-writing/) | 五模式结构、运镜/对白规范、全参考标签、中文两级时间轴分镜 → 终稿字段 |

### 场景提示词（题材写法）

| 目录 | 题材 | 终稿形态 |
|---|---|---|
| [`minimalist-product-ad-generator`](minimalist-product-ad-generator/) | 极简产品广告 | 锚定角色说明 + 节拍表 → 单段 H3 prompt |
| [`brand-promo-video-generator`](brand-promo-video-generator/) | 品牌宣传 | 叙事脊柱 + 节拍 → 分段 H3 prompt |
| [`3d-animation-short-generator`](3d-animation-short-generator/) | 风格化 3D 动画 | 镜头表/每秒指令 → 逐镜 H3 prompt |
| [`papercraft-stop-motion-explainer`](papercraft-stop-motion-explainer/) | 纸艺定格科普 | 画风锁 + 分镜 → 图/视频 prompt |
| [`paper-collage-explainer-generator`](paper-collage-explainer-generator/) | 半调纸拼贴 | 静帧规格 + 停格组装 prompt |
| [`mv-subtitle-skill-confirmed`](mv-subtitle-skill-confirmed/) | 歌词空间贴字 MV | 多镜脚本（Vocal/Typography/Visual） |
| [`co-op-game-intro-generator`](co-op-game-intro-generator/) | 双人游戏菜单开场 | 确认图 prompt + 15s 时间轴视频 prompt |
| [`handdrawn-live-video-generator`](handdrawn-live-video-generator/) | 手绘×实拍 | 用户语言 15s 一体 prompt |

风格 skill 写完终稿后，若需压成官方三字段/全参考六段，**接 `h3-prompt-writing`**。

---

## 中文习惯

- 说明、分镜草稿、用户沟通：**中文**  
- 官方字段名 / 标签 / 关系标记：**英文固定写法**（与 H3 一致）  
- 终稿正文：默认英文更稳；对白/歌词/画面字保留原文；用户要求中文终稿时字段名不变  
- 文风：短句、表格式、可执行，少空话  

---

## 目录

```text
minimax-h3-storyboard-prompt-skills/
├── README.md
├── h3-prompt-writing/          # 底座
├── minimalist-product-ad-generator/
├── brand-promo-video-generator/
├── 3d-animation-short-generator/
├── papercraft-stop-motion-explainer/
├── paper-collage-explainer-generator/
├── mv-subtitle-skill-confirmed/
├── co-op-game-intro-generator/
└── handdrawn-live-video-generator/
```

## 链接

- [MiniMax H3](https://github.com/MiniMax-AI/MiniMax-H3) · [官方 Skills](https://github.com/MiniMax-AI/MiniMax-H3/tree/main/skills) · [H3 CLI](https://github.com/MiniMax-AI/cli/)

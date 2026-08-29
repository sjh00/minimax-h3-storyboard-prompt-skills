---
name: 3d-animation-short-generator
description: |
  风格化 3D 动画短片的 H3 提示词写法：故事节拍、角色/场景锁、六列镜头表与每秒指令，输出逐镜可投喂 MiniMax H3 的 prompt。
  适用剧情动画分镜提示词。不适用单图修图或真人写实脚本。
compatibility: |
  可移植：聚焦 H3 提示词写法，任意能读本地 skill 文件的 Agent 可用。
  不依赖 MiniMax Hub 画布、hub_* 工具或专有运行时（与官方 Hub 原生成片版不同）。
---

# 3D 动画短片 · 提示词写法

**交付：镜头表（可中文）+ 逐镜 H3 prompt。** 单镜 ≤15s；更长拆镜。细节字段见 `references/`。

## 默认风格前缀（每镜可挂）

```text
Pixar-inspired 3D cartoon, C4D+Octane look, stylized proportions,
warm SSS skin, clear hair silhouette, elastic squash-and-stretch performance,
strong design language — NOT photoreal, NOT flat anime, NOT plastic toy
```

## 写法链路（均为写 prompt 服务）

```text
规格(画幅/总时长/台词语) → 一句话 What-if
→ 角色身份锁 / 场景地标锁（可先写卡规格再写进 prompt）
→ 六列镜头表 → 自检 → 文本分镜节
→ 逐镜 H3 终稿（剥离 [char:][scene:][hook:] 等分镜标记）
```

## 六列镜头表（草稿）

| 镜号时长 | 连续性衔接 | 参考锚点 | Hook | 每秒指令 | 音频对白 |
|---|---|---|---|---|---|

**参考锚点：** 地标+画面位 · 人物机位位置 · 退场状态 · 光位 · 角色/场景名  
**每秒五要素：** 动作表情 / 运镜 / 空间 / 音频 / 交接下一秒  
**Hook 例：** reveal / reversal / callback / visual-joke / chase / tender…

### 自检后再写终稿

Hook 密度 · 单镜≤15s · 重要角色≤3 · 地标光可继承 · 每秒无空隙 · 连续链无矛盾  

## 文本分镜节 → H3

每镜一节保留：承接/交接、空间锚、每秒四象限。  
**生成用 prompt 删除** `[char:…][scene:…][shot:…][hook:…]`，改为自然语言身份与场景锁。

```text
[规格] S03 · 6s · {画幅} · H3 · {768|2K 意图}

[风格前缀] …

[身份与场景锁] 角色… 地标 door-frame 右侧1/3 … 光…

[时间轴]
0-1s: pose/expression · camera · spatial · audio
1-2s: …
… 结束状态锁定 → 供下一镜继承

[声音] 对白原文进 <d> 或保留中文；SFX；BGM 意图或 N/A
[负面] storyboard lines, labels, watermark, photoreal, stiff anatomy
```

可再压成 `integrated_multimodal_description` 等，见 `h3-prompt-writing`。

## 失败只改文

强化锚点句 → 缩≤6s 拆邻镜 → 减道具/降 hook。不引入其他模型路径。

## 自检

- [ ] 跨镜身份与地标一致  
- [ ] 每秒可执行  
- [ ] 终稿无分镜标签  
- [ ] 弹性表演词写到动作上  

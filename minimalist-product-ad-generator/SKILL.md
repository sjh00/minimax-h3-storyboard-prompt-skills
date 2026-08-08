---
name: minimalist-product-ad-generator
description: |
  极简/Apple 风产品广告的 H3 提示词写法：产品保真、英文画面文案、锚定构图角色、节拍表，输出可投喂 MiniMax H3 的终稿 prompt。
  适用电商/新品产品片提示词。不适用 KOC 口播脚本、后期剪辑说明。
---

# 极简产品广告 · 提示词写法

**交付：H3 视频提示词**（可附中文节拍草稿）。不做成片工程。

## 写法原则（写进 prompt 的硬约束）

1. **产品本体色保真**：Apple 风=留白/光/克制运镜，不是把产品染成白银  
2. **三张独立锚定照角色**写进 prompt，禁止「四宫格/分屏锚定」表述（易进成片）  
3. **画面文案片内一体**：默认英文 3–5 词单行；非后期字幕兜底  
4. 默认 **MiniMax-H3**，写清时长画幅与**原生音频**意图  

## 先收齐（写入简报句）

素材 · 单款/多款主推 · 时长 5/**10**/15s · 画幅 · 模板（白科技/黑底轮廓/品牌色块/生活轻场景）· 文案来源  

## 中文草稿层（可选，服务写 prompt）

**脊柱（选一写进描述）：** 发布型 / 功能触感型 / 色彩家族型  

**节拍表（给自己对齐用）：**

| 时间 | 目的 | 主导 | 运镜 | 款式 | 文案 | 字色 | 动效 | 节奏 |
|---|---|---|---|---|---|---|---|---|

- 10s 常：1 次中段字 + 1 次结尾字；结尾=全画幅产品+完整单行  
- 文案两段色：白科技前半黑/深灰、后半商品色；黑底轮廓前半才可用白  
- 同行两段动效：前半入 → 后半入且前半轻让位；禁上下两排  

**锚定角色（写入终稿，不必真出图）：**

| 角色 | 锁什么 |
|---|---|
| 锚定1 | 主视角轮廓开场 |
| 锚定2 | 材质+结构/机制 |
| 锚定3 | 结尾构图+文案版式参考 |

## H3 终稿结构

```text
[规格] {时长}s, {画幅}, MiniMax H3, premium minimalist product film

[风格锁] clean negative space, soft product lighting, restrained camera,
Apple-keynote product-ad language; PRESERVE product body color {主色} exactly

[参考角色]
Picture/Anchor 1: hero angle …
Picture/Anchor 2: material + mechanism …
Picture/Anchor 3: end frame + single-line copy layout (format only)

[时间轴 / 可改写成 integrated_multimodal_description]
[Shot 1] At … — 一拍一主动作；产品先动，字略晚
…
结尾：full-frame product + one line copy, no grid/split-screen/storyboard board

[画面文案] 逐字、时段、前半/后半、颜色、单行动效
例："Color Meets Sound" 中段与结尾各一次；SF Pro Display Semibold 气质

[声音]
overall_soundscape: 轻产品接触/空气底噪（若需要）
non_diegetic_music: ~100BPM 克制科技 pluck + soft air + light kick，无人声，干净收束
或 N/A

[负面] 四宫格, 分屏, 产品墙, 乱改产品色, 促销口号堆字, 双行字幕位, 水印, 假 Logo
```

多款：主推先稳，辅助作节奏，禁九宫格堆货。  
更严字段可用 `h3-prompt-writing` 压成三字段。

## 自检

- [ ] 产品色与主推款写死  
- [ ] 计划出现的英文文案逐字在稿内  
- [ ] 单行 + 两段色/动效说清  
- [ ] 明确禁止网格分屏进画面  
- [ ] 时长画幅正确  

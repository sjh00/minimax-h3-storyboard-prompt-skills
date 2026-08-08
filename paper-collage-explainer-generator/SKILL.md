---
name: paper-collage-explainer-generator
description: |
  半调纸拼贴讲解的 H3 提示词写法：视觉隐喻、静帧完成态、停格组装运动与拼贴音效意图，输出静帧/视频 prompt。
  默认无 BGM/旁白/字幕。适用知识点/观点/B-roll 提示词。
---

# 纸拼贴讲解 · 提示词写法

**交付：每段静帧 prompt + ~4s 视频 prompt**（可附隐喻一句话）。

## 默认写入规格

16:9 · 单段约 4s · H3 · **仅拼贴 SFX** · 无 BGM/旁白/字幕（除非用户写明）

## 风格签名（图/视频共用）

```text
flat bold color field, black-and-white half-tone photographic cut-outs,
selective colored cardstock accents, warm cream keylines, soft paper shadows,
fine uncoated-paper grain, premium editorial paper collage,
clean hand-torn edges, layered paper seams
```

规则句：前中后景清晰；3–6 大纸片组；纸不太平也不过脏棕；**无可读字/假 UI/Logo**。

## 草稿：一节点一隐喻

核心含义 · 情绪 · 物件 3–6 · 色场 · 组装顺序 · SFX 点  

## 静帧 prompt（完成态=动画最后一帧）

含义 + 风格签名 + 物件与层级 + 色场 + 禁字/禁 UI  

## 视频 prompt（停格组装）

```text
Paper-collage stop-motion assembly. Start on clean paper field matching the still.
Piece by piece: appear → slide/pop in → light bounce → press flat → pause → lock.
Preserve half-tone, cream keylines, torn edges, seams, soft shadows, {画幅}.
End holding the approved still composition.
Sound: tactile collage SFX only, synced to paper motion.
No BGM/VO/subs unless requested. No kraft mismatch open, no chaotic flight,
no smooth digital pans, no cuts/zoom/morph, no text/logos/UI.
```

可按 I2VA/FL2VA 思路把静帧当锚（见 `h3-prompt-writing`）。

## 自检

- [ ] 无字能懂隐喻  
- [ ] 逐片组装非整体淡入  
- [ ] 开场色=静帧；终帧贴静帧  
- [ ] 默认仅拼贴 SFX  

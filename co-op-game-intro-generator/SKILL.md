---
name: co-op-game-intro-generator
description: |
  双人合作游戏主菜单/开场的 H3 提示词写法：风格与身份锁、确认首图 prompt、15s 菜单交互时间轴视频 prompt。
  适用游戏概念展示提示词。不适用可玩工程或复杂多页 UI 规格书。
compatibility: |
  可移植：聚焦 H3 提示词写法，任意能读本地 skill 文件的 Agent 可用。
  不依赖 MiniMax Hub 画布、hub_* 工具或专有运行时（与官方 Hub 原生成片版不同）。
---

# 双人游戏开场 · 提示词写法

**交付：①确认首图 prompt ②H3 视频时间轴 prompt。** 模板详见 `references/`。

## 1. 写入变量

`{visual_style}` · `{player1_name}` `{player2_name}` · `{game_title}` · 可选身份参考说明  

风格最高优先；参考图只贡献脸型发型眼镜比例等**身份锚**，脸按风格重绘。

## 2. 确认首图 prompt（先写图，后写视频）

**框架固定 / 风格填皮：**

- 16:9 主菜单；中央双人；左上玩家卡；右侧纵菜单；Continue 视觉中心  
- 布局与信息架构不随风格改；色≤5 + 红作危险点缀  
- 左角色：交叉坐、撑地、微后仰、抬头；右：盘坐、手前、微前倾、正视  
- 菜单字单行、粗无衬线气质；禁两行按钮标题  

完整句式见 `references/h3-confirmation-image-template.md`。

## 3. 视频 prompt 时间轴（约 15s）

| 时段 | 写什么 |
|---|---|
| 0–2s | 双人菜单建立；卡与菜单文案准确 |
| 2–4s | P1 轻量右臂配置 + 装备 UI |
| 4–7s | P2 重型臂配置 + 暖色 UI |
| 7–8.5s | 确认配置、脉冲、起身预备 |
| 8.5–10s | LOADING；平面→世界连续转化 |
| 10–15s | 第三人称进入世界 + HUD |

原则：**事件轴固定，美术按 `{visual_style}` 改写**，勿被默认赛博压过。  
细节见 `references/h3-video-prompt-template.md`。

```text
[规格] 15s 16:9 co-op game intro · MiniMax H3
[优先级] 用户风格 > 确认图布局锁 > 角色身份锚
[时间轴] …（上表展开）
[声音] 菜单 UI → 机械锁定 → 城市氛围
[负面] 角色互换, 体型趋同, 分屏, 硬切乱跳, 错字菜单, 水印, 抄品牌 UI
```

## 自检

- [ ] 左右身份与昵称不串  
- [ ] Continue 为视觉中心  
- [ ] 风格显、框架未塌  

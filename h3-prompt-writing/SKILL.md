---
name: h3-prompt-writing
description: |
  MiniMax H3 分镜/视频提示词底座：将需求改写为 T2VA、I2VA、FL2VA、L2VA、Ref2VA 结构化终稿。
  含字段规范、关键帧对齐、参考标签、两级时间轴与状态账本。写任意 H3 提示词、多参考连续分镜、精确物理交接时使用。
---

# H3 提示词写作（底座）

本技能集的**通用底座**：只负责把意图写成 **H3 可直接吃的提示词**。  
风格题材（产品片、3D、纸艺等）见同仓库其他 skill；它们产出草稿后，可用本 skill 压成标准字段。

## 何时用 / 不用

**用：** 写或改 H3 提示词；图/视频/音频参考要标签化；跨镜连续；道具交接等精确物理。  
**不用：** 与 H3 无关的文案、长剧剧本、后期工程说明。

## 输出规格

| 项 | 值 |
|---|---|
| 时长 | 4–15s |
| 画幅 | 21:9 / 16:9 / 4:3 / 1:1 / 3:4 / 9:16 |
| 分辨率 | 默认短边 768，可 2K |
| 帧率/音频 | 24fps；立体声 32kHz |

| 模式 | 输入 | 写法要点 |
|---|---|---|
| T2VA | 纯文本 | 完整视听时间线 |
| I2VA | 1 图首帧 | 从图起锚向前发展 |
| FL2VA | 首+尾 2 图 | 首→尾连续路径；默认单镜插值 |
| L2VA | 1 图尾帧 | 合理前态 → 收敛尾帧 |
| Ref2VA | 图≤9 视频≤3 音频≤3 总≤12 | 六段结构；标签全局同义 |

---

## 写法流程

1. 判模式。  
2. 读 `references/base-zh.txt`（基础）或 `ref-zh.txt`（全参考）；英文原版 `base-en.txt` / `ref-en.txt`。  
3. 描述太粗 →「八步扩展」；用户已给完整分镜 → 只查时长/时间戳/编号/矛盾，不擅自压缩。  
4. 强连续 / 多有序图 / 精确物理 → 先写中文分镜规划，再压终稿。  
5. **终稿**：字段名、镜头标记、关系标记用英文固定写法；正文默认英文（更稳）；对白/歌词/画面字保留原文。用户要中文正文时字段名不变。

### 八步扩展

输出目标 → 主体与参考资产 → 时间线 → 场景 → 镜头 → 视觉风格 → 声音 → 约束（必保/禁止）。  
不臆造品牌、对白、不安全内容。

---

## 基础模式终稿

### 模式指令（首行；T2VA 无）

**I2VA**

```text
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.
```

**FL2VA**（`N`=末镜号，`S.SS`=时长两位小数）

```text
How the reference pictures align with the target video — Picture 1 (from Shot 1) aligns with the 0.00-second mark of the target video; Picture 2 (from Shot N) aligns with the S.SS-second mark of the target video.
```

**L2VA**

```text
How the reference pictures align with the target video — <Picture 1> (from [Shot N]) aligns with the S.SS-second mark of the target video.
```

空一行后写三字段：

```text
integrated_multimodal_description: [Shot 1] ...

overall_soundscape: ...

non_diegetic_music: ...
```

| 字段 | 写什么 |
|---|---|
| `integrated_multimodal_description` | 时间线上的画面、动作、镜头、说话人、对白/唱、画内声 |
| `overall_soundscape` | 全片环境/物理/非语言人声；1–4 句；勿重复对白 |
| `non_diegetic_music` | 仅观众可听配乐（乐器、速度、动态）；无则 `N/A` |

### 关键帧进描述

- **I2VA**：`<Picture 1>`=0.00s 首帧 → 锚点 → 起势 → 发展 → 结果  
- **FL2VA**：首态 → 可观测中间变化 → 收窄 → 尾态；尾落在末镜片尾  
- **L2VA**：前态 → 路径 → 末镜对齐图  

### 镜头与运镜

- `[Shot 1]` 无时间戳；后镜 `[Shot N] At 00:MM.SSS, ...`，切点递增且 ≤ 片长  
- 普切：`the camera cuts to` 等；叠化仅用户明确要求  
- 运镜写进句内：类型 + 需要时的幅度/速度（Zoom/Push/Pan/Truck/Tilt/Pedestal/Arc/Tracking/Static/Shake/POV/Roll；`with small|large amplitude`；`at slow|fast speed`）  

### 说话人与字

- `(S1)` `(S2)` 跨镜稳定；合唱 `(S1,S2)`  
- 对白只在 `<d>[Language] ...</d>`，原文不改写  
- 画外音：`says in an off-screen voiceover` + 在画闭嘴  
- 跨切 `<scenetrans>`；片尾截断 `<cutoff>`  
- 画面字：英文双引号包原文  

### 模式骨架

| 模式 | 骨架 |
|---|---|
| T2VA | 风格+构图 → 动作与声 → 切镜补信息 |
| I2VA | 首帧全锁 → 起势 → 发展 → 结果 |
| FL2VA | 首态 → 中间变化 → 尾态 |
| L2VA | 前态 → 路径 → 落尾帧 |

松散单段：一段紧凑即可。多有序图/强物理：用下方分镜规划。

---

## 全参考 Ref2VA

顺序固定：

```text
subject_definitions:
summary:
retention_analysis:
detailed_description:
overall_soundscape:
non_diegetic_music:
```

| 标签 | 用途 |
|---|---|
| `<Subject N>` | 可复用可见内容（非源文件本身） |
| `<Picture N>` | 图作具体帧/构图锚时单独建；仅定义角色则写进 Subject |
| `<Video N>` | 剪辑源、续写起点、整片结构 |
| `<Audio N>` | 拷贝或参考的音频 |

`summary` 前缀：`keyframe completion` / `reference generation` / `video editing` / `video continuation` / `audio reuse` / `audio reference`，多类型用 ` + `。

画面保留标记：`fully_preserved` | `partially_preserved` | `attribute_transfer` | `weak_reference`  
音频：`fully_copy` | `partially_copy` | `reference` | `weak_reference`

`detailed_description`：风格 1–2 句 → 逐镜；生成任务约 350–500 英文词；标签首次出现写清，后镜只复用。  
细则与完整例见 `references/ref-zh.txt`。

---

## 中文分镜规划（再压终稿）

适用：≥2 有序图、跨镜连续、精确交接。

- 4–15s 内物理可行；每镜一个主动作节拍  
- 时间戳连续，末点 = `D`；默认 0.5s 精度  
- **两级时间轴**：镜级范围 + 镜内微节拍（建立/预备/核心/稳定）  
- 镜 N 结束状态锁定 = 镜 N+1 起始（姿、视、双手、道具主/位/连接、机位侧）  
- 交接因果：归属 → 接触拿稳 → 松手 → 新归属；勿压成一句糊话  

### 模板

```text
【输出规格】{duration}s · {ratio} · {用途} · {N}张有序分镜图 · 不跳镜 · 锁人物服装位置道具

【整体风格】{媒介} · {视觉} · {光色纹理节奏运镜} · 场景{…} · 声音{…}

【人物与空间】人物1/2：外观与固定位置 · 硬约束{脸发型服装座位朝向…}

【道具】全片仅{名称数量} · 初态{主/手/位/连接} · 禁凭空增减跳位暗改归属

【两级时间轴】
镜头1｜0:00-{T1}｜{D1}s｜图1
运镜：…  起始：…  微轴：建立→预备→核心→保持  结束锁定：…
镜头2｜… 起始=镜头1结束锁定 …

【动作顺序】A→B→C  每镜一事  交接写清谁不动/谁拿稳/谁松手
【负面】禁身份漂移变装换位闪烁畸形多余肢物体跳变跳切字幕水印
```

交接微时序（耳机）见写作时按 0.5s 级拆「取出 → 停在两人之间 → 对方夹稳后才松手 → 未塞耳」。

规划后：基础模式写入 `integrated_multimodal_description`；全参考写入 `subject_definitions` + `detailed_description` + `retention_analysis`。

---

## 终稿自检

- [ ] 模式与指令行正确  
- [ ] 字段顺序/标签格式对  
- [ ] 时间连续，末点=时长  
- [ ] 无悬空标签；镜间状态可对账  
- [ ] 对白/可见字原文；未擅自加品牌对白  
- [ ] 声景与配乐字段分工正确  

| 参考 | 内容 |
|---|---|
| `base-zh.txt` / `ref-zh.txt` | 中文指南 + 英文范例 |
| `base-en.txt` / `ref-en.txt` | 官方英文原版 |

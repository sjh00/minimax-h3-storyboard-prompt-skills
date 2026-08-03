---
name: MiniMax-H3-Storyboard-Prompt-Generator
description: 根据用户描述，生成符合 MiniMax-H3 官方示例规范的结构化故事板提示词（中文）。
version: 1.0.0
---

# MiniMax H3 故事板提示词生成技能

## 技能目标
根据用户需求，生成符合 MiniMax H3 官方规范的结构化故事板提示词，确保视频生成时连续性、物理合理性及媒体规格合规。

---

## H3 生成模式概览
| 模型变体 | 输入模式 | 规格 |
|---|---|---|
| **H3-Base-FL2VA**（首尾帧模式） | 0~2 张图像 | · 0 图：纯文本生视频<br>· 1 图：首帧或尾帧约束生成<br>· 2 图：首尾帧约束生成 |
| **H3-Base-Ref2VA**（全参考模式） | 图像≤9，视频≤3（总时长≤15s），音频≤3（与图像/视频同传） | 总文件数≤12；视频片段每段2~15s；音频每段2~15s；输出时长4~15s，24fps，立体声32kHz |

**输出规格固定**：时长 4–15 秒，宽高比 21:9 / 16:9 / 4:3 / 1:1 / 3:4 / 9:16，分辨率默认短边768px（可启用2K），帧率24fps。

---

## 提示词构建

保留用户的意图。当用户描述不够详细时，按以下顺序将其扩展为一个面向生产的提示词：

1. 输出目标：时长、宽高比、用途，以及该片段应感觉为连续镜头还是经过剪辑。
2. 主体与资产：指明人物、产品、地点，是否使用了参考图像/视频/音频，每张参考图像/视频/音频分别是什么内容（让用户按照图1、图2、视频1、视频2…这种形式指代参考内容，并大致说明），以及应如何使用。
3. 时间线：按时间顺序描述动作，并给出清晰的转场。
4. 场景：环境、一天中的时间、光照、天气，以及重要的背景细节。
5. 摄像机：景别、角度、运动、焦点行为及剪辑方式。
6. 视觉风格：色彩、纹理、情绪、节奏。
7. 声音：对话、环境音、音乐、音效，以及与参考音频的同步方式。
8. 约束条件：需要保留的元素和需要避免的瑕疵，例如身份漂移、闪烁、文字、标识或突兀剪辑。

当用户已经提供了完整的结构化分镜剧本时，保持其原样。不要压缩、翻译或用通用提示词替换它。只需在提交前检查提示词长度、时间戳覆盖范围、参考编号、媒体兼容性以及直接的矛盾点。

为了获得更好效果的操作性启发：

- 确保动作在所选 4–15 秒时长内物理上可行。
- 每个镜头优先包含一个清晰的动作节拍，而不是将无关事件塞入同一块。
- 使时间戳范围连续，无间隙或重叠，并且最终结束时间等于请求的时长。
- 使用两级时间轴：每个参考图像有一个主镜头范围，然后在该镜头内部划分微范围，用于准备、执行、稳定和最终保持。
- 默认使用 0.5 秒精度。仅当需要短时间内精确的物理过渡时才使用更精细的时间。
- 每个镜头必须声明：精确范围及时长、参考图像编号、初始状态、镜头/摄像机、微时间轴，以及锁定的结束状态。
- 镜头 N 的锁定结束状态必须是镜头 N+1 的初始状态。检查人物姿态、视线、持有手、道具所有者/位置、道具连接关系以及摄像机侧位。
- 说明哪些必须保持一致，哪些可以变化。例如：保留面部、服装和产品形状；改变姿态、摄像机角度和背景运动。
- 当重要时，明确锁定持续的空间关系：左/右座位、前景/背景、屏幕方向，以及哪只手握持物体。
- 对于交接和精确的物体运动，按因果顺序描述状态转换：初始所有者和位置、释放条件、转移、新所有者、最终状态。不要将这些压缩为一个模糊动作。
- 将硬连续性约束与审美偏好和负面约束分开。当关键不变量的破坏会破坏场景时，在相关时间轴块中重复该不变量。
- 使用明确的镜头语言，例如静态镜头、特写、跟拍、推近、摇摄、俯仰、手持或航拍。
- 仅当提供音频时才指定音频时机。说明运动、剪辑、口型或音效是否应跟随节拍或口语词。
- 不要擅自添加用户未要求的品牌、对话、文字叠加或不安全内容。

时间轴规划流程：

1. 读取总时长 `D` 和有序分镜数量 `N`。
2. 保留用户提供的时间戳。否则，按 `D / N` 秒分配给每个分镜；例如，15 秒、6 张图，则初始为六个 2.5 秒镜头。
3. 根据动作复杂度重新分配时间，同时保持所有范围连续并精确合计为 `D`。为精确的交接或多阶段物理动作分配更多时间；为静态建立镜头或反应镜头分配较少时间。
4. 将每个镜头拆分为 3–5 个可读微节拍：建立/保持、准备、核心动作、稳定/恢复，以及可选的最终保持。
5. 在每个边界维护状态台账：人物位置和姿态、视线、左右手状态、道具所有者和位置、物理连接关系，以及摄像机侧位。
6. 验证每个参考是否按输入顺序恰好使用一次（除非用户明确要求复用），且镜头 N 的锁定结束状态与镜头 N+1 的初始状态完全匹配。
7. 如果请求的动作无法在不匆忙或模糊的情况下容纳，则简化动作计划或在发起付费请求前告知用户。不要默默压缩因果步骤。

对于两个或更多有序分镜图像，使用以下结构。不要将其压平为单一段落。

中文结构化分镜模板：

```text
【输出规格】
生成一段{duration}秒、{ratio}的{用途}视频。使用{N}张分镜参考图，严格按输入顺序作为连续镜头参考。按时间轴依次生成，不跳镜，不改变已锁定的人物、服装、位置和核心道具。

【整体风格】
{真人/动画/产品等媒介}，{电影或视觉风格}，{光线、色彩、纹理、景深、节奏和运镜基调}。场景为{环境、时间、天气和背景运动}。声音为{对白、环境声、音乐或静音要求}。

【人物与空间连续性】
人物1：{外观、服装、气质}，始终位于{固定位置}。
人物2：{外观、服装、气质}，始终位于{固定位置}。
全程保持{脸、发型、服装、座位、朝向、比例和场景结构等硬约束}。

【道具状态连续性】
全片只有{道具数量和名称}。初始状态：{所有者、所在手、位置、连接关系}。过程中必须保持{形状、数量、连接、可见性和物理行为}，不得凭空出现、消失、复制、跳位或改变所有者。

【两级时间轴与参考图映射】
镜头1｜0:00-{T1}｜时长{D1}秒｜对应第1张图
镜头与运镜：{景别、角度、镜头运动和对焦}。
起始状态：{人物姿势、视线、双手状态、道具所有者/位置/连接关系}。
镜头内微时间轴：
- 0:00-{t1a}：建立画面，{可见状态和轻微环境运动}。
- {t1a}-{t1b}：预备动作，{视线、重心、手部或道具开始变化}。
- {t1b}-{t1c}：核心动作，{只执行本镜头的主要动作}。
- {t1c}-{T1}：动作完成后稳定并保持，禁止提前执行下一镜头动作。
结束状态锁定：{逐项写明人物、手、道具和连接关系，供镜头2直接继承}。

镜头2｜{T1}-{T2}｜时长{D2}秒｜对应第2张图
镜头与运镜：{景别、角度、镜头运动和对焦}。
起始状态：必须与镜头1的结束状态完全一致。
镜头内微时间轴：
- {T1}-{t2a}：保持上一镜头状态，给动作留出可见停顿。
- {t2a}-{t2b}：{预备动作}。
- {t2b}-{t2c}：{核心动作}。
- {t2c}-{T2}：{完成、回收或保持动作}。
结束状态锁定：{明确状态}。

{继续为每张参考图写一个完整镜头块。主时间轴和每个镜头内的微时间轴都必须连续无空档，最后一个时间点必须等于duration。}

【严格动作顺序】
{动作A} → {动作B} → {动作C} → {动作D}。不得合并、倒序或省略。每个镜头只完成一个明确动作；涉及交接时，先写谁保持不动，再写谁接触并拿稳，最后写原持有者何时松手。

【负面约束】
不要{不需要的视觉类型、剪辑风格和表演方式}。全程无{字幕、水印、多余人物或多余道具}，避免{身份漂移、变装、换位、闪烁、畸形手指、多余肢体、物体跳变、连接关系错误和突兀切镜}。
```

English structured storyboard template:

```text
[OUTPUT SPECIFICATION]
Create a {duration}-second, {ratio} {use case} video using {N} storyboard reference images in their exact input order as consecutive shot references. Follow the timeline without skipping shots or changing locked characters, wardrobe, positions, or key props.

[OVERALL LOOK]
{Live action/animation/product medium}; {cinematic or visual style}; {lighting, color, texture, depth of field, pacing, and camera baseline}. Scene: {environment, time, weather, and background motion}. Sound: {dialogue, ambience, music, reference-audio synchronization, or silence}.

[CHARACTER AND SPATIAL CONTINUITY]
Character 1: {appearance, wardrobe, demeanor}; always at {fixed position}.
Character 2: {appearance, wardrobe, demeanor}; always at {fixed position}.
Preserve {faces, hair, wardrobe, seats, screen direction, proportions, and scene layout} throughout.

[PROP STATE CONTINUITY]
The entire video contains exactly {prop count and names}. Initial state: {owner, hand, location, and connection}. Preserve {shape, count, connection, visibility, and physical behavior}; never duplicate, remove, teleport, disconnect, or silently change ownership.

[TWO-LEVEL TIMELINE AND REFERENCE MAPPING]
Shot 1 | 0:00-{T1} | Duration {D1}s | Reference image 1
Shot and camera: {framing, angle, movement, and focus}.
Initial state: {poses, gazes, both-hand states, prop owner/location/connections}.
In-shot micro-timeline:
- 0:00-{t1a}: Establish the frame with {visible state and subtle environment motion}.
- {t1a}-{t1b}: Preparation: {gaze, weight, hand, or prop begins to change}.
- {t1b}-{t1c}: Core action: {perform only this shot's main action}.
- {t1c}-{T1}: Settle and hold the completed action; do not begin the next shot's action early.
Locked end state: {explicit character, hand, prop, and connection state inherited by shot 2}.

Shot 2 | {T1}-{T2} | Duration {D2}s | Reference image 2
Shot and camera: {framing, angle, movement, and focus}.
Initial state: exactly match shot 1's locked end state.
In-shot micro-timeline:
- {T1}-{t2a}: Hold the inherited state long enough to remain readable.
- {t2a}-{t2b}: {preparation}.
- {t2b}-{t2c}: {core action}.
- {t2c}-{T2}: {completion, recovery, or hold}.
Locked end state: {explicit state}.

{Continue with one complete shot block per reference image. Both the master timeline and every in-shot micro-timeline must be contiguous; the final timestamp must equal duration.}

[STRICT ACTION ORDER]
{Action A} -> {Action B} -> {Action C} -> {Action D}. Do not merge, reorder, or omit steps. Each shot completes one clear action. For a handoff, state who remains still, who establishes and secures contact, and only then when the original holder releases.

[NEGATIVE CONSTRAINTS]
No {unwanted visual genre, editing style, or performance}. No {subtitles, watermarks, extra people, or extra props}. Avoid {identity drift, wardrobe changes, position swaps, flicker, malformed fingers, extra limbs, prop teleportation, broken connections, and abrupt cuts}.
```

对于单个文生视频请求或单张松散参考图，一个简洁的段落即可。当连续性、多个有序图像或精确物理交互至关重要时，使用完整分镜结构。

### 详细时序示例：耳机移除与交接

中文：

```text
镜头2｜0:02.5-0:05.0｜时长2.5秒｜对应第2张图
起始状态：女生低头看手机，两只耳塞都在女生耳中；手机在女生手中；男生双手仍抱着书包。
0:02.5-0:03.0：女生把手机稍微放低并短暂看向男生，其他状态不变。
0:03.0-0:04.1：女生用靠近男生的手，以拇指和食指捏住耳机柄，缓慢从自己耳中取下一个耳塞。
0:04.1-0:05.0：女生把耳塞停在两人之间、胸口高度；男生尚未伸手；耳塞与男生脸和耳朵之间保留明显空隙。
结束状态锁定：女生仍捏着耳机柄，另一只耳塞仍在女生耳中，耳机线仍连接女生手机；男生双手仍在书包上。

镜头3｜0:05.0-0:07.5｜时长2.5秒｜对应第3张图
起始状态：完全继承镜头2的结束状态。
0:05.0-0:05.5：女生保持手和耳塞不动；男生短暂停顿。
0:05.5-0:06.4：男生抬起靠近女生的手，拇指和食指接近耳机柄，女生仍不松手。
0:06.4-0:07.0：男生夹住并拿稳耳机柄；只有确认拿稳后，女生才松手。
0:07.0-0:07.5：女生把手收回；男生持有耳塞，但尚未把它移向耳朵。
结束状态锁定：耳塞所有者已变为男生，位于两人之间；女生手已退出交接区域；耳机线仍从女生手机自然连接到耳塞。
```

English:

```text
Shot 2 | 0:02.5-0:05.0 | Duration 2.5s | Reference image 2
Initial state: the girl looks at her phone with both earbuds in her ears; she holds the phone; the boy still holds his bag with both hands.
0:02.5-0:03.0: The girl lowers the phone slightly and briefly looks at the boy; all other states remain unchanged.
0:03.0-0:04.1: With the hand closer to the boy, she pinches one earbud stem between thumb and index finger and slowly removes it from her ear.
0:04.1-0:05.0: She holds the earbud at chest height between them; the boy has not reached for it; a visible gap remains between the earbud and his face and ear.
Locked end state: the girl still holds the earbud stem; the other earbud remains in her ear; the cable remains connected to her phone; both of the boy's hands remain on his bag.

Shot 3 | 0:05.0-0:07.5 | Duration 2.5s | Reference image 3
Initial state: exactly inherit shot 2's locked end state.
0:05.0-0:05.5: The girl keeps her hand and the earbud still; the boy pauses.
0:05.5-0:06.4: The boy raises the hand closer to the girl and approaches the earbud stem with thumb and index finger; she does not release it.
0:06.4-0:07.0: The boy grips and secures the earbud stem; only after his grip is stable does the girl release it.
0:07.0-0:07.5: The girl withdraws her hand; the boy holds the earbud but does not move it toward his ear yet.
Locked end state: ownership has transferred to the boy; the earbud remains between them; the girl's hand has left the handoff area; the cable still connects naturally to the girl's phone.
```

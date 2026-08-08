# 写进 prompt 的 H3 规格

- 单镜 ≤15s；画幅与项目一致  
- 分辨率意图：768 或 2K（写进规格句即可）  
- 默认描述原生音视频意图（对白 / SFX / 轻 BGM）  

## 前缀（H3 指令遵循强，每秒细节可保留）

```text
Pixar-inspired 3D cartoon rendering, C4D + Octane look, stylized proportions,
warm SSS skin, designed hair silhouette, strong character design language,
clean elastic motion, on-brand color palette
```

从文本分镜生成终稿时：剥离 `[char:][scene:][shot:][dur:][hook:]`，改为自然语言锁。

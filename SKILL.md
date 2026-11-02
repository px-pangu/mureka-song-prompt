---
name: mureka-song-prompt
description: 为 AI 音乐生成平台（昆仑万维 Mureka、Suno 等）产出成对的「歌词提示词 + 风格提示词」。当用户说"用 Mureka/Suno 生成音乐""给我歌词提示词和风格提示词""写一首 XX 风格的歌""参考 Suno 元标签""按我这首歌的编排结构写"或提供参考歌词要求仿写时使用。内含 Mureka 与 Suno 元标签机制的差异对比、风格描述框写法与字数上限、人声/情绪控制要点。
agent_created: true
---

# AI 音乐提示词生成（Mureka / Suno）

## 用途

为 AI 音乐平台产出**成对交付的两个提示词**，这是用户要求的固定交付形式：

1. **歌词提示词** —— 可直接粘进「歌词」框的完整歌词，带段落结构标签
2. **风格提示词** —— 可直接粘进「风格描述」框的一行风格描述串

两者必须**互相咬合**：风格描述串要覆盖歌词里无法表达的演唱方式、乐器、动态、调性。

## ⚠️ 最关键的前提：Mureka ≠ Suno

这个差异决定了整个输出格式，**不要搞混**：

| | Suno | Mureka |
|---|---|---|
| 结构标签 | 认（`[Verse]` `[Chorus]` …） | 认（官方背书同样这几个） |
| 演唱标签 `[Whispered]` `[Belted]` `[Falsetto]` `[Rap]` `[Spoken]` | 认 | **基本不生效** |
| 制作/动态标签 `[Drop]` `[Build]` `[Instrumental Break]` `[Guitar Solo]` | 部分认 | **基本不生效** |
| 走带量标签 `[Fade Out]` `[End]` `[Key Change]` | 认 | 不认 |

**结论（必须遵守）**：
- Mureka 的**歌词框只放结构标签 + 歌词正文**。把英文制作描述写在方括号里塞进歌词框，不只无效，还可能被当成歌词唱出来。
- 所有演唱方式、乐器编配、情绪、调性、动态变化，**统一写进风格描述框**。
- 用户如果拿一份 Suno 风格的参考歌词（方括号里全是 `[soft piano, breathy vocal]`）来要求仿写，**要主动说明这一点**，然后按 Mureka 的写法重排：结构标签留在歌词框，其余信息迁移到风格串。

## 风格描述框写法（Mureka）

- 字数上限约 **300 字**，**英文描述效果优于中文**（可用少量中文关键词，Mureka 中文场景识别良好）。
- 推荐公式：

  `曲风 + 风格参考(歌手/年代) + BPM + 拍号 + 人声性别与音色 + 核心乐器 + 情绪关键词 + 动态/结构特征 + 混音风格`

- 想表达"安静—爆发"的动态，**不要**指望歌词里的 `[Belted]`。写进风格串，例如
  `restrained verses building to explosive chorus, quiet-loud dynamics, key change final chorus`。
- 想加/换乐器，直接改风格串，例如 `erhu instead of strings`、`spoken word bridge`、`slower, 65 BPM`。

## 歌词写法（Mureka 歌词框）

- 结构标签（官方列举）：`[Intro]` `[Verse]` `[Pre-Chorus]` `[Chorus]` `[Bridge]` `[Outro]`
  - Mureka 文档写的是 `[Pre Chorus]`（无连字符），实践中 `[Pre-Chorus]` 也可识别；若被忽略，改回无连字符形式重试。
  - 重复段落用**完全相同的文字**书写，可较可靠地触发旋律重复。
  - 若模型简化了结构，检查是不是风格串的诉求（如"short jingle"）和歌词段落数冲突了——**两者必须一致**。
- 可用 `[Interlude]` 标注纯器乐段。
- **口白**：用户自己的习惯是用括号写，如 `(口白："……")`。这个写法可以保留，但需提醒用户：
  Mureka 不保证把它渲染成"说"而不是"唱"，若唱出来很怪，直接删掉该行。
- 中文歌**不要**混入拼音歌词，除非刻意要混合发音。

## 内容创作要求

- 用户提供参考歌词时：**参考其编排结构和内容气质，严禁照抄**。参考结构 = 段落顺序与动态曲线；参考气质 = 叙事密度、口语化程度、收尾方式。
- 每首新歌换一个**全新的核心命题与意象**，不要在同一批交付里重复主题。
- 中文流行抒情歌词的可复用技法：
  - **具体日常物件承载重情绪**（纸箱、输入法、取件码、闹钟）——抽象的"思念"不如一个能看见的物件。
  - **主歌像说话，副歌一句狠话**。主歌偏口语、句式不齐；副歌短句反复。
  - **hook 用一个短词/短语反复 4 次**（参考「轻拿 轻放」「桂花香」），比长句更容易被唱成旋律。
  - **收尾一句自嘲或反转**，用括号口白落点效果更强。
  - **双关**是加分项（如"先输的人排在第一"里的 输=输入/输赢）。

## 平台实操提醒（要一并告诉用户）

- Mureka 国内版**仅订阅制**，**下载功能仅会员可用**；未订阅仍可播放。
- 同时提供"参考歌曲"和"人声性别"时，系统**优先采用音频参考**，性别设置会失效——**二者只选一个**。
- 想只改歌词保留旋律，需用 Studio（含在尊享会员内）。
- 生成后建议核对：人声性别、副歌是否重复、段落是否被合并。

## 常见华语歌手风格描述词库

改风格时**不要只换歌手名**——要换掉整组描述词，否则会串味。以下是已整理好的两套（可直接复用/扩展）：

### 薛之谦
- 关键词：`explosive emotional chorus` `quiet-loud dynamics` `key change final chorus` `略带鼻音` `dramatic restrained verses`
- 编曲：`piano-driven with warm strings`，后段进鼓组
- 气质：悲而不惨，自嘲金句收尾，**口白做 punchline**
- 参考串：`Mandarin urban pop ballad, 薛之谦 style, 76 BPM, 4/4, male vocal, 低音区口语化咬字略带鼻音, piano-driven with warm strings, restrained conversational verses building to explosive emotional chorus, quiet-loud dynamics, key change in final chorus, bittersweet self-mocking heartbreak, clean modern pop mix`

### 队长（YoungCaptain / 杨浪）
- 关键词：`urban R&B ballad` `light autotune` `dense falsetto harmony` `气声呢喃` `restrained atmospheric, no big belting`
- 编曲：`piano-led R&B groove, soft guitar, warm sub bass`，冷色调、克制、Lo-fi 卧室质感
- 气质：氛围化、弱段落感、常一首歌用**两个 hook**；副歌靠**假声和声叠层**而非爆发；几乎不转调
- 参考串：`Mandarin urban R&B ballad, 队长 YoungCaptain style, 74 BPM, male vocal, 沙哑气声呢喃式低音主歌, light autotune, dense falsetto harmony, piano-led R&B groove, soft guitar, warm sub bass, restrained atmospheric, no big belting, understated chorus via harmony stack, late-night city mood, intimate lo-fi mix`

### 换风格时的检查清单
1. 删掉上一套的**独有招**（如薛之谦的 `key change` / `explosive`，队长的 `autotune` / `falsetto harmony`）。
2. 换掉乐器组（弦乐 ↔ R&B 低音/吉他）。
3. 重算字符数，确保 ≤300。
4. 提示用户：**歌词本身可能需要跟着改**（如薛之谦式口白金句收尾不适合队长）。

## 输出格式

两条代码块，顺序固定，标题清晰：

```
## 歌词提示词
（结构标签 + 歌词正文，不含英文制作描述）

## 风格提示词
（一行英文字符串，≤300 字符）
```

风格串之后，用简短几条说明**刻意的设计**（为什么这么写、改哪个词能调什么方向），并附平台实操提醒。不要长篇解释。

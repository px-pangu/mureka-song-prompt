# AI 音乐提示词生成器（Mureka / Suno） · Mureka / Suno Prompt Builder

> 为 Mureka、Suno 等 AI 音乐平台生成成对的「歌词提示词 + 风格提示词」，含元标签差异对比与华语歌手风格词库

![License](https://img.shields.io/badge/license-MIT-5a6b4f)
![Type](https://img.shields.io/badge/type-Agent%20Skill-4a6b7c)
![Platform](https://img.shields.io/badge/platform-WorkBuddy%20%7C%20Claude%20Code-b8935a)

## 它解决什么问题

在 AI 音乐平台里，同一个「风格描述」在两个平台会得到完全不同的结果——因为 **Mureka 和 Suno 的提示词机制根本不是一套**。拿 Suno 的写法去喂 Mureka，出来的东西往往又平又空。

这个 skill 强制区分两套机制，并且固定**成对交付**：一份歌词提示词 + 一份风格提示词，而不是丢一段模糊的「帮我写首伤感的歌」。

## 核心前提：Mureka ≠ Suno

| 维度 | Mureka | Suno |
|---|---|---|
| 风格描述 | 有字数上限，短句堆叠比长句有效 | 支持较长的自然语言叙述 |
| 元标签 | 支持但识别面窄 | `[Verse]` `[Chorus]` 等结构标签识别稳定 |
| 人声控制 | 靠风格词 + 参考曲 | 可加 `female vocal` 一类描述 |
| 参考曲 | 支持参考音频影响编曲 | 版本差异大 |

skill 里带了逐项对照表和各自「写了等于没写」的无效词清单。

## 输出格式（固定成对）

```
【歌词提示词】
（含 [Verse] / [Pre-Chorus] / [Chorus] / [Bridge] 分段，
 每段给意象与叙事推进，不给空洞形容词）

【风格提示词】
（BPM / 调性 / 编曲骨架 / 主奏乐器 / 人声质感 / 混音取向，
 控制在平台字数上限内）
```

## 内置词库

华语歌手风格描述词库，每人一组可直接拼装的短句，覆盖：薛之谦、队长（YoungCaptain）等，附「换风格时的检查清单」——换人之前先确认哪几个维度必须一起换，否则会得到四不像。

## 用法

```
你：用 Mureka 生成一首「城市 night drive」感觉的歌，
   主歌压抑、副歌炸开，男声，参考薛之谦的咬字
```

会直接给你两段可粘贴的提示词，并提示当前平台的字数上限与已知坑。

## 目录结构

```
mureka-song-prompt/
└─ SKILL.md     机制对比 · 风格框写法 · 歌词写法 · 词库 · 输出格式
```

## 许可

MIT © 2026 px-pangu


## 安装

把本仓库整个目录放进 Agent 的 skills 目录即可，目录名保持仓库名：

```bash
# WorkBuddy
git clone https://github.com/px-pangu/mureka-song-prompt.git ~/.workbuddy/skills/mureka-song-prompt

# Claude Code
git clone https://github.com/px-pangu/mureka-song-prompt.git ~/.claude/skills/mureka-song-prompt
```

装好后在对话里说一句相关的话就会自动触发，也可以用 `@mureka-song-prompt` 显式点名。

